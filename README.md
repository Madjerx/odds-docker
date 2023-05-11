# docker-mysql8-phpmyadmin

Dockerized MySQL8 / PHPMyAdmin  


## Most important commands

### Run the **prod container** with good name:

```cmd
docker compose --env-file .env -p dbodds-mysql-app up -d
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


## Move to the project folder


## Run the container

`docker compose up -d`

## Run with another name and with another .env

For **TU** db

`docker compose --env-file .env-testu -p dbodds-tu up -d`

For **prod** db

`docker compose --env-file .env -p dbodds-mysql-app up -d`

## Dump table from docker image

```cmd
docker compose -p <docker-image_name> exec -it db mysqldump -u <user-name> -c -p -N -t -y --skip-opt --skip-comments --skip-quote-names dbodds <table-name>
```

For "prod" docker with root user:

Show **in terminal**

```cmd
docker compose -p dbodds-mysql-app exec -it db mysqldump -u root -c -pazerty -N -t -y --skip-opt --skip-comments --skip-quote-names dbodds <table-name>
```

Save **In file**



## Command to enter in mysql docker image prompt
