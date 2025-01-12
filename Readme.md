# Instalación de oddo de 2 formas :smile:

**Indice**
1. Usando docker
2. descargando la version desde la página oficial


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



