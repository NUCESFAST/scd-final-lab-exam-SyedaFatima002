FROM node:14

WORKDIR /Classrooms
COPY package*.json ./
RUN npm install
COPY . .
#exposing backend module 2 on : 2000 + 1213 = 3213 + 1
EXPOSE 3214                
CMD ["node", "index.js"]
