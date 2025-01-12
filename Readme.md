# Instalación de oddo de 2 formas :smile:

**Indice**
1. Usando docker (forma fácil)
2. paso a paso manualmente (forma difícil)


## 1. Usando docker 🕶️

**Requisitos previos** :hushed:
- tener instalado docker en tu entorno de trabajo

Una vez tengas docker instalado, podemos comenzar

**Como instalar la version 17.0 de odoo (Comunity) con docker**

```bash
#Creamos un directorio donde vamos a meter el docker compose
mkdir docker_compose_odoo
cd docker_compose_odoo
nano docker-compose.yml
```

Una vez dentro, copia y pega lo siguiente:

```bash
services:
  web:
    image: odoo:17.0
    depends_on:
      - mydb
    ports:
      - "8069:8069"
    environment:
      HOST: mydb
      USER: odoo
      PASSWORD: myodoo
    volumes:
      - odoo-web-data:/var/lib/odoo

  mydb:
    image: postgres:15
    environment:
      POSTGRES_DB: postgres
      POSTGRES_PASSWORD: myodoo
      POSTGRES_USER: odoo
    volumes:
      - odoo-db-data:/var/lib/postgresql/data

volumes:
  odoo-web-data:
  odoo-db-data:
```

Guardamos y cerramos.

```bash
#Ejecuta lo siguiente dentro de la carpeta donde está el docker-compose.yml
sudo docker-compose up
```
Si todo ha ido bien iremos a **(http://(ip de tu maquina virtual o entorno de trabajo):8069

Debería de salir esto 

![instalacion1Parte2](https://github.com/user-attachments/assets/70d0efa1-f59c-443e-af36-fde33672aed9)

```bash
#Creamos la base de datos
```

![instalacion1Parte3](https://github.com/user-attachments/assets/a22945d7-a3a9-4ad4-a197-4ed2a4c1ee09)

```bash
#le damos a aceptar y saldrá la siguiente imagen
```

![instalacion1Parte4](https://github.com/user-attachments/assets/5be327e5-fea6-4b91-aa7c-bc79a4a8291e)

```bash
#usa las credenciales que pusiste en el apartado anterior, dale a enter y entrarás a odoo
```

![instalacion1Parte5](https://github.com/user-attachments/assets/44f4d359-043b-4cc3-af49-45876c160c14)

```bash
#Comprobación de que tienes la versión 17.0 y la community
```

![instalacion1Parte6](https://github.com/user-attachments/assets/1427dd31-332f-4e55-a047-d7496410df30)

### FELICIDADES, INSTALASTE ODOO CON DOCKER Y AHORA PODRÁS USARLO COMO PREFIERAS 🥳🥳🥳


### 2. Paso a paso :smile:

```bash
#En linux en el terminal del entorno de trabajo ejecutamos
sudo apt update
sudo apt upgrade 
```

```bash
#Despues ejecutamos las siguientes dependencias de python
sudo apt install python3-dev python3-pip python3-venv build-essential libxml2-dev libxslt1-dev zlib1g-dev libsasl2-dev
libldap2-dev libssl-dev libmysqlclient-dev libjpeg8-dev liblcms2-dev libblas-dev libatlas-base-dev -y
```

```bash
#Creamos un usuario dedicado a odoo
sudo adduser --system --home /opt/odoo --group odoo
```

```bash
#Descargamos odoo desde el repositorio oficial
sudo apt install git -y
sudo su - odoo
git clone --branch 17.0 https://github.com/odoo/odoo .
```

```bash
#Creamos un entorno virtual para python
sudo su - odoo
python3 -m venv odoo-venv
source odoo-venv/bin/activate
```

```bash
#Dentro del entorno virtual, instalamos las dependencias necesarias para odoo
pip install -r /opt/odoo/requirements.txt
```

```bash
#Ahora necesitas crear un archivo de configuración para Odoo. Crea el archivo odoo.conf en /etc/odoo:
sudo mkdir /etc/odoo
sudo nano /etc/odoo/odoo.conf
```

```bash
#Agrega lo siguiente en el archivo odoo.conf:
[options]
   ; This is the password that allows database operations:
   admin_passwd = admin
   db_host = False
   db_port = False
   db_user = False
   db_password = False
   dbfilter = .*
   log_level = info
   logfile = /var/log/odoo/odoo.log
   addons_path = /opt/odoo/addons
   xmlrpc_port = 8069
```

```bash
#Odoo necesita un directorio para almacenar los archivos de log. Crea este directorio y asigna los permisos adecuados.
sudo mkdir /var/log/odoo
sudo chown odoo: /var/log/odoo
```

```bash
#Ejecuta odoo
sudo su - odoo
./odoo-bin -c /etc/odoo/odoo.conf
```

```bash
#accede a odoo
http://localhost:8069
```
