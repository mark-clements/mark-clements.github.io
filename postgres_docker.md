---
layout: default
title: Postgresql on EC2 with Docker
---

## Simple Postgresql database on an AWS EC2 Instance using Docker  

### 1) Get docker container from hub.docker
```sudo docker pull postgres```

>*You can view the dockerfile settings here: https://github.com/docker-library/postgres/blob/0d0485cb02e526f5a240b7740b46c35404aaf13f/12/Dockerfile*

### 2) Check image now exists on server  
```sudo docker images```   
Should show an image called "postgres"

- Make a note of the Image ID, needed for the next step

### 3) Create persistent data volume container

```sudo docker create -v /var/lib/postgresql/data --name <my_postgres_volume><image_ID>```   
E.g.
sudo docker create -v /var/lib/postgresql/data --name my_postgres_volume cf879a45faaa

### 4) Check that the volume exists with:   
```sudo docker volume ls```   
```sudo docker volume inspect```

### 5) Check that the w container <my_postgres..> with
```sudo docker container ps -a```
```sudo docker container inspect my_postgres_volume```

### 6)  run the PostreSQL container
sudo docker run --name postgres \
-p 5432:5432 \
-e POSTGRES_PASSWORD=password \
-e POSTGRES_USER=myusername \
-e POSTGRES_DB=my_postgres_db \
-d --volumes-from my_postgres_volume postgres

> Note: if you receive the error 'container already exists' try deleting the stock container named 'postgres' with ```sudo docker rm <containerid>```

### 7) Check your postgres_db container is up
```sudo docker container ps```

### 8) Log in to container:
```sudo docker exec -it <containerID> /bin/bash```   
E.g. sudo docker exec -it 0a1073e01b25 /bin/bash

### 9) Change dir to the location of the config files   
In our case these were at: *cd /var/lib/postgresql/data*   

### 10) Install a file editor  
E.g.
```apt-get update```   
```apt-get install vim```
> Alternatively you could setup a shared file volume or copy the file across (we'll not cover that here).   

### 11) Edit the file   
```vi postgresql.conf```   
Check that the listen_addresses is set to '*':
```listen_addresses='*'```

### 12) Edit pg_hba.conf  
```vi pg_hba.conf```   
Check you have a line *host all all 0.0.0.0/0 md5* or *host all all all md5*

### 13) You should be done!
Check you're able to access the database with   
```psql my_postgres_db```

A few commands :  
\c prog_logs (connect to db)   
\l (list all db)   
\dt (table in current db)   
\q to quit   

### 14) Login to remote ec2 from local machine   
```psql -U <my_username> -p 5432 -h <your_vm_ip_and_region>.compute.amazonaws.com my_postgres_db```  


