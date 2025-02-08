## dev

### excute the commmand

1. clone rpo
2. create .env file base on `.env.template`
3. excute `git submodule --init --recursive` to rebuild repos

```
    docker-compose up -d
```


## add a module

```
    git submodule add https://github.com/microservices-jdvpl/payments-ms
```

## run for prod

```
 docker compose -f docker-compose.prod.yml build
```

## create deployment config for services:

```
    kubectl create deployment client-gateway --image=us-east1-docker.pkg.dev/microservices-store-449702/registry-image/client-gateway-prd -
-dry-run=client -o yaml>deployment.yml
```


## register artifact

```
    kubectl create secret docker-registry grc-json-key --docker-server=us-east1-docker.pkg.dev --docker-username=_json_key --docker
-password="$(cat '/Users/jdvpl/Documents/nest/microservices/microservices-store-449702-20293ab250f1.json')" --docker-email=jdvplsuarez@gmail.com
```


## patch service

```
    kubectl patch serviceaccounts default -p '{"imagePullSecrets":[{"name":"grc-json-key"}]}'
```