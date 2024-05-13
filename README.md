# Azure

Primero necesitamos una máquina virtual o virtual machines

Se crea una máquina virtual dentro del grupo de recursos. En regiones y zonas se encuentran distribuidas, se suele buscar el foco principal de clientes. Algunos pueden estar capados nen zonas y algunos pliegos donde se obligan a almacenar en servidores europeos.

 - Se busca una B1 o B2
 - El servidor nos interesa e West Europe (Europa)
 - Se usa una imagen de Windows 11 Pro o Ubuntu 22.04 LTS

Se puede calcular dentro de Azure Pricing Calculator for Virtual Machine. El Windows se escoge de Tier Basic.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/d5fc1a09-58dd-494c-b798-ab21e6c1e440)

Se debe realizar Create RDP File. Se accede por Acceso a Escritorio Remoto instalado en Windows usando la direccion IP.

Se tiene un archivo **myVm_key.pem** que contiene la clave de acceso
Acceso a la maquina virtual:
-	En el caso de Linux se usa SSH, para ello en Windows usamos PuTTY
-	En el caso de Windows a pedir la IP, las keys SSH
Abrimos una terminal e introducimos el siguiente comando **cd C:\Users\hecto\azure** para
acceder a la ubicación de la clave

Ejecutamos el comando **ssh -i myVm_key.pem azureuser@172.210.148.251** donde definimos donde esta la **clave privada de acceso a la maquina virtual** con el nombre **myVm_key.pem** y la dirección IP publica que es **172.210.148.251**

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/a4b4eeae-4cb1-4a46-9288-c95fcd02ce93)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/2cda2d25-c2f6-4165-be8b-3ea428a43b09)
 
Lo actualizamos con **sudo apt update**

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/d6337c22-e38c-4ceb-84d4-822f60db59a9)
 
Luego **sudo apt install nginx** para instalar nginx

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/ae6e8d9b-4c1a-4c59-acb3-18869fb6d90c)
 
Se hace **sudo systemctl status nginx** para mirar si el demonio está vo

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/e4b75872-3e4c-46cd-860d-0acfe4f9e851)
 
Se crea un puerto ACL de servicio custom en el 80, en protocolo TCP.
En este caso el puerto 80 se nos muestra la página de base
Se debe crear una regla dentro del puerto 443 para poder abrir la pagina

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/4861be2c-f198-4719-880c-481c97e19310)

Se crea un puerto ACL de servicio custom en el 80, en protocolo TCP.
En este caso el puerto 80 se nos muestra la página de base
(Falla) Se debe crear una regla dentro del puerto 443 para poder abrir la pagina
 

Se puede acceder a la configuración de usuario de nginx con los comandos de **cd /usr** y luego **cd local**

Para modificar instalamos nano con **sudo apt install nano** y modificamos el archivo **nginx.conf** de la carpeta de **/etc/nginx**.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/8b6d47a5-5a14-44e0-be37-5463fe7f1ac7)

Dentro de etc/nginx se puede acceder a **sites-enabled** y **sites-available**

Accedemos a **/var/www/html** y aquí esta la pagina original, aquí se crea el index

Creamos un **index.html** dentro de este sitio con **sudo nano index.html** para no tener problemas con permisos.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/88b28ad5-e340-44f1-a6b0-596621441c55)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/96b3a971-e26e-44b3-b267-344f629ac800)
 
Accedemos a **etc/nginx** y luego se accede a** sites-available**, para comprobar que se ha puesto previamente a cargarse el html de **index.html** al **index.nginx-debian.html**
  
![image](https://github.com/HectorCRZBQ/azure/assets/148070442/96585a3b-f54f-4714-9edf-0465d3781b19)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/ab960aa8-edd7-4bf0-913f-e59697396700)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/6fb57cb5-5e4d-48f6-95b7-dcb802471f71)
 
Para poder visualizar que nuestro **index.html** funciona de la manera correcta accedemos por medio del buscador a **http://172.210.148.251** que es la IP publica de nuestra maquina virtual

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/056a2706-b65f-4282-8ec4-a08743fd87ba)

