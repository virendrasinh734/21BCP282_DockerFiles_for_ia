# 21BCP282_DockerFiles_for_ia
Repository containing docker files for IA 

	
## Dockerfile Explanation

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
