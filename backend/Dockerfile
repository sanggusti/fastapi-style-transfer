FROM python:3.8-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV ENVIRONMENT prod
ENV TESTING 0

RUN apt-get update
RUN apt-get install \
    'ffmpeg'\
    'libsm6'\
    'libxext6' -y

COPY requirements.txt .
RUN pip install -r requirements.txt
RUN pip install "uvicorn[standard]==0.13.4"

COPY . .

# run gunicorn
CMD gunicorn --bind 0.0.0.0:$PORT main:app -k uvicorn.workers.UvicornWorker