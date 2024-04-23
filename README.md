# 21BCP282_DockerFiles_for_ia
Repository containing docker files for IA 

	
FROM node:16

Next, let’s quickly create a directory to house our image’s application code. This acts as the working directory for your application:


WORKDIR /app

The following COPY instruction copies the package.json and src file from the host machine to the container image. The COPY command takes two parameters. The first tells Docker what file we’d like to copy into the image. The second tells Docker where we want those files to be copied. We’ll copy everything into our working directory called /app:
2
COPY ./package.json ./package.json
COPY ./public ./public

Next, we need to add our source code into the image. We’ll use the COPY command just like we previously did with our package.json file:
COPY ./src ./src

Then, use yarn install to install the package:
RUN yarn install

The EXPOSE instruction tells Docker which port the container listens on at runtime. You can specify whether the port listens on TCP or UDP. The default is TCP if the protocol isn’t specified:
EXPOSE 3000

Finally, we’ll start a project by using the yarn start command:
CMD ["yarn","start"]
