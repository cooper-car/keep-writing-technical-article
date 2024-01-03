# Context
- 認真的前端大大想升級 node16.13 到 node18
- 剛好可接觸一下docker
<br><br>

# Problem
- 在升級的過程中，可能會遇到套件相依性問題
- 可能會需要調整原先code的寫法
<br><br>

# Step by Step 實作

### 1. 準備好代碼
```
1. 本機創建一個新資料夾 ToNode18 (可隨意命名)
2. ToNode18 資料夾中 clone backendweb 的 code下來
3. clone 這個 github 專案並將 dockerfile 複製到 backendweb 裡面
```
### Optional
```
// 下載 docker desktop
https://www.docker.com/products/docker-desktop/
```


### 2. 進入鯨魚王的世界

### 打開 IDE (這邊用vscode)
```
開啟 backendweb 的 code，並打開 terminal
```

### Build image
```go
// Tag an image (-t, --tag)
// The repository name will be node-app and the tag will be 18
docker build -t node-app:18 .
```

### Create container
```
docker run -it -d -v $(pwd):/app -p 3000:3000 --name backend-node18  node-app:18
```
![Alt text](<CleanShot 2024-01-03 at 14.30.51@2x.jpg>)
### Access to the container
```
docker exec -it {CONTAINER_ID} bash
```

### 3. 處理相依性套件升級問題
```
1. export NODE_OPTIONS=--openssl-legacy-provider
2. npm install -g npm
3. npm install typescript@4.4.3
4. npm install (optional)
5. npm run serve
```


