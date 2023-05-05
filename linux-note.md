### 查看ip與port使用狀態
```
sudo lsof -i -P -n
```
### 看port有沒有使用
```
nc -v 127.0.0.1 6443
```
