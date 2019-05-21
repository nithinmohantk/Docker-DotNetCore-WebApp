### Useful docker-compose commands 


```console

docker-compose ps # lists all services (id, name)
docker-compose stop <id/name> #this will stop only the selected container
docker-compose rm <id/name> # this will remove the docker container permanently 
docker-compose up # builds/rebuilds all not already built container 

```

```console
docker-compose up -d --force-recreate --build

```

```console
Options:
  -d                  Detached mode: Run containers in the background,
                      print new container names. Incompatible with
                      --abort-on-container-exit.
  --force-recreate    Recreate containers even if their configuration
                      and image haven't changed.
  --build             Build images before starting containers.
```


 ```console 
docker-compose restart 
```
### Stop and Remove Container(s)

```console 
docker-compose stop dotnetcorebundle_contoso.api_1
docker-compose kill dotnetcorebundle_contoso.api_1
docker stop dotnetcorebundle_contoso.api_1
docker rm -f dotnetcorebundle_contoso.api_1

```



### Working with Kubernetes

```console
# Start minikube
minikube start

# Set docker env
eval $(minikube docker-env)

# Build image
docker build -t foo:0.0.1 .

# Run in minikube
kubectl run hello-foo --image=foo:0.0.1 --image-pull-policy=Never

# Check that it's running
kubectl get pods
```


### Pushing the container to DockerHub

```console 

docker login

docker tag bb38976d03cf thingxcloud/vslaunch-contoso-api-demo:v1
docker tag bb38976d03cf thingxcloud/vslaunch-contoso-api-demo:latest

docker push thingxcloud/vslaunch-contoso-api-demo
```

### Deploy the app to Kubernetes

```console
# 1. Step 1: Create Pods
kubectl run my-app --image=gcr.io/some-repo/my-app:v1 --port=3000

kubectl get pods

#2. Step 2: Expose the Kubernetes Deployment through a Load Balancer
kubectl expose deployment my-app --type=LoadBalancer --port=8080 --target-port=3000

#3. Step 3: Find the external IP of your Container
kubectl get svc

#4. (Extra) Step 4: Use Kubernetes Rolling Updates
kubectl set image deployment/my-app  my-app=gcr.io/some-repo/my-app:v2

#5. Clean Up 
kubectl delete deployment my-app
kubectl delete svc my-app

```

```console 

#
# Clean up dying pods
#
pods=$( kubectl get pods | grep -v Running | tail -n +2 | awk -F " " '{print $1}' )
for pod in $pods;
do
    kubectl delete pod $pod --grace-period=0 --force 
done

```