Creamos un segundo **index2.html** dentro de este sitio con **sudo nano index.html** para no tener problemas con permisos.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/6cbdf879-88c8-4bc1-857f-b1c590dc538e)
 
Dentro de **etc/nginx** se puede acceder a **sites-enabled** y **sites-available**

Accedemos a **/var/www/html** y aquí esta la pagina original, aquí se crea el index

Creamos un **index2.html** dentro de este sitio con **sudo nano index2.html** para no tener problemas con permisos.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/37c70b01-3fc6-47dd-a269-ac7628e29f14)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/078923b7-065a-466e-898a-55009f37ddb6)
 
Accedemos a **etc/nginx** y luego se accede a **sites-available**, para comprobar que se ha puesto previamente a cargarse el html de **index2.html** al **index.nginx-debian.html**.

Para ello se acede a **/etc/nginx/sites-available** donde se ejecuta el comando **sudo nano default**, en este caso se sobrescribe en el archivo **default** el nombre de **index.html** por **index2.html**
 
![image](https://github.com/HectorCRZBQ/azure/assets/148070442/c633707e-ca7a-4e55-b741-6dd7c197683b)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/7afad7f9-f88a-4129-85cf-bd3f8ef2ceef)

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/c92b0166-91d2-4617-85cc-3044199747b2)

Se actualiza usando **sudo systemctl restart nginx**, debido a que hemos realizado modificaciones en la configuración de nginx.

Para poder visualizar que nuestro **index2.html** funciona de la manera correcta accedemos por medio del buscador a **http://172.210.148.251** que es la IP publica de nuestra maquina virtual

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/253f0e8e-b6c4-4406-9940-cc585fa0a93e)

**Importante siempre apagar la maquina cuando no se este usando desde el Portal de Azure** 

# Actividad

Donde esta var/www se añaden los html y se redireccionan que se ponga al dominio 1 nos lleve a primer html y cuando ponga al dominio dos nos lleve al segundo dominio.

Para el dominio 1: 
-	Creamos la carpeta de **dominio1** con el comando **sudo mkdir dominio1** dentro de **/var/www**
-	Para mover el **index.html** a **dominio1** realizamos el siguiente comando **sudo mv /var/www/html/index.html /var/www/dominio1/**

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/f0fce505-e7b6-4bf9-8bcc-8f14e16702ec)
 
Y hacemos lo mismo con el dominio 2:
-	Creamos la carpeta de **dominio2** con el comando **sudo mkdir dominio2** dentro de **/var/www**
-	Para mover el **index2.html** a **dominio2** realizamos el siguiente comando **sudo mv /var/www/html/index2.html /var/wcd ww/dominio2/**

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/986706a4-55aa-4666-bdd1-4ed571bcd5fa)

Para habilitar el dominio1 lo hacemos desde dentro **sites-available** dentro de **/etc/nginx** al archivo de **deafult** y modificamos el archivo.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/e1faff13-2b3d-4c0d-bc17-ddf234333b5e)

Para habilitar el dominio2 lo hacemos igual, desde dentro **sites-available** dentro de **/etc/nginx**.
En este caso lo posicionamos debajo del código ya existente del dominio1.

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/b722fbbf-60e0-44d7-a4d6-d934fdfcaa5b)
 
Como se han realizado modificaciones en la configuración de nginx, se actualiza usando **sudo systemctl restart nginx**.

**Para el dominio 1 (midominio1 y www.midominio1)**:
-	Dirección del sitio: http://midominio1
-	Dirección del sitio (con www): http://www.midominio1
**Para el dominio 2 (midominio2 y www.midominio2)**:
-	Dirección del sitio: http://midominio2
-	Dirección del sitio (con www): http://www.midominio2

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/8fe44227-d6b6-4718-bb79-0530654e43cf)

**Siempre cuando terminemos de usarla, debemos apagar la máquina virtual.**

![image](https://github.com/HectorCRZBQ/azure/assets/148070442/94495bb6-239c-4efb-b5bb-3f0f2dbfcb7e)
