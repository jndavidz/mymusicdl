FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 安装系统依赖和 git
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

# 2. 暴力手术：拉取源码 -> 批量替换代码里的错误引用 -> 离线安装
WORKDIR /app
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    # 这一步是核心：把所有代码文件里的 Cryptodome 替换为 Crypto
    grep -rl "Cryptodome" . | xargs sed -i 's/Cryptodome/Crypto/g' && \
    # 安装依赖包
    pip install --no-cache-dir pycryptodome .

# 3. 创建下载和配置目录
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

# 4. 再次检查链接（双保险）
RUN python -c "import site; import os; sp = site.getsitepackages()[0]; os.symlink(os.path.join(sp, 'Crypto'), os.path.join(sp, 'Cryptodome')) if not os.path.exists(os.path.join(sp, 'Cryptodome')) else None"

CMD ["musicdl"]
