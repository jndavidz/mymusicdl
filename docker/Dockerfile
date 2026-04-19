FROM python:3.10-slim

# 强制禁用缓存的关键环境变量
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
# 增加一个版本标识，每次构建只要改一下这个日期，就能强制刷新
ENV REFRESH_DATE=2026-04-19

# 1. 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg git && \
    rm -rf /var/lib/apt/lists/*

# 2. 暴力手术：拉取、替换、安装
WORKDIR /app
RUN git clone https://github.com/CharlesPikachu/musicdl.git . && \
    # 这一步是核心：确保递归搜索所有目录，强行替换
    find . -type f -name "*.py" | xargs sed -i 's/Cryptodome/Crypto/g' && \
    # 先装加密库，再装本身
    pip install --no-cache-dir pycryptodome && \
    pip install --no-cache-dir .

# 3. 运行前最后一次路径校验
RUN python -c "import site; import os; sp = site.getsitepackages()[0]; os.symlink(os.path.join(sp, 'Crypto'), os.path.join(sp, 'Cryptodome')) if not os.path.exists(os.path.join(sp, 'Cryptodome')) else None"

RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
