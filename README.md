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

## Vulnerabilities y verciones en el software

### OpenSSH

La ultima version de este programa es: OpenSSH 9.3/9.3p1 (2023-03-15)

>  https://www.openssh.com/releasenotes.html


### APACHE

La ultima version de este programa es: 2.4.57 (released 2023-04-06)

> https://httpd.apache.org/download.cgi







