###  Configuração Nginx:


## Rode os comandos:

```
sudo apt update
```
```
sudo apt install nginx
```

## Para criar um novo arquivo de configuração, execute:

```
sudo nano /etc/nginx/sites-available/config.conf
```

Em seguida entre com suas configurações citadas no arquivo "[config.conf](https://raw.githubusercontent.com/tiuram0n/nginx/master/config.conf)",

Feche e salve.



## Publicando o site
```
sudo ln -s /etc/nginx/sites-available/config.conf /etc/nginx/sites-enabled/
```


Depois reinicie o Nginx com o comando:

```
service nginx restart
```

Feito!
