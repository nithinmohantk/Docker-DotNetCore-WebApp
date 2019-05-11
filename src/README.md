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