### 1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.

La imagen se puede descargar con el comando: <code>docker image pull httpd:2.4</code>  
Para comprobar que la imagen se ha descargado correctamente utilizamos <code>docker images</code>, obteniendo:  
~~~
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
alpine        latest    91ef0af61f39   5 weeks ago     7.8MB
httpd         2.4       1bcf11fa154f   3 months ago    148MB
hello-world   latest    d2c94e258dcb   17 months ago   13.3kB
~~~

### 2. Crea un contenedor con el nombre 'dam_web1'.

Para crear el contenedor con el nombre indicado se utiliza: <code>docker create --name dam_web1 httpd:2.4</code>
Para comprobar que se creó correctamente y obtener su nombre utilizamos docker ps -a, obteniendo:  
~~~
CONTAINER ID   IMAGE         COMMAND              CREATED              STATUS                  PORTS     NAMES
5047f80cfe75   httpd:2.4     "httpd-foreground"   About a minute ago   Created                           dam_web1
~~~

### 3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer?

Como no puedo modificar el contenedor previamente, lo elimino con <code>docker rm dam_web1</code>.
Creo un nuevo contenedor indiciando el puerto con <code>docker run --name dam_web1 -d -p 8000:80 httpd:2.4</code>
- --name -> Para ponerle un nombre al contenedor
- -d -> Para que se ejecute en segundo plano
- -p -> Para indiciar el puerto

![image](https://github.com/user-attachments/assets/db08b0fa-5540-4722-9343-87849dca4c78)


### 4. Utiliza bind mount para que el directorio del apache2 'htdocs' esté montado un directorio que tu elijas.

De nuevo, no puedo modificar el contenedor ya creado y la única forma que encontré de realizarlo es eliminar el creado previamente <code>docker rm dam_web1</code> y crearlo nuevamente con todos los parámetros que necesito:    
<code>docker run --name dam_web1 -d -p 8000:80 -v /home/enrique/web:/usr/local/apache2/htdocs httpd:2.4</code>
