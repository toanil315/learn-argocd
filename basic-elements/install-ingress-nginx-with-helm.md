## Install helm

```bash
brew install helm
```

## Add ingress-nginx repo

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm pull ingress-nginx/ingress-nginx
tar -xzf ingress-nginx-4.12.2.tgz
```

## Change ingress-nginx config

```bash
>> Sửa type: LoadBalancing => type: NodePort
>> Sửa nodePort http: "" => http: "30080"
>> Sửa nodePort https: "" => https: "30443"
```

## Helm apply

```bash
kubectl create ns ingress-nginx
```

```bash
helm -n ingress-nginx install ingress-nginx -f ingress-nginx/values.yaml ingress-nginx
```

## Nginx apply

```bash
docker run -d \
  --name app-nginx \
  -p 8080:80 \
  -v ./basic-elements/nginx.conf:/etc/nginx/nginx.conf:ro \
  --network kind \
  nginx
```
