###  Configuração Nginx (Ubuntu Server 16.04):


## Execute os seguintes comandos:

```
sudo apt update
```
```
sudo apt install nginx
```

## Para criar um novo arquivo de configuração para o nginx, execute:

```
sudo nano /etc/nginx/sites-available/dominio.com
```
Em seguida entre com suas configurações citadas no arquivo '[config.conf](https://github.com/tiuram0n/nginx/blob/master/config.conf)',

Feche e salve.



## Publicando o site:
(O comando abaixo cria uma pasta virtual com o nome "config" em "/etc/nginx/sites-enabled/ )
```
sudo ln -s /etc/nginx/sites-available/dominio.com /etc/nginx/sites-enabled/
```


Depois de feito os passos acima, reinicie o nginx com o comando:

```
service nginx restart
```

Feito!
