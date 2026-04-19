FROM python:3.10-slim

# 解决中文显示乱码（如果你搜索中文歌名，这很重要）
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

# 核心依赖：一次性安装 musicdl 和相关的加密库
# 在云端构建不需要 -i 镜像源，直接拉官方的最稳
RUN pip install --no-cache-dir pycryptodome musicdl

# 创建目录并设置权限
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

# 启动
CMD ["musicdl"]
