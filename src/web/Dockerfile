FROM node:22
ENV PORT 3000
EXPOSE 3000

RUN mkdir -p /usr/src/web
WORKDIR /usr/src/web
COPY . .
RUN ls -al /usr/src/web
RUN npm install


CMD ["npm", "start"]
