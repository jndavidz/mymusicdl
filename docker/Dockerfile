FROM python:3.10-slim
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
RUN apt-get update && apt-get install -y --no-install-recommends ffmpeg && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir musicdl -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads
CMD ["musicdl"]
