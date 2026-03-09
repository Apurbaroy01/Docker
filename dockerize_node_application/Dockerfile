FROM node:22

WORKDIR /app

RUN npm install -g nodemon

COPY package.json .

RUN npm install

COPY . .

EXPOSE 5001

CMD [ "npm", "run", "dev" ]
