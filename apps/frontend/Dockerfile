# syntax=docker/dockerfile:1

# 1) Install dependencies with Bun
FROM oven/bun:1 AS deps
WORKDIR /app
COPY package.json ./
RUN bun install

# 2) Build the Next.js app
FROM oven/bun:1 AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . ./
RUN bun run build

# 3) Production runtime with smaller Node image
FROM node:20-slim AS production
WORKDIR /app
ENV NODE_ENV=production
EXPOSE 3000
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public
CMD ["node", "server.js"]