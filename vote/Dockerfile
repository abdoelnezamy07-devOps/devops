FROM python:3.9-slim as builder
WORKDIR /app
COPY requirements.txt .
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.9-slim
WORKDIR /app
COPY --from-builder /opt/venv /opt/venv
COPY . .
ENV PATH="/opt/venv/bin:$PATH"
ENV PYTHONDONTWRITEBITECODE 1
ENV PYTHONUNBUFFERED 1
EXPOSE 8080
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "app:app"]

