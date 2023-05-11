# docker-mysql8-phpmyadmin

Dockerized MySQL8 / PHPMyAdmin  
[https://github.com/AgathePons/docker_poe_db_mysql_conf_prod_and_tu](https://github.com/AgathePons/docker_poe_db_mysql_conf_prod_and_tu)

## Most important commands

### Run the **prod container** with good name:

```cmd
docker compose --env-file .env -p dbpoe-mysql-app up -d
```

### **Remove all** except the GUI volume (DB volume + datas folder + recreate the datas folder)

(**PowerShell** script)

```cmd
.\scripts\stop-remove-all-except-gui-vol.ps1
```

### Insert all datas (if the container has just been up, **run the back API project at least one time to build the tables**)

(**PowerShell** script)

```cmd
.\scripts\insert-data.ps1
```

-------------------

## Clone the project

`git clone git@github.com:AgathePons/docker_poe_db_mysql_conf_prod_and_tu.git`

## Move to the project folder

`cd docker_poe_db_mysql_conf_prod_and_tu`

## Run the container

`docker compose up -d`

## Run with another name and with another .env

For **TU** db

`docker compose --env-file .env-testu -p dbpoe-tu up -d`

For **prod** db

`docker compose --env-file .env -p dbpoe-mysql-app up -d`

## Dump table from docker image

```cmd
docker compose -p <docker-image_name> exec -it db mysqldump -u <user-name> -c -p -N -t -y --skip-opt --skip-comments --skip-quote-names post-suivi-stagiaire <table-name>
```

For "prod" docker with root user:

Show **in terminal**

```cmd
docker compose -p dbpoe-mysql-app exec -it db mysqldump -u root -c -pazerty -N -t -y --skip-opt --skip-comments --skip-quote-names post_suivi_stagiaire poe
```

Save **In file**

```cmd
docker compose -p dbpoe-mysql-app exec -it db mysqldump -u root -c -pazerty -N -t -y --skip-opt --skip-comments --skip-quote-names post_suivi_stagiaire poe > export-poe.sql
```

With set names (if the Docker image has a name set)

```cmd
docker exec -it <name of the service set> mysqldump -u root -c -pazerty -N -t -y --skip-opt --skip-comments --skip-quote-names --default-character-set=utf8 post_suivi_stagiaire poe > poe.sql
```

## Command to enter in mysql docker image prompt

```cmd
docker compose -p dbpoe-mysql-app exec -it db mysql -u poe -ppoe post_suivi_stagiaire
```

And `exit` to exit.

## To run the `.sql` file in mysql docker image

With **PowerShell**

Play `poe.sql`

```cmd
Get-Content data-poe.sql | docker compose -p dbpoe-mysql-app exec -T db mysql -u poe -ppoe post_suivi_stagiaire
```

Play `trainee.sql`

```cmd
Get-Content data-trainee.sql | docker compose -p dbpoe-mysql-app exec -T db mysql -u poe -ppoe post_suivi_stagiaire
```

With **cmd**

Play `poe.sql`

```cmd
docker compose -p dbpoe-mysql-app exec -T db mysql -u poe -ppoe post_suivi_stagiaire < data-poe.sql
```

Play `trainee.sql`

```cmd
docker compose -p dbpoe-mysql-app exec -T db mysql -u poe -ppoe post_suivi_stagiaire < data-trainee.sql
```

## Play `.bat` script

Delete data in table

`test`
