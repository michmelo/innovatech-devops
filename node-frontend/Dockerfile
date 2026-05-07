# ── ETAPA 1: Instalar dependencias ────────────────────────────
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY server.js .
COPY public ./public

# ── ETAPA 2: Imagen final ─────────────────────────────────────
FROM node:20-alpine

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/server.js ./server.js
COPY --from=builder /app/public ./public

USER appuser

EXPOSE 3000

CMD ["node", "server.js"]