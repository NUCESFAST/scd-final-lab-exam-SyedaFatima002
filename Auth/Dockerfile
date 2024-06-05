FROM node:14

WORKDIR /Auth
COPY package*.json ./
RUN npm install
COPY . .
#exposing backend module 1 on : 2000 + 1213 = 3213
EXPOSE 3213                
CMD ["node", "index.js"]
