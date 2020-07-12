# MySQL users

### MySQL recover root password

```
$ sudo /etc/init.d/mysql stop
$ sudo mkdir /var/run/mysqld
$ sudo chown mysql:mysql /var/run/mysqld
$ sudo mysqld_safe --skip-grant-tables &
$ mysql -uroot
```

```sql
> use mysql;
> update user set authentication_string=PASSWORD("mynewpassword") where User='root';
> update user set plugin="mysql_native_password" where User='root';
> flush privileges;
> quit
```


### MySQL adicionar novo usuário

```
mysql -u root -p
```
```sql
> create database django_db;

CREATE USER 'novousuario'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'novousuario'@'localhost'; # ou...
GRANT ALL PRIVILEGES ON django_db . * TO 'novousuario'@'localhost';
FLUSH PRIVILEGES;
```
`GRANT OPTION` permite conceder ou revogar privilégios de outros usuários

```sql
GRANT [tipo de permissão] ON [nome da base de dados].[nome da tabela] TO ‘[nome do usuário]’@'localhost’;
```

`OPTION`

* ALL PRIVILEGES como vimos anteriormente, isso daria a um usuário do MySQL todo o acesso a uma determinada base de dados (ou se nenhuma base de dados for selecionada, todo o sistema)
* CREATE permite criar novas tabelas ou bases de dados
* DROP permite deletar tableas ou bases de dados
* DELETE permite deletar linhas das tabelas
* INSERT permite inserir linhas nas tabelas
* SELECT permite utilizar o comando Select para ler bases de dados
* UPDATE permite atualizar linhas das tabelas


`REVOKE`

```sql
REVOKE [tipo de permissão] ON [nome da base de dados].[nome da tabela] FROM ‘[nome do usuário]’@‘localhost’;
```

`DROP`
```sql
DROP USER ‘demo’@‘localhost’;
```

Lembre-se `FLUSH PRIVILEGES`;

