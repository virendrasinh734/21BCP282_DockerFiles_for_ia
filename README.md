# 21BCP282_DockerFiles_for_ia
Repository containing docker files for IA 

	
## Dockerfile Explanation (Backend)

- `FROM node:16`: Specifies the base image as Node.js version 16.

Next, let’s quickly create a directory to house our image’s application code. This acts as the working directory for your application:

- `WORKDIR /app`

The following `COPY` instruction copies the `package.json` and `src` file from the host machine to the container image. The `COPY` command takes two parameters. The first tells Docker what file we’d like to copy into the image. The second tells Docker where we want those files to be copied. We’ll copy everything into our working directory called `/app`:

- `COPY ./package.json ./package.json`
- `COPY ./public ./public`

Next, we need to add our source code into the image. We’ll use the `COPY` command just like we previously did with our `package.json` file:

- `COPY ./src ./src`

Then, use `yarn install` to install the package:

- `RUN yarn install`

The `EXPOSE` instruction tells Docker which port the container listens on at runtime. You can specify whether the port listens on TCP or UDP. The default is TCP if the protocol isn’t specified:

- `EXPOSE 3000`

Finally, we’ll start a project by using the `yarn start` command:

- `CMD ["yarn","start"]`




## React Dockerfile Explanation

- `FROM node:16`: Specifies the base image as Node.js version 16.
- `WORKDIR /app`: Sets the working directory inside the container to `/app`.
- `COPY ./package.json ./package.json`: Copies `package.json` from the host to `/app` in the container.
- `COPY ./public ./public`: Copies the `public` directory from the host to `/app/public` in the container.
- `COPY ./src ./src`: Copies the `src` directory from the host to `/app/src` in the container.
- `RUN yarn install`: Installs dependencies listed in `package.json`.
- `EXPOSE 3000`: Exposes port 3000 on the container.
- `CMD ["yarn","start"]`: Sets the default command to start the React UI application using `yarn start`.




## Docker Compose Explanation


slackfrontend: 
  - Service for the Slack frontend.
  - build: Specifies build instructions.
    - context: .: Build context set to the current directory.
    - dockerfile: Dockerfile.reactUI: Specifies Dockerfile for building the image.
  - ports: Maps container port 3000 to host port 3000.
  - depends_on: Service depends on the db service.

nodebackend: 
  - Service for the Node backend.
  - build: Specifies build instructions.
    - context: ./server: Build context set to the server directory.
    - dockerfile: Dockerfile.node: Specifies Dockerfile for building the image.
  - ports: Maps container port 9000 to host port 9000.
  - depends_on: Service depends on the db service.

db: 
  - Service for MongoDB.
  - volumes: Mounts a volume named slack_db to persist data.
  - image: mongo:latest: Specifies the Docker image to use (latest version of MongoDB).
  - ports: Maps container port 27017 to host port 27017.
  - volumes: Defines named volume slack_db for persisting MongoDB data.

This Docker Compose configuration sets up three services: slackfrontend, nodebackend, and db, where slackfrontend and nodebackend depend on db (MongoDB). Each service has specific build instructions, port mappings, and dependencies. Additionally, a named volume slack_db is defined for persisting MongoDB data.

