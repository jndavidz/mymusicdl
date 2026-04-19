FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 安装系统依赖和 git
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

# 2. 彻底解决 Cryptodome 报错：
# 直接克隆源码 -> 强行把代码里的 Cryptodome 改写成 Crypto -> 然后安装
WORKDIR /app
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    grep -rl "Cryptodome" . | xargs sed -i 's/Cryptodome/Crypto/g' && \
    pip install --no-cache-dir pycryptodome .

# 3. 创建目录
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
