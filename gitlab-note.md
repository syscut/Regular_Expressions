### list all container
```
docker container ls
```
### check composoe settings
```
docker inspect <container id> | grep com.docker.compose
```
### run command in gitlab container
```
docker exec -it <container id> <your command>
```
