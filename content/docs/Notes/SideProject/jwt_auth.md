# JWT Auth

> https://github.com/elvin9281/jwt_auth

## Flow
![](https://i.imgur.com/QELG0Bn.png)

## 目的：用 docker compose 將 Apifox 測試後端的流程串起來

### Makfile
```
Usage: make [target]
Targets:
  up            - All Services up
  down          - All Services down
  clean_all     - Clean all images
  ls            - Running services up by docker-compose
  into_db       - Go into postgres container
  build_apifox  - Build apifox container image
```

### docker-compose 的 Service Discovery
- 注意：都在 `app-net` 的情況下，`apifox` Container 打到 `backend` Container 的 URL 會是 `http://backend.app-net:8080`
- 注意： Apifox 建立測試時，環境要另外建立
![](https://i.imgur.com/klLAE65.png)

### Backend
- 來源：[Node.js JWT Authentication with PostgreSQL example](https://www.bezkoder.com/node-js-jwt-authentication-postgresql/)

### Apifox

- 注意：後置操作，要將 `access_token` 存起來
```
pm.test("Get access token", ()=>{
    const response = pm.response.json();
    const token = response["accessToken"];
    pm.environment.set("access_token", token);
});
```
- 注意：用`apifox-cli`產出報告會在`apifox-reports`，所以執行 container 的時候要 `mount /apifox-reports`
```
# test_jwt_auth.sh
docker run -it --rm --network app-net \
	-v ./apifox-reports:/apifox-reports \
	-v ./data/jwt_auth.apifox-cli.json:/data/jwt_auth.apifox-cli.json \
	apifox:latest bash -c "apifox run /data/jwt_auth.apifox-cli.json -r cli,html,json"
```

## TODO
- Apifox 產出 Swagger 文件的流程