FROM node:12-alpine
COPY package.json /usr/src/app/package.json
WORKDIR /usr/src/app
RUN npm install
COPY . ./
EXPOSE 3000
EXPOSE 3002
RUN npx prisma generate
CMD ["npx", "serverless", "offline"]