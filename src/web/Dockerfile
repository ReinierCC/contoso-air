FROM node:22
ENV PORT 3000
EXPOSE 3000

RUN mkdir -p /usr/src/web
WORKDIR /usr/src/web
COPY package.json .
RUN npm install
COPY . .

CMD ["npm", "start"]
