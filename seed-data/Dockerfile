# Stage 1: Build & Data Generation
FROM python:3.9-slim AS builder
WORKDIR /app
COPY make-data.py generate-votes.sh ./
RUN python make-data.py

# Stage 2: Execution Image
FROM alpine:latest
WORKDIR /app

# تثبيت أداة apache2-utils اللي فيها أمر 'ab'
RUN apk add --no-cache apache2-utils

# نسخ الملفات المولدة والسكريبت من المرحلة الأولى
COPY --from=builder /app/posta /app/postb ./
COPY --from=builder /app/generate-votes.sh ./

# إعطاء صلاحية التنفيذ للسكريبت
RUN chmod +x generate-votes.sh

# تشغيل السكريبت عند بدء الـ Container
CMD ["sh", "./generate-votes.sh"]
