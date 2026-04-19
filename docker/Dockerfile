FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

# 2. 核心补丁：
WORKDIR /app
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    # 强制将所有代码中的 Cryptodome 替换为 Crypto
    find . -type f -name "*.py" -print0 | xargs -0 sed -i 's/Cryptodome/Crypto/g' && \
    # 安装 pycryptodome 并安装当前目录下的 musicdl
    pip install --no-cache-dir pycryptodome . && \
    # 物理补丁：在 python 库目录强制做一个软链接，双保险
    python -c "import site; import os; sp = site.getsitepackages()[0]; os.symlink(os.path.join(sp, 'Crypto'), os.path.join(sp, 'Cryptodome')) if not os.path.exists(os.path.join(sp, 'Cryptodome')) else None"

RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
