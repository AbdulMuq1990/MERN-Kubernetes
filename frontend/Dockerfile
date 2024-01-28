FROM node:18-alpine AS build
LABEL maintainer="muqtadeer<muqtadeer@gmail.com>"
WORKDIR /app
COPY package*.json ./
#RUN npm install -g npm@10.3.0(This is not required since image has latest npm)
RUN npm install --silent
RUN npx update-browserslist-db@latest
COPY . .
RUN npm run build

FROM nginx:alpine
LABEL maintainer="muqtadeer<muqtadeer@gmail.com>"
RUN rm -rf /usr/share/nginx/html/*
COPY default.conf /etc/nginx/conf.d
COPY --from=build /app/build/ /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
