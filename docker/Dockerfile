FROM python:3.10-slim

# 设置环境变量
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 安装系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

# 2. 核心修正：
# 先卸载可能存在的冲突库，然后显式安装 pycryptodome
# 并在 site-packages 目录下强制创建两个名字的指向
RUN pip install --no-cache-dir pycryptodome musicdl && \
    python -c "import site; import os; sp = site.getsitepackages()[0]; os.symlink(os.path.join(sp, 'Crypto'), os.path.join(sp, 'Cryptodome')) if os.path.exists(os.path.join(sp, 'Crypto')) and not os.path.exists(os.path.join(sp, 'Cryptodome')) else None"

# 3. 创建目录
RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
