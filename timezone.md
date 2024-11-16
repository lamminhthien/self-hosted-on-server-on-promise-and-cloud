# **Document: Handling Date-Time data in React.js and NestJS**

This document provides updated guidelines for consistent handling of `start_date` and `end_date` (or `expiry_date`) in campaign-related modules like **points strategy**, **expiry strategy**, and **campaign manager**. It addresses frontend and backend responsibilities to ensure data integrity and consistency.

---

## **Context and Challenges**

### **Existing Issue**
1. The frontend does not ensure proper timestamp formatting for `start_date` and `end_date`.
2. The backend receives and stores dates in inconsistent formats, leading to data integrity issues.

### **Objective**
1. **Frontend (FE):**
   - Ensure `start_date` is submitted in **start-of-day UTC** format:  
     `YYYY-MM-DDT00:00:00.000Z`
   - Ensure `end_date` (or `expiry_date`) is submitted in **end-of-day UTC** format:  
     `YYYY-MM-DDT23:59:59.999Z`

2. **Backend (BE):**
   - Regardless of the format received, normalize and store:
     - `start_date` as: `YYYY-MM-DDT00:00:00.000Z`  
     - `end_date` (or `expiry_date`) as: `YYYY-MM-DDT23:59:59.999Z`

---

## **Frontend Implementation**

The frontend ensures all dates are formatted before submission to the backend.

### **1. Submitting Dates**

When users select a date, the frontend formats:
- `start_date` to **start-of-day UTC** (`00:00:00.000Z`).
- `end_date` (or `expiry_date`) to **end-of-day UTC** (`23:59:59.999Z`).

#### **Using Day.js**
```javascript
import dayjs from 'dayjs';
import utc from 'dayjs/plugin/utc';

dayjs.extend(utc);

function formatDatesForSubmission(selectedStartDate, selectedEndDate) {
  // Format start_date as start-of-day UTC
  const start_date = dayjs(selectedStartDate).utc().startOf('day').toISOString();

  // Format end_date as end-of-day UTC
  const end_date = dayjs(selectedEndDate).utc().endOf('day').toISOString();

  return { start_date, end_date };
}

// Example usage
const { start_date, end_date } = formatDatesForSubmission('2024-11-15', '2024-12-05');
console.log(start_date); // Outputs: "2024-11-15T00:00:00.000Z"
console.log(end_date);   // Outputs: "2024-12-05T23:59:59.999Z"
```

#### **Using Moment.js**
```javascript
import moment from 'moment';

function formatDatesForSubmission(selectedStartDate, selectedEndDate) {
  // Format start_date as start-of-day UTC
  const start_date = moment(selectedStartDate).utc().startOf('day').toISOString();

  // Format end_date as end-of-day UTC
  const end_date = moment(selectedEndDate).utc().endOf('day').toISOString();

  return { start_date, end_date };
}

// Example usage
const { start_date, end_date } = formatDatesForSubmission('2024-11-15', '2024-12-05');
console.log(start_date); // Outputs: "2024-11-15T00:00:00.000Z"
console.log(end_date);   // Outputs: "2024-12-05T23:59:59.999Z"
```

---

### **2. Handling Dates From Backend**

The frontend displays dates formatted for the user without timezone shifts.

#### **Using Day.js**
```javascript
function formatDatesForDisplay(dateString) {
  return dayjs(dateString).format('DD/MM/YYYY'); // Example: 15/11/2024
}
```

#### **Using Moment.js**
```javascript
function formatDatesForDisplay(dateString) {
  return moment(dateString).format('DD/MM/YYYY'); // Example: 15/11/2024
}
```

---

## **Backend Implementation**

The backend ensures all dates are normalized to UTC before storage.

### **1. Validating and Normalizing Incoming Dates**

Normalize dates to the correct format regardless of the input.

#### **Using Day.js**
```typescript
import dayjs from 'dayjs';
import utc from 'dayjs/plugin/utc';

dayjs.extend(utc);

@Injectable()
export class DateService {
  normalizeDates(startDate: string, endDate: string) {
    const start_date = dayjs(startDate).utc().startOf('day').toISOString(); // "YYYY-MM-DDT00:00:00.000Z"
    const end_date = dayjs(endDate).utc().endOf('day').toISOString();       // "YYYY-MM-DDT23:59:59.999Z"

    return { start_date, end_date };
  }
}
```

#### **Using Moment.js**
```typescript
import moment from 'moment';

@Injectable()
export class DateService {
  normalizeDates(startDate: string, endDate: string) {
    const start_date = moment(startDate).utc().startOf('day').toISOString(); // "YYYY-MM-DDT00:00:00.000Z"
    const end_date = moment(endDate).utc().endOf('day').toISOString();       // "YYYY-MM-DDT23:59:59.999Z"

    return { start_date, end_date };
  }
}
```

---

### **2. Storing Normalized Dates**

Save the normalized dates directly to the database.

#### Example Controller:
```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { DateService } from './date.service';

@Controller('campaign')
export class CampaignController {
  constructor(private readonly dateService: DateService) {}

  @Post('dates')
  saveDates(@Body() body: { startDate: string; endDate: string }) {
    const { start_date, end_date } = this.dateService.normalizeDates(body.startDate, body.endDate);

    // Logic to save start_date and end_date in the database
    return { start_date, end_date };
  }
}
```

---

## **Cron Job Integration**

### **Why Normalize to UTC?**
Cron jobs are timezone-specific, and UTC normalization ensures that:
1. **Consistency:** Dates are stored in a universal format.
2. **Ease of Conversion:** Start and end dates can be easily converted to any timezone for cron job scheduling.

### **Example: Converting UTC for Cron Jobs**
```typescript
import moment from 'moment-timezone';

function scheduleCronJob(utcDate: string, timezone: string) {
  const localDate = moment(utcDate).tz(timezone).format('YYYY-MM-DD HH:mm:ss');
  console.log(`Cron job scheduled for: ${localDate} in ${timezone}`);
}

// Example usage
scheduleCronJob('2024-11-15T00:00:00.000Z', 'Asia/Bangkok'); // Outputs: "2024-11-15 07:00:00 in Asia/Bangkok"
```

---

## **Best Practices**
1. **Frontend:**
   - Always submit `start_date` and `end_date` in UTC (`start_date` at the start of the day, `end_date` at the end of the day).
   - Format dates explicitly for user display.
2. **Backend:**
   - Validate and normalize all incoming dates to UTC before storage.
   - Ensure consistent storage format (`start_date`: `YYYY-MM-DDT00:00:00.000Z`, `end_date`: `YYYY-MM-DDT23:59:59.999Z`).
3. **Cron Jobs:**
   - Use stored UTC dates and convert them to the required timezone dynamically.
   - Regularly test timezone-specific scheduling to ensure accuracy.

By following this approach, the frontend and backend can work together seamlessly to ensure data integrity and consistency, even across timezone-specific scenarios.
