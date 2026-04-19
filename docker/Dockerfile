FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# 1. 系统依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*

# 2. 暴力安装策略：
# - 卸载可能干扰的所有加密库
# - 显式安装 pycryptodomex (这个库的导入名就是 Cryptodome)
# - 手动通过 Python 将 pycryptodomex “伪装”成 Cryptodome 路径
RUN pip install --no-cache-dir pycryptodomex musicdl && \
    python -c "import site; import os; sp = site.getsitepackages()[0]; os.rename(os.path.join(sp, 'cryptodomex'), os.path.join(sp, 'Cryptodome')) if os.path.exists(os.path.join(sp, 'cryptodomex')) else None"

RUN mkdir -p /downloads /root/.musicdl
WORKDIR /downloads

CMD ["musicdl"]
