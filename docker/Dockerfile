FROM python:3.10-slim

# 设置环境变量
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

# 核心修正：安装 pycryptodome 和 musicdl
# 云端构建不需要国内镜像源，直接从官方拉取极快
RUN pip install --no-cache-dir pycryptodome musicdl

# 创建目录
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
