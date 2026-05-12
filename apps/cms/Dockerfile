FROM node:20-alpine AS dev
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "run", "dev"]

FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS prod
WORKDIR /app
ENV NODE_ENV=production
RUN addgroup -S app && adduser -S app -G app
COPY --from=builder --chown=app:app /app/build ./build
COPY --from=builder --chown=app:app /app/package*.json ./
COPY --from=builder --chown=app:app /app/config ./config
COPY --from=builder --chown=app:app /app/src ./src
COPY --from=builder --chown=app:app /app/public ./public
RUN npm ci --omit=dev
USER app
EXPOSE 1337
CMD ["npm", "start"]
