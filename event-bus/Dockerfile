FROM node:14

WORKDIR /event-bus
COPY package*.json ./
RUN npm install
COPY . .
#exposing backend module 3 on : 2000 + 1213 = 3213 + 2
EXPOSE 3215                
CMD ["node", "index.js"]
