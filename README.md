# 1. Preparar las maquinas
## 1.1 Balanceador de carga

Para empezar tenemos que instalar el nginx y lo haremos con el comando: sudo apt install nginx -y

<img width="643" height="161" alt="imagen" src="https://github.com/user-attachments/assets/b8cbf910-0900-4524-aa38-ce0210d71e12" />

<img width="770" height="175" alt="imagen" src="https://github.com/user-attachments/assets/b6dab1ab-906a-4de1-a061-f361174c47d9" />

Para configurar el balanceador de carga haremos un sudo nano /etc/nginx/sites-available/default

Añadiremos la parte donde dice upstream y ademas las IP son de los dos front end.

<img width="390" height="155" alt="imagen" src="https://github.com/user-attachments/assets/4d08d63c-6365-496c-81e6-9db5c363fb4c" />

## 1.2 NFS Server (Capa de frontend)
Tendremos que instalar el kernel para compartir el contenido estático

<img width="699" height="161" alt="imagen" src="https://github.com/user-attachments/assets/578960e6-318d-4b35-aca6-fd6aa07ae482" />

Tendremos que crear la carpeta /var/www/html y cambiarle el usuario y el grupo por ninguno.

<img width="648" height="72" alt="imagen" src="https://github.com/user-attachments/assets/5f7b4ddd-d8e4-4fa2-b938-7232356f0316" />

Entraremos al archivo /etc/exports

<img width="805" height="342" alt="imagen" src="https://github.com/user-attachments/assets/12da53fe-3749-42f3-a1b5-b97f7d2fc795" />

Y por ultimo reiniciamos el servidor kernel.

<img width="662" height="49" alt="imagen" src="https://github.com/user-attachments/assets/806c98ab-c96e-4cff-bf63-10b339d9fcb3" />

## 1.3 Servidores web (Capa frontend)
Empezaremos instalando apache2

<img width="816" height="270" alt="imagen" src="https://github.com/user-attachments/assets/88d9443e-c904-4092-a6b7-23fb5cb8636f" />

<img width="521" height="115" alt="imagen" src="https://github.com/user-attachments/assets/613ef935-1187-4f11-8ab5-bf12e5f62693" />

Reiniciamos el apache2 para que se apliquen los canbios.

<img width="585" height="51" alt="imagen" src="https://github.com/user-attachments/assets/69fb8f45-5da7-4c25-84b2-621aad1bfebc" />

### Instalamos wordpress en front-end

<img width="816" height="315" alt="imagen" src="https://github.com/user-attachments/assets/8a110bcf-1ee4-4998-b556-fab0a8e467a8" />

<img width="536" height="315" alt="imagen" src="https://github.com/user-attachments/assets/ce00a8af-661a-47f6-a4b7-7aba04dbfaa8" />

<img width="680" height="53" alt="imagen" src="https://github.com/user-attachments/assets/0377ef06-9d11-40e6-8bd2-706d5dcd5feb" />

Esto se debe hacer en las dos maquinas de front-end. Solo se muestran las capturas de un solo Front-end.

## 1.4 Servidor de base de datos
Instalaremos el mysql server con este comando.

<img width="700" height="156" alt="imagen" src="https://github.com/user-attachments/assets/ef2a55a0-d0bc-4d0d-b5ce-37d8f6414b66" />

Entramos en /etc/mysql/mysql.conf.d/mysqld.cnf y modificamos la siguiente linea a como esta en la imagen.

<img width="811" height="568" alt="imagen" src="https://github.com/user-attachments/assets/2c456585-0101-4195-b5cc-c5c39ef4e793" />

Y ahora reiniciamos mysql.

<img width="540" height="47" alt="imagen" src="https://github.com/user-attachments/assets/d4d5dcbd-7831-4a3d-b736-e7f51a4c92a7" />

Entramos en mysql y creamos la base de datos y el usuario en mi caso se llamara la base de datos wordpress_db y el usuario atila.

<img width="619" height="334" alt="imagen" src="https://github.com/user-attachments/assets/f6f6067e-575d-49cd-b084-8da221dd262b" />

# 2 Sincronización del contenido estático en la capa de Front-End
## Paso 1: Instalación de paquetes

Instalamos el nfs en el servidor

<img width="699" height="159" alt="imagen" src="https://github.com/user-attachments/assets/00aab033-f64c-4014-83ad-215b22627a09" />

Y instalamos el nfs en los front-end

<img width="639" height="160" alt="imagen" src="https://github.com/user-attachments/assets/2d819bd2-3dfb-4878-af21-188ea31d89a1" />

## Paso 2: Exportamos el directorio en el servidor NFS
Ahora entramos en /etc/exports

<img width="806" height="314" alt="imagen" src="https://github.com/user-attachments/assets/1975e066-4e69-4ac6-b841-38322d0ba421" />

## Paso 3: Reiniciamos el servicio NFS
Y reiniciamos el servicio NFS

<img width="657" height="50" alt="imagen" src="https://github.com/user-attachments/assets/4b455584-078c-4a1e-8685-72dba982809a" />

## Paso 4: Creamos el punto de montaje en el cliente NFS
Donde 172.31.1.77 es la IP del servidor NFS que está compartiendo el directorio.

<img width="778" height="22" alt="imagen" src="https://github.com/user-attachments/assets/8f12e721-f615-4938-86c3-86f633941226" />

Donde 192.168.33.11 es la IP del servidor NFS que está compartiendo el directorio.

<img width="646" height="257" alt="imagen" src="https://github.com/user-attachments/assets/7f28054b-854d-4218-b95a-406c97064b7f" />

## Paso 5: Editamos el archivo /etc/fstab en el cliente NFS
Entramos en el /etc/fstab

<img width="480" height="51" alt="imagen" src="https://github.com/user-attachments/assets/c2dfb568-b0e3-4857-93be-e6795a466b66" />

Debemos de poner nuestra ip del servidor NFS

<img width="1004" height="113" alt="imagen" src="https://github.com/user-attachments/assets/a2f1886b-4569-48a5-81ac-361e210caae2" />
