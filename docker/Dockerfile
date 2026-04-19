FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

# 2. 暴力手术补丁
WORKDIR /app
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    # 强制递归替换所有子目录下的 Cryptodome 为 Crypto
    find . -type f -name "*.py" -exec sed -i 's/Cryptodome/Crypto/g' {} + && \
    # 先安装依赖，再安装自己
    pip install --no-cache-dir pycryptodome && \
    pip install --no-cache-dir .

# 3. 建立物理软链接（防止 Python 导入机制死板）
RUN python -c "import site; import os; sp = site.getsitepackages()[0]; \
    src = os.path.join(sp, 'Crypto'); \
    dst = os.path.join(sp, 'Cryptodome'); \
    os.symlink(src, dst) if os.path.exists(src) and not os.path.exists(dst) else None"

RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
