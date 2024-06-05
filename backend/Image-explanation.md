## Dockerfile for Backend Service

We create an image for the backend service which would be used to run containers and test out its workability

The backend image has gone through multiple iterations as shown in the dockerhub commits

 ### Image Iterations over time

![image](https://github.com/Jmaisiba/yolo/assets/35705417/c9450e91-53a9-465a-ad45-9b08799093b5)

The different iterations have had massive improvements to the size of the image as illustrated below

 ### First Iteration

![image](https://github.com/Jmaisiba/yolo/assets/35705417/d60287a9-97fb-4a40-9c16-461b2b5789fe)

 ### Latest Iteration

![image](https://github.com/Jmaisiba/yolo/assets/35705417/a8acd4c8-92ab-4fbb-9833-5a811fea0f63)



### Explanation:
#### Reducing Image size
The changes to the image are due to choice of and selection of different components to get the optimal image while building the image from the Dockerfile

 #### Base image 
 - The alpine version of base images provided by dockerhub are more light-weight compared to other versions of the images
 - Changing from `node:latest` to the alpine version `node22.1-alpine13.8` greatly reduced the size of the image
 - Later moving to `node:13.12-alpine` had no bearing on size but compatibility and stability of the image

 ### dockerignore File
 - Using the dockerignore file reduces the size of the image by excludoing unecessary files in the image
 - These unecessary file add on to the size of the image.
 - By adding the node-modules folder that is generated after installing dependancies size of the image was greatly reduced
