## Dockerfile for Client Service

We create an image for the client application which would be used to run containers and test out its workability

The client images have gone through multiple iterations as shown in the dockerhub commits

### Image Iterations over time
![image](https://github.com/Jmaisiba/yolo/assets/35705417/f6e99951-6339-4e71-bdb3-3c5517f7b1cd)


## Image Size Comparison

#### First Iteration
![image](https://github.com/Jmaisiba/yolo/assets/35705417/df795e89-6526-409a-a304-3f0f5e70d670)

#### Latest Iteration
![image](https://github.com/Jmaisiba/yolo/assets/35705417/abbc4cc2-94fe-4c62-88c0-1164db8eac47)



## Explanation:
Here we go through the features that have made the latest image size be optimal in size and features

## Key Features of Dockerfile

  ### Optimization

- The build is optimized by removing dev dependenxies and leaving only the production dependencies using `npm prune --production` after dependancy installation
- By running the `npm run build` command we are building the client application that is more optimized
- Using the dockerignore file to exclude unwanted or unnecessary files from the image  

### Multi-stage Build
Utilizes a two stage build pattern to separate the build environment from the final production image, reducing the size of the final image.

  #### Stage 1: Builder

- Specifies the base image to use `node:22.1-alpine3.18` and it is assigned the name `builder`. This image is used for building the client application.
- Copies and installation of dependencies based on the copied packages folders which ensures that all required Node modules are installed within the container.
- The client application is build using the specified build script from the command `npm build`, this compiles and bundles the source code into static assets for production deployment.
- `npm prune --production` is run to remove development dependencies from the `node_modules` directory to reduce the image size

  #### Stage 2: Final Image

- We create a server to host our client image build, the server uses the base image `nginx:alpine` a lightweight nginx web server image based on alpine
- It is suitable for serving static content from the `/usr/share/nginx/html` where Nginx serves static files
- `--from=builder /client/build .` this copies the built client application from the `builder` stage(stage 1) to the current directory in the final image. 
- This step ensures that the built static assets are available for serving by Nginx.
- It is exposed at port `80`(default nginx port) to allow connections to the Nginx server.
- The `nginx -g "daemon off;"` command starts the Nginx server and keeps it running in the foreground, allowing Docker to manage the container's lifecycle.

  

