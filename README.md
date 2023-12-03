# Tutorial: Self-Hosted Node.js App Deployment on On-Premise and Cloud Servers with CI/CD

# Create and EC2 on AWS

### 1. Type "EC2"
![Step 1 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/de2daf92-ba1d-4483-951e-e2fbe48ada52/d01b25f2-19af-4142-ba4b-afe641183521.png?crop=focalpoint&fit=crop&fp-x=0.3130&fp-y=0.0271&fp-z=1.5599&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=267&mark-y=7&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz02MzgmaD02MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 2. Click on EC2
![Step 2 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/0225e2b3-dcbb-48c5-9494-87e69232401c/4acebbb8-dfb1-47dd-9896-3a6c450d7a90.png?crop=focalpoint&fit=crop&fp-x=0.4243&fp-y=0.2492&fp-z=2.9962&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=539&mark-y=402&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0xMjEmaD04MCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 3. Click on Launch instance
![Step 3 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/686d8423-1e73-4e30-b291-a4209a8f0281/58699548-c24a-4244-8f20-ffe9cfc7523d.png?crop=focalpoint&fit=crop&fp-x=0.3224&fp-y=0.6319&fp-z=2.3050&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=415&mark-y=395&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zNzAmaD05NiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 4. Type a name for your server
![Step 4 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/9a4e096c-f943-457f-8481-6465f34f04a1/c8f31aa1-d393-4e0c-b5a2-bf41f2773abd.png?crop=focalpoint&fit=crop&fp-x=0.3303&fp-y=0.4330&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=125&mark-y=417&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 5. Choose Ubutnu
![Step 5 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/064e8ece-005a-4ca5-a63a-c51e28f90abc/5ffb3b07-5252-4b7d-b624-b30cddac8fd7.png?crop=focalpoint&fit=crop&fp-x=0.2979&fp-y=0.6237&fp-z=2.1988&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=486&mark-y=290&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0yMjgmaD0zMDUmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 6. Choose Amazon Machine Image (AMI)
![Step 6 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/91e2357e-5650-4f99-8490-ce03162d2cd9/013cc38f-a339-42c7-a846-af0eafa1bc6c.png?crop=focalpoint&fit=crop&fp-x=0.4144&fp-y=0.6787&fp-z=1.0903&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=108&mark-y=535&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz04NjgmaD04MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 7. Click on Ubuntu Server 22.04 LTS (HVM), SSD Volume Type…
![Step 7 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/2cdef9d2-ae39-464f-8254-a231deb93a24/886a4863-5de4-414a-a7b1-dff07a2532d5.png?crop=focalpoint&fit=crop&fp-x=0.4144&fp-y=0.2255&fp-z=1.0903&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=108&mark-y=177&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz04NjgmaD04MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 8. Choose Instance type
![Step 8 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/fee14828-f2ad-4ce3-969d-171cbdf979c9/1ee59054-fe3e-426b-b57c-9378eba23bf8.png?crop=focalpoint&fit=crop&fp-x=0.3259&fp-y=0.5947&fp-z=1.2718&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=126&mark-y=364&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDImaD0xNTgmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 9. Searching t3.medium for server with 2vCPU and 4GB Ram.
![Step 9 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/7c61f83d-dc09-4843-b29f-c91b98874812/e6e37674-60d3-46f4-8ba6-2ac194579f96.png?crop=focalpoint&fit=crop&fp-x=0.3259&fp-y=0.1660&fp-z=1.2718&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=126&mark-y=161&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDImaD01MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 10. Click on t3.medium. If you want more RAM, you can choose t3.large.
![Step 10 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/63218ee3-e83a-4825-adcc-1ce6da9597de/a5fb0c31-9628-481f-92da-27069331e2e4.png?crop=focalpoint&fit=crop&fp-x=0.3259&fp-y=0.4622&fp-z=1.2718&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=126&mark-y=362&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDImaD0xNjEmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 11. Key pair (login). Click create new key pair. This will use for login to server and using in CI/CD
![Step 11 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/a6c470c5-4a36-46a0-92f0-e372b6183b7c/dd1eb541-351a-4d51-a248-5da6e5f78ffa.png?crop=focalpoint&fit=crop&fp-x=0.6678&fp-y=0.6213&fp-z=2.5660&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=423&mark-y=403&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zNTQmaD04MCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 12. Type Key pair name. Example "self-hosted"
![Step 12 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/b298522e-5513-42f8-920e-ab7fc3b4ea25/56dfc6f3-7b73-4f82-932a-fd474b21784d.png?crop=focalpoint&fit=crop&fp-x=0.5173&fp-y=0.3207&fp-z=1.3736&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=196&mark-y=362&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz04MDkmaD01NyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 13. Click on Create key pair in this popup
![Step 13 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/35ccba9d-916b-44be-a087-c6761b058eb3/975fd719-2e10-4f9a-adfe-2125ae17a228.png?crop=focalpoint&fit=crop&fp-x=0.6966&fp-y=0.8580&fp-z=2.7106&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=387&mark-y=488&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00MjYmaD0xMTImZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 14. Check Allow HTTPS traffic from the internet (For SSL later)
![Step 14 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/094152ad-db5e-4c83-8331-cd41a5e4325c/8c3bf87a-7229-45c2-8842-c2233bfc2f09.png?crop=focalpoint&fit=crop&fp-x=0.0922&fp-y=0.7872&fp-z=3.1364&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=312&mark-y=407&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03MSZoPTcxJmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D)


### 15. Check Allow HTTP traffic from the internet (For port 80)
![Step 15 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/e60ea2d8-b43e-4163-97d5-4c31d4c5e87f/b10ab31d-6d0e-4b03-90e6-19e3bf43f75b.png?crop=focalpoint&fit=crop&fp-x=0.0922&fp-y=0.8457&fp-z=3.1364&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=312&mark-y=422&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03MSZoPTcxJmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D)


### 16. Choose storage size for SSD in "EBS Volumes". Example 32GB
![Step 16 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/ccb7258b-c92c-4feb-a56b-3c27dbce230b/a79e1dbd-5f86-48d9-9ec6-3ba5661b37f7.png?crop=focalpoint&fit=crop&fp-x=0.1900&fp-y=0.8271&fp-z=1.9444&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=193&mark-y=547&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz01MDAmaD04MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 17. Change Volume type (SSD Type).
![Step 17 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/927c841c-f36d-416d-8a43-ef3851eed86b/494840ff-8624-4fb7-a9f8-26a38433adc7.png?crop=focalpoint&fit=crop&fp-x=0.4144&fp-y=0.8271&fp-z=1.9444&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=350&mark-y=547&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz01MDAmaD04MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 18. Click on General purpose SSD (gp3)…
![Step 18 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/3d9d75b7-8a3c-40f0-8d9b-c27f227b053a/b017e486-d9b5-44e3-b106-f80c2f3e7e63.png?crop=focalpoint&fit=crop&fp-x=0.4144&fp-y=0.5713&fp-z=1.9444&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=350&mark-y=402&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz01MDAmaD04MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 19. Click on Advanced details. To setup terminate protection, Cloudwatch Detailed Monitoring and UserData (For preinstall some of software we need)
![Step 19 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/4ed5a6c1-64da-4634-becb-4bad2435babb/6e1847d3-068e-4707-8ac4-14c2f3600214.png?crop=focalpoint&fit=crop&fp-x=0.1576&fp-y=0.4553&fp-z=2.2246&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=221&mark-y=408&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zOTkmaD02OSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 20. Enable Termination protection
![Step 20 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/d4084a31-41ab-4586-b420-a01693528180/455469f5-1213-4023-aee3-27c46229730b.png?crop=focalpoint&fit=crop&fp-x=0.3303&fp-y=0.7043&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=125&mark-y=530&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 21. Enable Detailed CloudWatch monitoring
![Step 21 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/15f2ef58-bebc-4e39-829d-d8356bdf7bb3/e7c93a74-3662-4dc3-968b-913a551230ea.png?crop=focalpoint&fit=crop&fp-x=0.3303&fp-y=0.7351&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=125&mark-y=564&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 22. Scrolldown to User data - optional

Add this content below:

```sh
#!/bin/bash
sudo apt update -y

# Install Docker and Nginx using Snap
sudo snap install docker
sudo snap install nginx

# Grant permission for run Docker without root user
sudo chmod 666 /var/run/docker.sock

# Install Certbot for Let's Encrypt
sudo apt install -y certbot python3-certbot-nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

![Step 22 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/0d313b05-6cf5-4f7c-804f-3efa238b5e45/bc224a1b-2086-4a2e-9098-68c5aeb1e659.png?crop=focalpoint&fit=crop&fp-x=0.3303&fp-y=0.5585&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=125&mark-y=216&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD00NTQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 23. Click on Launch instance
![Step 23 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/5c28d19e-2bac-443c-b7e2-d6987bad8edc/2528bb9d-3b06-432d-a4e2-f2a8f5ec7362.png?crop=focalpoint&fit=crop&fp-x=0.6774&fp-y=0.8638&fp-z=2.5557&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=389&mark-y=524&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00MjEmaD0xMDYmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)
