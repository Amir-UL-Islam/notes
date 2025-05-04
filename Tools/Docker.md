### Images and containers
A container is nothing but a running process, with some added encapsulation features applied to it in order to keep it isolated from the host and from other containers. One of the most important aspects of container isolation is that each container interacts with its own private filesystem; this filesystem is provided by a Docker **image**.

An image includes everything needed to run an application - the code or binary, runtimes, dependencies, and any other filesystem objects required.
### Containers and virtual machines
A container runs _natively_ on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

By contrast, a **virtual machine** (VM) runs a full-blown “guest” operating system with _virtual_ access to host resources through a hypervisor. In general, VMs incur a lot of overhead beyond what is being consumed by your application logic.

|                                                                                   |                                                                                  |
| --------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| ![Container stack example](https://docker-docs.uclv.cu/images/Container%402x.png) | ![Virtual machine stack example](https://docker-docs.uclv.cu/images/VM%402x.png) |
### Basic

1. docker inspect container

```bash
docker exec -it [container-name] bash
```
2. Kill Port for same service exist in Local and Docker

   ```bash
sudo kill `sudo lsof -t -i:3306`
```
### MariaDB

- Create Container

```bash
docker run --name mariadbtest -e MYSQL_ROOT_PASSWORD=mypass -p 3306:3366 -d mariadb:10.3
```

- Log In to Docker MariaDB

```bash
mysql -h localhost -P 3366 --protocol=TCP -u root -p
```

- or  User this command if you don't have MySQL installed in your system

```bash
docker exec -it mysql mysql -u root -p
```

- Import Database

```bash
docker exec -i mysqlvii mysql -u root --password=Ittertools.com88 etbmanager < etbmanager-2023-10-03_01-00-01.sql
```

### MySQL

```bash
docker run --name mysql -v /Users/amir/Desktop/my.cnf:/etc/mysql/my.cnf -e MYSQL_ROOT_PASSWORD=Ittertools.com88 -p 3306:3366 -d mysql:5.7
```

### Postgres
```bash
docker run --name postgres -e POSTGRES_PASSWORD=Ittertools.com88 -p 5432:5432 -d postgres:14
docker exec -it postgres  psql -h localhost -U postgres
```
