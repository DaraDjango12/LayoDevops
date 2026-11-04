FROM node:22-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --omit=dev
COPY --from=builder /app ./

EXPOSE 3001
HEALTHCHECK --interval=10s --timeout=5s --start-period=5s --retries=3 \
  CMD node -e "require('http').get('http://localhost:3001/api/tags', (r) => r.statusCode === 200 ? process.exit(0) : process.exit(1))"

CMD ["npm", "start"]

