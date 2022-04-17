# Docker & Container Commands 
> 紀錄常用的指令

## Images

- 查看目前 Images(不包含「Intermediate Images」)

>  Docker 17.05+ 以後提供名為「多階段構建 (multi-stage builds)」的新功能，透過將原先流水線中的多個映像檔整合進同個 Dockerfile 內，而後續的映像檔可透過指令取得中間映像檔 (intermediate image) 所產生的檔案 (artifacts)，如此便能讓整個過程更為簡單，也確保流水線簡潔易懂及提高維護性
```tpl
docker images
// or
docker image ls
```

- 查看目前 Images(含「Intermediate Images」)
```tpl
docker images -a
// or
docker image ls -a
```

- 只列出所有 Images 的 ID(不含「Intermediate Images」)
```tpl
docker images -q
// or
docker image ls -q
```

- 只列出所有 Images 的 ID(含「Intermediate Images」)
```tpl
docker images -qa
// or
docker image ls -qa
```
- 建立一個名稱為 busybox 的 Image
  - `-i` : Interactive，Keep STDIN open even if not attached \n
  - `-t` : Allocate a pseudo-TTY
```tpl
docker create -it --name busybox busybox
```
- 強制刪 Docker Image (用 ID)
```tpl
docker rmi -f <Image_ID>
```
- 強制刪除所有 docker images(含「Intermediate Images」)
```tpl
docker rmi -f $(docker images -q) 
```
## Container

- 自動執行 docker pull(若 Local 無該 Image)，啟動並進入背景執行
> `-d` : Run container in background and print container ID
```tpl
# docker run -d <REPOSITORY>:<TAG>
docker run -d debian:jessie 
```
- 自動執行 docker pull(若 Local 無該 Image)，跑起來自動執行 bash 程式進入此 Container
```tpl
# docker run -it <REPOSITORY>:<TAG> sh
docker run -it debian:jessie sh
```


### [Stop All Containers](https://typeofnan.dev/how-to-stop-all-docker-containers/)
```tpl
docker kill $(docker ps -q)
```

### Remov All Containers
```tpl
docker rm $(docker ps -a -q)
```
### [List all Docker Container Names and their IPs](https://bytefreaks.net/applications/docker/how-to-list-all-docker-container-names-and-their-ips)
```tpl
docker ps -q | xargs -n 1 docker inspect --format '{{ .Name }} {{range .NetworkSettings.Networks}} {{.IPAddress}}{{end}}' | sed 's#^/##'
```


---

- Ref
  - https://tachingchen.com/tw/blog/docker-multi-stage-builds/
  - https://blog.longwin.com.tw/2017/01/docker-learn-initial-command-cheat-sheet-2017/
