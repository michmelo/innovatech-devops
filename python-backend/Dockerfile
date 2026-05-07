# ── ETAPA 1: Instalar dependencias ────────────────────────────
FROM python:3.11-alpine AS builder

WORKDIR /app

# Copiamos solo el requirements.txt primero (truco de caché)
COPY requirements.txt .

# Instalamos las dependencias en una carpeta separada
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# ── ETAPA 2: Imagen final liviana ─────────────────────────────
FROM python:3.11-alpine

WORKDIR /app

# Usuario sin privilegios root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copiamos las dependencias instaladas desde la etapa anterior
COPY --from=builder /install /usr/local

# Copiamos el código fuente
COPY app.py .

USER appuser

EXPOSE 5000

CMD ["python", "app.py"]