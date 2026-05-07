# ── ETAPA 1: Compilar el archivo .java ────────────────────────
# JDK completo para poder compilar con javac
FROM eclipse-temurin:17-jdk-alpine AS builder

WORKDIR /app

# Copiamos el único archivo Java
COPY App.java .

# Compilamos — genera un archivo app.class
RUN javac App.java

# ── ETAPA 2: Imagen final solo para ejecutar ──────────────────
# Solo JRE (mucho más liviano que JDK, no incluye compilador)
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Usuario sin privilegios root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copiamos el .class compilado desde la etapa anterior
COPY --from=builder /app/*.class .

USER appuser

EXPOSE 8080

# Ejecutamos la clase compilada
CMD ["java", "App"]