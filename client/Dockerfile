FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# Copy result of builder step and put it where nginx serves from
# Note: only copying files necessary for running in prod (ie. no tests, etc.)
COPY --from=builder /app/build /usr/share/nginx/html
