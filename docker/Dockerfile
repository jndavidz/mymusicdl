FROM python:3.10-slim
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
RUN apt-get update && apt-get install -y --no-install-recommends ffmpeg && rm -rf /var/lib/apt/lists/*
# 显式安装依赖，解决 Cryptodome 报错
RUN pip install --no-cache-dir pycryptodome musicdl
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads
CMD ["musicdl"]
