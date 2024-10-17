# Práctica 2.1 - Instalación y configuración de un servidor web Nginx

## Instalación del servidor

Lo primero que hice actualizar los repositorios he instalar nginx

![Imagen 1](assets//Imágenes/1.png)

Comprobamos que esté bien instalada

![Imagen 2](assets/Imágenes/2.png)

Ahora creamos la carpeta del sitio web y clonamos el repositorio https://github.com/cloudacademy/static-website-example para poder realizar las pruebas.

![Imagen 3](assets//Imágenes/3.png)

Clonamos

![Imagen 4](assets/Imágenes/4.png)

Ahora nos aseguramos que el usuario del servicio web pueda acceder a la carpeta donde está alojado el servidor.

![Imagen 5](assets/Imágenes/5.png)

Por último comprobamos que si entramos a la ip de la máquina esta de servicio. En mi caso, en la wifi de mi casa era 192.168.1.250

![Imagen 6](assets/Imágenes/7.png)

## Configuración del servidor web

Ahora abordamos la correcta configuración del servidor. Para ello creamos un archivo de configuración en la ruta sudo nano /etc/nginx/sites-available/vuestro_dominio y configuramos el archivo.

![Imagen 7](assets/Imágenes/9.png)

![Imagen 8](assets/Imágenes/8.png)

Cuidado que la directiva root debe de tener la ruta absoluta del archivo index.html

Ahora creamos un archivo simbólico entre este archivo y el de sitios que están habilitados. Esto es para que el servidor sepa que nuestro sitio web está habilitado.

![Imagen 9](assets/Imágenes/10.png)

Por último reiniciamos el servicio.

![Imagen 10](assets/Imágenes/11.png)

Ahora comprobamos que todo haya sido configurado correctamente. Primero antes de nada modificaremos el archivo /etc/hosts para que nuestra máquina anfitriona asocie la IP de la máquina virtual con el nombre del servidor

![Imagen 11](assets/Imágenes/14.png)

Para terminar esta parte comprobaremos los registros del servidor. Miraremos primero el log de las peticiones correctas y después las incorrectas, para ver si se registran correctamente.

![Imagen 12](assets/Imágenes/15.png)

EL de las incorrectas

![Imagen 13](assets/Imágenes/16.png)

## FTP

Lo primero que debemos de hacer es descargar vsftpd

![Imagen 14](assets/Imágenes/17.png)

Ahora creamos el directorio donde vamos a copiar las cosas y creamos los certificados de seguridad necesarios

![Imagen 15](assets/Imágenes/18.png)

![Imagen 16](assets/Imágenes/19.png)

Ahora vamos al archivo de configuración y después de eliminar las siguientes lineas: 

```
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
```

añadimos:

![Imagen 17](assets/Imágenes/20.png)

Después reiniciamos el servicio e instalamos filezilla

![Imágenes 18](assets/Imágenes/21.png)

![Imágenes 19](assets/Imágenes/22.png)

Ahora entramos en el filezilla. Para conectarnos en la parte de servidor ponemos la ip de este, después el nombre del usuario con el que accedemos. Si entramos por el puerto 22 que es el de SFTP no hace falta poner contraseña. Esto es porque el servidor ya tiene mi clave pública ssh. 

![Imagen 20](assets/Imágenes/23.png)

Como vemos sale el certificado que hemos configurado antes con openssl. Ahora transferimos un archivo para hacer la comprobación de que funciona bien.

![Imagen 21](assets/Imágenes/25.png)

## HTTPS

Para esto tenemos que generar otro grupo de claves ssl y creamos un directorio que las contenga

![Imagen 22](assets/Imágenes/26.png)

Generamos la clave

![Imagen 23](assets/Imágenes/27.png)

Modificamos el archivo de configuración de Nginx para que oiga las peticiones al puerto 443 y redireccionamos las peticiones del puerto 80. 

![Imagen 24](assets/Imágenes/28.png)

Por último comprobamos que funcione

![Imagen 25](assets/Imágenes/29.png)

![Imagen 26](assets/Imágenes/30.png)