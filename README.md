# simple-java-maven-app

Simple Spring Boot app with one endpoint:

- `GET /` -> `Hello from Spring Boot on Kubernetes`

## Run locally (without Kubernetes)

```bash
mvn spring-boot:run
```

Then open [http://localhost:8080/](http://localhost:8080/).

## Build container image

```bash
docker build -t my-app:local .
```

## Run on local Kubernetes

Apply manifests:

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### If using `kind`

Load the local image into the cluster first:

```bash
kind load docker-image my-app:local
```

Access the app:

```bash
kubectl port-forward service/my-app 8080:8080
```

Then open [http://localhost:8080/](http://localhost:8080/).

### If using `minikube`

Build image into minikube Docker daemon:

```bash
eval "$(minikube docker-env)"
docker build -t my-app:local .
```

Access the app:

```bash
minikube service my-app --url
```
