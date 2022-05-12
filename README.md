# react 開發建置 docker 環境

### 專案情境
> react 專案已開始開發，後續導入 docker

### 資料夾環境:
+ 專案外新增      docker-compose.yaml
+ 專案資料夾內新增 Dockerfile
```
│  docker-compose.yaml
│  
└─practice-project
    │  Dockerfile
    │  package.json
    │  
    ├─.idea
    ├─public
    └─src
```

### yaml 檔

```
version: "3.9"
services:
  react_practice:
    image: dev/react_practice
    container_name: frontend
    build:
      context: practice-project
    restart: always
    environment:
      IS_DEV: "true"
    ports:
      - "3000:3000"
```

### Dockerfile
+ 初次 build : 若專案以 yarn 執行
```
FROM node:14.18-alpine3.15
WORKDIR .
RUN npm install yarn
COPY practice-project .
RUN yarn
RUN yarn run build
CMD yarn start
```
+ 後續執行: 可註解掉不需重複做的步驟

### 指令
+ 建立 : 指定使用的 yaml 檔建立 container 與 image
```
docker compose -f docker-compose.yaml up -d
```
+ 更新 : 先停下執行中的 container 再重新 build
```
docker compose -f docker-compose.yaml down
docker compose -f docker-compose.yaml up -d --build
```
+ 進入 : 可實際查看/異動內部結構
```
docker compose -f docker-compose.yaml exec react_practice /bin/sh
```

### 遇到問題
+ npm 安裝 套件失敗
    + 錯誤訊息: ETIMEDOUT
    + 解決方法：建立 container 時，yaml 檔安裝套件前新增
    ```
    RUN npm config set registry https://registry.npmjs.org/
    RUN npm config set strict-ssl false
    ```
+ yarn 安裝套件失敗
    + 錯誤訊息: ETIMEDOUT
    + 解決方法：在 yaml 執行 RUN yarn 前新增
    ```
    RUN yarn config set registry https://registry.yarnpkg.com
    RUN yarn config set strict-ssl false
    ```