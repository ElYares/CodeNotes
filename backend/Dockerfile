# Imagen base
FROM node:20-alpine AS builder

WORKDIR /app

# Instalar dependencias
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Copiar código
COPY . .

# Compilar NestJS
RUN yarn build

# Imagen final
FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
COPY package.json yarn.lock ./

EXPOSE 3000

CMD ["node", "dist/main.js"]

