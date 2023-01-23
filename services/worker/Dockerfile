FROM python:3.9-slim-bullseye
WORKDIR /app
COPY ./services/worker/requirements.txt .
RUN pip install -r requirements.txt

COPY ./common/config.json /app/config.json
ENV CONFIG-JSON-PATH=/app/config.json

COPY ./common/utils.py .

COPY ./services/worker/app.py /app/app.py
CMD ["python3", "/app/app.py"]