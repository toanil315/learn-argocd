## List all local images loaded inside Kind cluster

```bash
docker exec -it dev-cluster-control-plane crictl images
```

## Delete

```bash
docker exec -it dev-cluster-control-plane crictl rmi docker.io/library/ecommerce-backend:v1
```
