FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /app

COPY ./ ./

RUN npm ci
RUN npm run build

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

EXPOSE 5173

WORKDIR /app

RUN mkdir -p /app/node_modules

COPY package.json ./
COPY package-lock.json ./
COPY vite.config.ts ./
COPY --from=BUILDER /app/dist ./
COPY --from=BUILDER /app/node_modules/ ./node_modules

CMD [ "npm", "run", "dev" ]