FROM node:20-alpine

WORKDIR /app

# 先复制依赖清单，利用 Docker layer cache
COPY package.json package-lock.json ./

# 仅安装生产依赖
RUN npm ci --omit=dev

# 再复制源码
COPY public ./public
COPY src ./src

# 数据目录（用于 users.json / servers.json / invite-codes.json 等）
RUN mkdir -p /app/data

ENV NODE_ENV=production
ENV PORT=3070
ENV LISTEN_HOST=0.0.0.0

EXPOSE 3070

CMD ["node", "src/server.js"]
