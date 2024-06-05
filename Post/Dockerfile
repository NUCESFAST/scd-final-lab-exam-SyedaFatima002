FROM node:14

WORKDIR /Post
COPY package*.json ./
RUN npm install
COPY . .
#exposing backend module 4 on : 2000 + 1213 = 3213 + 3
EXPOSE 3216                
CMD ["node", "index.js"]
