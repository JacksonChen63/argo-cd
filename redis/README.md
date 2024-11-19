1. 到 gosu repo, 第一層有一個 version.go , 裡面有版本, 可以直接修改成對應 go version


2. 執行下面的 command 就會編譯 gosu 

```
go build -o gosu
```


3. 將 gosu cp 到 argocd repo 的 argo-cd/redis

```
cp gosu ../argo-cd/redis
```

4. 重新 build docker image  
```
docker build -t argo-cd-argocd-redis .
```


5. 登入gcp
```
gcloud auth login
```

6. 設定projectID
```
gcloud config set project project-gcp-idol-k8s
```

7. 登入 docker 
```
gcloud auth configure-docker asia-east1-docker.pkg.dev
```

8. docker tag image
```
docker tag argo-cd-argocd-redis:latest asia-east1-docker.pkg.dev/project-gcp-idol-k8s/idol-global-image/argo-cd-argocd-redis:v1.23.0
```

9. 推到 gcp artifact registry
```
docker push asia-east1-docker.pkg.dev/project-gcp-idol-k8s/idol-global-image/argo-cd-argocd-redis:v1.23.0
```
