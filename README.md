# Retrieving files

Install git : https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

To start, create a new folder on your computer, open a terminal in it and run:

```bash
git clone https://github.com/Maxence1502/TD7A4.git
```

# With docker

Install docker : https://docs.docker.com/engine/install/

### Apache2 container (bind-mount)

In a terminal run the following command to start the container:
```bash
docker run -d -p 8080:80 -v "/mnt/c/Users/maxen/Desktop/GIT/ESILV/TD7A4/php:/usr/local/apache2/htdocs/" httpd:latest
```
Please change the volume path to match your GIT folder.

### MySQL container (volume)

In a terminal run the following command to create the volume:
```bash
docker volume create maxence-db
```

Then the following command to launch the container:
```bash
docker run -d -v maxence-db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=maxence mysql:latest
```

You can interact with the database with the following command:
```bash
docker exec -it 52ea339b7d2f mysql -u root -p
```
Don't forget to replace the container ID that you can get with ``docker ps``

For example you can add the data :
```sql
CREATE DATABASE maxence;
USE maxence;
CREATE TABLE users (
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
email VARCHAR(50) NOT NULL,
PRIMARY KEY (id)
);
INSERT INTO users (name, email) VALUES ('John Doe', 'johndoe@example.com');
```

# With docker-compose

Install docker-compose: https://docs.docker.com/compose/install/

In the docker-compose.yml file change the path to match your GIT folder:
```
- "/mnt/c/Users/maxen/Desktop/GIT/ESILV/TD7A4/php:/usr/local/apache2/htdocs"
```

Then in a terminal launch the containers with the command:
```bash
docker-compose up -d
```
