# Etapa de build
FROM node:22-bookworm-slim AS build

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci --no-audit --no-fund

COPY . .

ARG VITE_API_URL=http://localhost:5200
ENV VITE_API_URL=${VITE_API_URL}

RUN npm run build

# Etapa de execução
FROM nginx:alpine AS runtime

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]