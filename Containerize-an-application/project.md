
## Building a docker application

## building a simple to-do application (todoapp)image with Docker.

## Prerequisite

- You have installed the latest version of [Docker Desktop](https://docs.docker.com/get-docker/)
- You have installed a [Git Client](https://git-scm.com/downloads)

- You have an IDE or a text editor to edit files. I will be using vi editor

## Get the app
- Before you can run the application, you need to get the application source code onto your machine.

- Clone the [getting-started-app](https://github.com/docker/getting-started-app/tree/main )repository using the following command:

`git clone https://github.com/docker/getting-started-app.git`


- View the contents of the cloned repository. You should see the following files and sub-directories.

![](../docker/images/content.PNG)

##  Build the app's image

- To build the image, you'll need to use a Dockerfile
- A Dockerfile is a text file with a series of commands in it. 
- In the getting-started-app directory, the same location as the package.json file, create a file named Dockerfile
- In the terminal, run the following commands.

- Make sure you're in the getting-started-app directory. Replace /path/to/getting-started-app with the path to your getting-started-app directory.

`cd /path/to/getting-started-app`

- Create an empty file named Dockerfile.

`touch Dockerfile`
- Using a text editor or code editor, add the following contents to the Dockerfile:

`# syntax=docker/dockerfile:1

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000`

## Build the image using the following commands:

- In the terminal, make sure you're in the getting-started-app directory. Replace /path/to/getting-started-app with the path to your getting-started-app directory.

`cd /path/to/getting-started-app`

![](../docker/images/direc.PNG)


### Build the image.
`docker build -t getting-started .`

![](../docker/images/build-image.PNG)





 - You’ve defined your Dockerfile’s build steps. Now
you’re going to build the Docker image from it by
typing the command . The output will
look similar to this:
![](../docker/images/docker-image.PNG)

## STEP3 Running a Docker container
- You’ve built and tagged your Docker image. Now you can run it as a container:

` docker run -i -t -p 8000:8000 --name example1 todoapp`

![](../docker/images/docker-tag.PNG)   

- The docker build command uses the Dockerfile to build a new image. You might have noticed that Docker downloaded a lot of "layers". This is because you instructed the builder that you wanted to start from the node:18-alpine image. But, since you didn't have that on your machine, Docker needed to download the image.

- After Docker downloaded the image, the instructions from the Dockerfile copied in your application and used yarn to install your application's dependencies. The CMD directive specifies the default command to run when starting a container from this image.

- Finally, the -t flag tags your image. Think of this as a human-readable name for the final image. Since you named the image getting-started, you can refer to that image when you run a container.

- The . at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.


### Starting an app container

- The . at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.

- Run your container using the docker run command and specify the name of the image you just created:

`docker run -dp 172.31.28.64:3000:3000 getting-started`

- The -d flag (short for --detach) runs the container in the background. The -p flag (short for --publish) creates a port mapping between the host and the container. The -p flag takes a string value in the format of HOST:CONTAINER, where HOST is the address on the host, and CONTAINER is the port on the container. The command publishes the container's port 3000 to 172.31.28.64:3000 (localhost:3000) on the host. Without the port mapping, you wouldn't be able to access the application from the host.
- N.B 172.31.28.64 is the private ip address

- After a few seconds, open your web browser to [http://localhost:3000](http://localhost:3000/). You should see your app.

![todolist](../docker/images/todolist.PNG)


- Add an item or two and see that it works as you expect. You can mark items as complete and remove them. Your frontend is successfully storing items in the backend.

![](../docker/images/edited.PNG)

- If you take a quick look at your containers, you should see at least one container running that's using the getting-started image and on port 3000. To see your containers, you can use the CLI or Docker Desktop's graphical interface

`sudo docker ps`
- Output similar to the following should appear.

![output](../docker/images/output.PNG)

