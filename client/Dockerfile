FROM node:14
r
WORKDIR /client
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
RUN npm install
#exposing port my roll number - 1213
EXPOSE 1213
CMD ["npm", "build"]
