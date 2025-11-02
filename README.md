# Taller Autoguiado: Vagrant con Provisionamiento

## 👨‍💻 Autor
**Saith Gurrute Granada**

## 🎯 Objetivo del Proyecto
Crear y configurar un entorno de desarrollo de infraestructura-como-código utilizando **Vagrant** y **VirtualBox**. El entorno se compone de dos máquinas virtuales:
1.  **Servidor Web:** Con **Apache** y **PHP** para servir la aplicación.
2.  **Servidor DB:** Con **PostgreSQL** para la base de datos.

El reto final consiste en demostrar la comunicación exitosa entre PHP y PostgreSQL, mostrando datos de la base de datos en la web.

---

## 🚀 Instalación y Despliegue

### Requisitos Previos

Asegúrate de tener instalado en tu máquina local:
1.  **VirtualBox**
2.  **Vagrant**

### Pasos de Inicio

1.  Abre la terminal en el directorio raíz donde se encuentra el `Vagrantfile`.
2.  Inicia y provisiona ambas máquinas virtuales con un solo comando:

    ```bash
    vagrant up
    ```

---

## 📋 Configuración y Scripts

| Máquina | Rol | Dirección IP | Servicios Instalados |
| :--- | :--- | :--- | :--- |
| **web** | Servidor Web/Aplicación | `192.168.33.10` | Apache, PHP, Cliente PostgreSQL |
| **db** | Servidor de Base de Datos | `192.168.33.11` | PostgreSQL 12 |

### 📄 Scripts de Provisionamiento

#### `provision-web.sh`
Este script instala Apache, PHP y el módulo para PostgreSQL. También copia los archivos `index.html` e `info.php`.

```bash
#!/bin/bash
echo "--- Provisionando servidor WEB (Apache y PHP) ---"
apt-get update -y
apt-get install -y apache2 php libapache2-mod-php php-pgsql postgresql-client

# Habilitar modulos necesarios
a2enmod rewrite

# Copiar archivos del proyecto al directorio web
cp /vagrant/index.html /var/www/html/
cp /vagrant/info.php /var/www/html/

# Reiniciar Apache para aplicar cambios
service apache2 restart

echo "--- Provisionamiento de WEB completado ---"
