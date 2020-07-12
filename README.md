# MySQL Tutorial
## Description

In this tutorial we will show the main features from [MySQL](https://www.mysql.com/).

Read [this tutorial](https://support.rackspace.com/how-to/install-mysql-server-on-the-ubuntu-operating-system/) from Rackspace.

## Install

```
$ sudo apt-get install mysql-server
```

## Start service

```
$ sudo systemctl start mysql
```

## Launch at reboot

```
$ sudo systemctl enable mysql
```

## Connect with mysql shell

```
$ mysql -u root -p
```

## Create database

```sql
mysql> create database zoo;
```

## Create user for database

```sql
mysql> CREATE USER 'novousuario'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL PRIVILEGES ON zoo . * TO 'novousuario'@'localhost';
mysql> FLUSH PRIVILEGES;
```
## Create table

Read [this tutorial](https://dev.mysql.com/doc/refman/8.0/en/loading-tables.html) fom MySQL.
```sql
mysql> use zoo;
mysql> CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20),
       species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);
```

## Insert data

```sql
mysql> INSERT INTO pet
       VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
```

## Load data from file

```sql
mysql> load data local infile '/path/pet.txt' into table pet FIELDS TERMINATED BY ',';
```

```txt
Fluffy,Harold,cat,f,1993-02-04,
Claws,Gwen,cat,m,1994-03-17,
Buffy,Harold,dog,f,1989-05-13,
Fang,Benny,dog,m,1990-08-27,
Bowser,Diane,dog,m,1979-08-31,1995-07-29
Chirpy,Gwen,bird,f,1998-09-11,
Whistler,Gwen,bird,,1997-12-09,
Slim,Benny,snake,m,1996-04-29,
```

## Update records 

```sql
mysql> update pet set sex = 'm' where name = 'Fluffy';
```
## Delete records

```sql
mysql> delete from pet;
```