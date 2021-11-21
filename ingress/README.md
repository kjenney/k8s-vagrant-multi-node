# ingress

To stand up an NGINX ingress:

1. Stand up cluster `BOX_OS=ubuntu KUBERNETES_VERSION=1.21.7 make up -j 3`
2. Deploy NGINX controller

```
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

3. Deploy

```
kubectl apply -f sample.yaml
```

4. Test services

```
kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 8080:80 &
curl http://demo1.localdev.me:8080/
curl http://demo2.localdev.me:8080/
killall kubectl
```

5. Cleanup

```
kubectl delete -f sample.yaml
```