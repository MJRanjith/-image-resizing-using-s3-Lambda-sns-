# -image-resizing-using-s3-Lambda-sns-

# Automated Image Resizing and Transfer System Using AWS Services

## Project Description:
This project focuses on building an automated system for image processing and management within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.

## Key Features:
1. Image processing automation: Automatically resize and optimize images upon upload.
2. Secure storage: Store processed images in a secure and reliable S3 bucket.
3. Real-time notifications: Receive immediate updates about image processing via SNS.
4. Scalable architecture: Design for scalability to handle image processing demands.
5. Cost-efficient solution: Leverage AWS serverless technologies to minimize operational costs.

## Overview :

![a1](https://github.com/itz-mathesh/image-resizing-using-s3-lambda-and-sns/assets/144098846/d806e90a-365e-4f59-a6ac-2606c74b79e3)



## Steps :
### Step 1 :
### Creating Source and Designation s3 Buckets :

1. Navigate to the S3 Console.
2. Follow the Outlined Steps below.

![2](https://github.com/user-attachments/assets/082e4cbf-4892-458d-bc76-974ce4e36ca7)


![3](https://github.com/user-attachments/assets/b9467764-9800-40d9-8469-93f65758de25)


![4](https://github.com/user-attachments/assets/14613cd7-205a-41c3-ad1a-059a04599cc9)




3. Create the destination bucket using the same steps and name it with a unique name.

![5](https://github.com/user-attachments/assets/5065b543-e6aa-497f-a75d-382fd04b8565)



4. As you can see above , I created two buckets one is Source bucket and another one is Destination bucket.

### Step 2 :
### Creating the SNS Notification :

1. Navigate to the SNS console.
2. Follow the Outlined Steps below.

![6](https://github.com/user-attachments/assets/20ccb48a-9bef-4470-a71d-a325263e80f3)


![7](https://github.com/user-attachments/assets/431e7c81-bd04-43aa-a543-c8d1e1253ba5)


![8](https://github.com/user-attachments/assets/b7bf6430-2d62-4d90-9c36-ba7cd883c700)


![9](https://github.com/user-attachments/assets/eee7ea9a-17fa-48aa-87e9-5722fd8f573e)



3. Scroll down and Click "Create subscription" <br>
4. After this , you will receive some mail for Subscription Confirmation and you have to confirm that.<br>
5. You can use any other protocols also like SQS, HTTP, SMS etc .,<br>

![10](https://github.com/user-attachments/assets/2d62115b-61b5-4a45-8d61-17d4ad28848b)


![11](https://github.com/user-attachments/assets/7e193a5a-14a7-469e-8ba2-633704c774ca)



### Step 3 :
### Creating the Lambda :

1. Navigate to the Lambda Console.
2. Follow the Outlined steps below.

![12](https://github.com/user-attachments/assets/d6d6b93b-9ab3-478c-80ac-70299e9205bd)


![13](https://github.com/user-attachments/assets/c8e423dc-a1ca-4b12-b0c0-073b56a66a62)



3. Now replace the default code with the image-resizing-s3.py and deploy the changes , Don't test the code now we have to do some more actions before testing.
4. After that , We have to give some permission for our Lambda Function to do our process (resizing) , For that navigate to the IAM Console and follow the below steps.

![14](https://github.com/user-attachments/assets/d7f9e9ec-43c4-440b-ad9f-d740d82652ad)


![15](https://github.com/user-attachments/assets/37976fca-0bb0-4146-919d-137e2c2b1e25)


![16](https://github.com/user-attachments/assets/e5acd721-2077-42bf-9dee-479381538bb4)



![17](https://github.com/user-attachments/assets/0d8dad0f-5ac1-4f2a-a385-6ba08a96f0a7)



![18](https://github.com/user-attachments/assets/6a066878-7bd3-431e-a5d0-f472f2616e0f)


![19](https://github.com/user-attachments/assets/596cf105-d05e-40e7-8a34-4edd4cb0594a)


![20](https://github.com/user-attachments/assets/198c47c6-7795-4d15-ad6e-9600ce9816a0)


![21](https://github.com/user-attachments/assets/ef3bf12f-f280-4325-9cba-39fa09deed49)



5. Now navigate to the Lambda Console and follow the steps below.

![22](https://github.com/user-attachments/assets/f06a5d0c-39b9-497e-82eb-38f51039a0d4)


![23](https://github.com/user-attachments/assets/cd0131b5-daa5-48d9-b2d7-677205ab9bf9)


![24](https://github.com/user-attachments/assets/478bfe2b-01a2-45c7-9e9e-9c82d3cb3e19)



6. Now we have to trigger the function.

![25](https://github.com/user-attachments/assets/8eb005a8-e703-4640-81da-ef59c28ab148)


![26](https://github.com/user-attachments/assets/776b1b0f-5b10-4aaf-8c00-e5232ba9cc94)




7. Now we have to go to code section , and scroll down to  layers.<br>
8. We have to add layer .<br>
9. May be you can think , why ?<br>
10. It's because for resize the image we upload in our source S3 bucket , We need a python library called pillow in our code to resize the image . We can manually add Pillow library also, But it's very time consuming and you have to do lot more , Instead of manually adding pillow library we are going to use layers for Some easy action.<br>
11. Follow the outlined Steps below.

![27](https://github.com/user-attachments/assets/7f35e633-2263-4d38-9739-33930e2f89de)


![28](https://github.com/user-attachments/assets/ffad4218-a1c1-4ed4-b70d-2796e3e2b7e1)



12.You can copy the arn from below.

```
arn:aws:lambda:ap-south-1:770693421928:layer:Klayers-p39-pillow:1
```

13. After done all the actions above , now we can test our code.

![29](https://github.com/user-attachments/assets/c24fc5d1-ae6b-4a76-8b80-eae96dea314a)

![30](https://github.com/user-attachments/assets/3dee106e-f533-4139-bd3a-b9fe441168cd)




14. It will show some results like below , It runs successfully but return some error because we still not upload the images in S3 yet.

![31](https://github.com/user-attachments/assets/fd38ce7f-1e0a-4f1c-91c8-dea26e782422)




### Step 4 :
### Results :

1. Navigate to the S3 Console.
2. Upload Some images in  Source Bucket.

![32](https://github.com/user-attachments/assets/9abcfab4-64dd-4f39-82c8-5edc3bd5bc45)


![33](https://github.com/user-attachments/assets/7cf987c9-5470-4d1b-b3bd-f83941fe37fd)


![34](https://github.com/user-attachments/assets/5c81ffaf-e926-4cb1-baf8-87a1ae0c8ebf)

![35](https://github.com/user-attachments/assets/ee479fed-c943-4140-b0a8-868f8c2feb8f)


![36](https://github.com/user-attachments/assets/6ddd66c4-9e91-4d93-9463-7b0e57c1d043)


![37](https://github.com/user-attachments/assets/8d1d684a-553f-4dd4-ae12-eb074c5a396b)



### It Successfully resized the Image and sends me the Notification.
