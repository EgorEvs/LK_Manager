# backend/Dockerfile
# 1. База — официальный Node.js
FROM node:18-alpine AS builder
WORKDIR /app

# 2. Копируем package.json и устанавливаем зависимости
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# 3. Копируем весь код и собираем
COPY . .
RUN yarn build

# 4. Финальный образ
FROM node:18-alpine
WORKDIR /app
# Копируем собранные артефакты и prod-зависимости
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

EXPOSE 4000
CMD ["node", "dist/main.js"]
