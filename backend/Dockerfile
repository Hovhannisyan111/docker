FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps
COPY . . 
RUN npm run build

FROM node:18 AS runtime
WORKDIR /app
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules node_modules/
COPY --from=builder /app/dist dist/
COPY --from=builder /app/nest-cli.json nest-cli.json
COPY --from=builder /app/tsconfig.build.json tsconfig.build.json
COPY --from=builder /app/.env .env
COPY --from=builder /app/tsconfig.json tsconfig.json
#COPY --from=builder /app /app
#CMD ["npm", "run", "start"]
CMD ["node", "dist/main"]
