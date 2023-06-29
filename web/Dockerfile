FROM node:18 AS base
CMD [ "bash" ]

# Build
FROM base AS test-and-build
# 今見ているものをコンテナーのworkspaceにコピーする
COPY . /workspace
WORKDIR /workspace
#　変数に任意の値を入れるdockerファイルの中だけで有効
ARG REACT_APP_API_SERVER
# npm install
RUN npm ci && npm run test && npm run build
# Hosting in ninx
# build配下のものをnginxにコピー
FROM nginx:latest AS production
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf
