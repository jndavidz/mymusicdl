FROM python:3.10-slim

# 设置环境变量
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

# 核心修正：
# 1. 显式安装 pycryptodome
# 2. 建立软链接，确保 Cryptodome 和 Crypto 文件夹互通，彻底解决 ModuleNotFoundError
RUN pip install --no-cache-dir pycryptodome musicdl && \
    ln -s /usr/local/lib/python3.10/site-packages/Crypto /usr/local/lib/python3.10/site-packages/Cryptodome || true

# 创建目录
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
