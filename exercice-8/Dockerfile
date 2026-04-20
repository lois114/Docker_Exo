FROM python:3.12-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --prefix=/install --no-cache-dir -r requirements.txt

FROM python:3.12-slim
WORKDIR /app
COPY --from=builder /install /install
COPY app.py .
ENV PYTHONPATH=/install/lib/python3.12/site-packages
EXPOSE 5000
RUN groupadd -r appuser && useradd -r -g appuser appuser
RUN chown -R appuser:appuser /app
USER appuser
CMD ["flask", "run", "--host=0.0.0.0"]