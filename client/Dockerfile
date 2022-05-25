FROM node:16-alpine as builder

RUN mkdir -p /home/app
RUN chown node:node /home/app

USER node
WORKDIR '/home/app'
COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
