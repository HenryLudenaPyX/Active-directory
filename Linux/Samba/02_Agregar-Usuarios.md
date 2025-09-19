# Introducción

<p> Antes de todo cabe recalcar que esta parte es si previamente se definió como guest ok = no al modificar el archivo smb.conf, debido a que en ese caso
  el servidor solo permite ingresar a la carpeta compartida a usuarios con credenciales, caso contrario, cualquiera puede entrar. </p>
<p> Previamente se describió como crear un directorio compartido en Samba, ahora para que otros usuarios puedan ingresar a ese directorio se requiere 
crear usuarios esto debido al parámetro security = user que se usó previamente, que dice que solo usuarios pueden ingresar. </p>

## Instrucciones:
<h3> 1. Crear usuario </h3>
<p> Primero se crea un usuario en Linux para que este tenga acceso al directorio compartido, en este caso se llama "atacante"</p>
<code> sudo useradd -M -s /usr/sbin/nologin atacante </code>
<p> Luego se le asigna una contraseña de smb</p>
<code>sudo smbpasswd -a atacante</code>
<p> Se habilita el usuario samba</p>
<code> sudo smbpasswd -e atacante</code> <br>
<img width="651" height="122" alt="image" src="https://github.com/user-attachments/assets/3d9129c7-ed80-460b-9384-aab72b18a0e9" />

<h3> 2. Usuario administrador </h3>
<p> Este paso puede ser opcional, pero si se quiere que el usuario administre el directorio share</p>
<code> sudo chown atacante:atacante /srv/samba/share</code>

<h3> 3. SMBv1 en el servidor </h3>
<p> En la mayoría de los casos al crear un servidor este tiene las versiones SMBv3 o SMBv4, y el cliente se suele conectar mediante SMBv1, entonces
en esos casos hay dos opciones: forzar al cliente a usar una versión más reciente de SMB, o permitir que el servidor acepte SMBv1 (vulnerable a EternalBlue)</p>
<p>Para este caso al ser un laboratorio de pentesting se usa el segundo </p>
<p> Para ello se accede al archivo de configuraciones del servidor </p>
<code> sudo nano /etc/samba/smb.conf </code>
<p> Luego en Global se añaden las siguientes líneas que es para establecer como protocolo mínimo una versión antigua y que siga aceptando 
  protocolos recientes como máximo</p>
  
``` bash
[global]
   server min protocol = NT1
   server max protocol = SMB3_11
```
<p> Luego se hace el reinicio del servidor </p>
<code> sudo systemctl restart smbd nmbd</code>
<p> Y se comprueba el estado del servidor</p>
<code> sudo systemctl status smbd -l</code>
<img width="720" height="420" alt="image" src="https://github.com/user-attachments/assets/caf16520-f749-463f-84b4-d2f31c550cdb" />

<p> Pero en caso de no desear que el servidor sea vulnerable, entonces se puede forzar al cliente a usar la versión más reciente</p>
<code>smbclient -L //192.168.23.7 -U atacante -m SMB3</code>

<h3> 4. Conectarse desde el cliente</h3>
<p> Una vez el servidor está listo se puede conectar desde el cliente, al hacerlo pedirá la contraseña previamente creada</p>
<code>smbclient -L //IP_SERVER -U atacante -m NT1</code>
<img width="621" height="301" alt="image" src="https://github.com/user-attachments/assets/05f83e47-d0ce-442f-981b-232fa1c73d23" />
