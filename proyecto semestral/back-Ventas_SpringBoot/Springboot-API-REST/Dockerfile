# Etapa 1: Construcción (Build)
FROM maven:3.9-eclipse-temurin-17-alpine AS builder
WORKDIR /app

# Copiamos el pom.xml y descargamos dependencias offline para aprovechar la caché de Docker
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiamos el código fuente y compilamos el proyecto
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución (Run)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Crear un usuario y grupo sin privilegios (no-root)
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Cambiamos al usuario creado para ejecutar la aplicación de forma segura
USER appuser

# Copiamos el archivo .jar generado en la etapa de construcción
COPY --from=builder /app/target/*.jar app.jar

# Exponemos el puerto interno del contenedor (asegúrate de que coincida con el de tu application.properties)
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]