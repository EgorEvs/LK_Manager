# frontend/Dockerfile
FROM node:18-alpine AS builder
WORKDIR /app

# Устанавливаем зависимости
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Сборка приложения
COPY . .
RUN yarn build

# Финальный образ для сервера
FROM nginx:stable-alpine
COPY --from=builder /app/.next /usr/share/nginx/html
COPY --from=builder /app/public /usr/share/nginx/html
# Берём дефолтный конфиг, который обслуживает статические файлы

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
