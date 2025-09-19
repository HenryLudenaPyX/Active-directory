# Introducción
<p> Este documento explica como instalar Samba en Linux, para este caso se va a usar Ubuntu 22.04 en una máquina virtual en VirtualBox.</p>

## Prerrequisitos:
<p> Es necesario recalcar que para este laboratorio se desactivo el firewall del sistema (solo recomendado para estas prácticas), de esta manera se evita cualquier interrupción, esto es
  con el siguiente comando: </p>
<code> sudo ufw disable</code>

## Pasos:
<h3> 1. Actualizar apt e instalar samba: </h3>
<code> sudo apt update </code> <br>
<code> sudo apt install -y samba </code>
<p> Se puede verificar el estatus de Samba para esta manera verificar una instalación correcta con el siguiente comando: </p>
<code> sudo systemctl status smbd nmbd </code>  

<img width="802" height="487" alt="image" src="https://github.com/user-attachments/assets/5085ae55-2be0-48a0-b398-835c83e750b4" />

<h3> 2. Crear directorio y compartir permisos </h3>
<p> Una vez creado el servidor se procede a crear la carpeta compartida donde se van a exponer los documentos </p>
<code> sudo mkdir -p /srv/samba/share </code>
<p> A este directorio no se le asigna a ningún grupo específico ni a un usuario porque se quiere que esté disponible para todos </p>
<code>sudo chown nobody:nogroup /srv/samba/share</code>
<p> Y si le asigna permisos de lectura y escritura </p>
<code> sudo chmod 0775 /srv/samba/share </code> <br>

<img width="628" height="220" alt="image" src="https://github.com/user-attachments/assets/6c7eefaf-a042-4a13-923c-1cb899c35876" />

<h3> 3. Configurar directorio share en samba </h3>
<p> Al instalar samba se crea un un archivo llamado smb.conf, este archivo contiene información como el nombre lo dice relacionada a la configuración.
La carpeta creada previamente creada solo es como un directorio cualesquiera hasta el momento, para que samba la reconozca se debe agregarla. </p>

``` bash
[global]
   workgroup = WORKGROUP
   server string = Samba Server %v
   netbios name = ubuntu-samba
   security = user
   map to guest = Bad User
   dns proxy = no

[share]
   path = /srv/samba/share
   browsable = yes
   read only = no
   guest ok = yes
   create mask = 0775
   directory mask = 0775
```
<p> guest ok = yes, es una parte importante porque permite que cualquier usuario anónimo acceda a la carpeta sin necesidad de credenciales, además de read only = no que permite la escritura</p>

<h3> 4. Reinicio y prueba</h3>
<p> Una vez configurado samba se realiza el reinicio del servicio para asegurarse que lo cambios se aplicaron </p>
<code>sudo systemctl restart smbd nmbd</code>
<p> Y luego se comprueba la configuración</p>
<code>testparm</code>
