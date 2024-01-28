FROM node:18-alpine
LABEL maintainer="muqtadeer<muqtadeer@gmail.com>"
WORKDIR /app
COPY package*.json .

#Below ENVs not required, Since we have created a .env file in backend folder & specified MONGO_CONNECTION_STRING, SESSION_SECRET, PORT

#ENV MONGO_INITDB_ROOT_USERNAME: muqtadeer
#ENV MONGO_INITDB_ROOT_PASSWORD: welcome
#ENV MONGO_INITDB_DATABASE: cool_notes_app
#ENV MONGO_CONNECTION_STRING=mongodb+srv://abdulmuq1990:test123@muqtadeer-cluster.rjqkyx0.mongodb.net/cool_notes_app?retryWrites=true&w=majority
#ENV SESSION_SECRET=hfg52jjf$654c
#ENV PORT=5000

RUN npm install
RUN npm install -g npm@10.3.0
COPY . .
RUN npm install -g typescript
RUN tsc
#RUN node dist/server.js	(pm2 is running service in backgroung, this is not required)
RUN npm install pm2 -g
#CMD ["pm2-runtime", "server.js"]
CMD ["pm2-runtime", "start", "dist/server.js", "--name", "server"]
