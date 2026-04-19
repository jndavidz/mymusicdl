FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app
# 强制拉取源码并批量替换掉代码里那个该死的 Cryptodome
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    grep -rl "Cryptodome" . | xargs sed -i 's/Cryptodome/Crypto/g' && \
    pip install --no-cache-dir pycryptodome .

RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
