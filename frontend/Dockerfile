# ============ 1 Стадия: сборка ============
FROM node:20 AS build

# Создать рабочую директорию
WORKDIR /app

# 1) Скопировать package.json и package-lock.json
COPY package*.json ./

# 2) Выполнить npm ci
RUN npm install

# 3) Скопировать оставшийся код
COPY . .

# 4) Выполнить npm run build
RUN npm run build

# ============ 2 Стадия: рантайм ============
FROM nginx:alpine

# 1) Удалить содержимое дефолтной директории nginx
RUN rm -rf /usr/share/nginx/html

# 2) Скопировать результат сборки из первой стадии
COPY --from=build /app/dist /usr/share/nginx/html

# 3) Скопировать конфиг nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 4) Запустить nginx
CMD ["nginx", "-g", "daemon off;"]