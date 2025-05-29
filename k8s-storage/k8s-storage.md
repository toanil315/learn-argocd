## Install nfs common inside nodes

```bash
docker exec -it dev-cluster-control-plane bash
apt update && apt install -y nfs-common
exit

docker exec -it dev-cluster-worker bash
apt update && apt install -y nfs-common
exit
```

### Best Practice

build a new image containing kind/node based image and then install nfs-common inside it

```bash
FROM kindest/node:v1.29.0

RUN apt-get update && \
    apt-get install -y nfs-common && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
```

## Create folder nfs-data then assign properly permission for it

```bash
sudo chown -R nobody:nogroup ./nfs-data
sudo chmod -R 777 ./nfs-data
```

then run docker compose

### After run docker compose, exec this in nfs-server container

```bash
rpc.mountd
exportfs -v
```
