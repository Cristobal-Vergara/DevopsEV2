# Etapa 1: Construcción (Build)
FROM node:18-alpine AS builder
WORKDIR /app

# Copiamos los archivos de configuración y dependencias
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y construimos la versión de producción
COPY . .
RUN npm run build

# Etapa 2: Servidor Web (Nginx No-Root)
# Utilizamos una imagen oficial de Nginx ya configurada para ejecutarse sin privilegios root
FROM nginxinc/nginx-unprivileged:alpine

# Copiamos los archivos estáticos generados por Vite (usualmente en la carpeta 'dist')
COPY --from=builder /app/dist /usr/share/nginx/html

# ¡IMPORTANTE! Copiamos nuestra configuración personalizada
COPY nginx.conf /etc/nginx/conf.d/default.conf

# La imagen unprivileged de Nginx usa el puerto 8080 por defecto, no el 80
EXPOSE 8080

# Comando de inicio de Nginx
CMD ["nginx", "-g", "daemon off;"]