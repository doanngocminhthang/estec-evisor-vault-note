```
(venv) PS D:\estec\project\estec_evisor\estec_evisor_code\EVisor---Backend---RnD> docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                  again.
At line:1 char:1
+ docler ps
+ ~~~~~~
    + CategoryInfo          : ObjectNotFound: (docler:String) [], CommandNotFoundException
     NAMES
4e2f60f0cb0d   postgres:15                     "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp                                                postgres
b59d89691a33   portainer/portainer-ce:latest   "/portainer"             3 minutes ago   Up 3 minutes   0.0.0.0:9000->9000/tcp, [::]:9000->9000/tcp                                                portainer
79020d93ff61   minio/minio:latest              "/usr/bin/docker-ent…"   3 minutes ago   Up 3 minutes   0.0.0.0:9090->9090/tcp, [::]:9090->9090/tcp, 0.0.0.0:9009->9000/tcp, [::]:9009->9000/tcp   minio
ad81a5084f99   postgres:latest                 "docker-entrypoint.s…"   11 days ago     Up 2 hours     0.0.0.0:15432->5432/tcp, [::]:15432->5432/tcp                                              wildfire-postgres
```

