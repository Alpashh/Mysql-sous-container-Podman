# MySQL-Podman

## Quick Tutorial for Installing and Using MySQL with a Podman Container

### Prerequisites

- Ensure that Podman is installed on your system. You can follow the installation instructions for your operating system [here](https://podman.io/getting-started/installation).

### Steps

#### 1. Install Podman and MySQL

To install MySQL using Podman, run the following command:

```sh
podman run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```

### 2. Verify the MySQL Container is Running

To check if the MySQL container is running, use the following command:

```
podman ps
```

This command lists the running containers, and you should see your MySQL container in the list.

### 3. Connect to MySQL from the Container

You can connect to MySQL directly from the container using the following command :

```
podman exec -it mysql mysql -uroot -p
```

You will be prompted to enter the root password you set (`my-secret-pw`).

### 4. Connect to MySQL from the Host

If you want to connect to MySQL from your host (the machine where Podman is installed), you need to expose the MySQL port. To do this, stop the existing container and restart it with the port exposed:

```
podman stop mysql
podman rm mysql
podman run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql:latest
```

Now, you can connect to MySQL from your host using a MySQL client or the command line:

```
mysql -h 127.0.0.1 -P 3306 -uroot -p
```
