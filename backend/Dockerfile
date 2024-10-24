FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps
COPY . . 
RUN npm run build

FROM node:alpine AS runtime
WORKDIR /app
COPY --from=builder /app/node_modules node_modules/
COPY --from=builder /app/dist dist/
COPY --from=builder /app/.env .

CMD ["node", "dist/main"]
