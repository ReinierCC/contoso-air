FROM node:22
ENV PORT 3000
EXPOSE 3000

COPY package.json .
RUN npm install
COPY . .

CMD ["npm", "start"]
