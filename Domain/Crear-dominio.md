# Crear Dominio AD

<p> Esta descripción es para crear un Dominio en AD en Windows Server con GUI, para este caso se va a usar Windows Server 2022.</p>
<p> 1. Ir al Administrador del Servidor e ingresar a Roles y Características</p>
<img width="1011" height="259" alt="image" src="https://github.com/user-attachments/assets/a1c51ba5-82c9-45fc-8fa6-0ff2a6494d1a" />

<p> 2. Una vez aparece la pestaña correspondiente, se selecciona siguiente (todos las opciones por defecto) hasta llegar a Roles del Servidor, 
  en esta sección aparte de los Servicios de Dominio, se pueden agregar varios roles al servidor como agregar un servidor DNS o un DHCP y de esta 
  manera se le destina un uso al servidor, en este caso con Servicios de Dominio de AD lo que se está haciendo es prácitcamente crear un servidor AD. </p>
<img width="855" height="498" alt="image" src="https://github.com/user-attachments/assets/dbf468fa-8dd2-4283-ad7c-e5cfd0d5c44d" />
<p> 3. Luego se da clic en Siguiente hasta llegar a la Instalación, debido a que no se quiere añadir ninguna característica extra </p>
<p> 4. Una vez se ha instalado el Servicio, se seleccionar Añadir este Servidor como Controlador de Dominio, técnicamente lo que hace es que el servidor se convierta en el nodo central de toda la red de AD.
En la nueva pestaña se selecciona Nuevo Bosque porque este Dominio es nuevo, no ha habido ninguno previo y se escoge un nombre cualesquiera para el dominio</p>

<img width="767" height="683" alt="image" src="https://github.com/user-attachments/assets/a8266dc4-3a3b-4d46-9b2c-9e0e35d4bbf9" />

<p> 5. Para ejecutar una posible restauración del sistema se esocge una contraseña cualesquiera</p>
<img width="749" height="538" alt="image" src="https://github.com/user-attachments/assets/d71c61d4-3f42-4c96-8d34-250c6a7cc502" />

<p> 6. Se da clic en Siguiente hasta llegar a las Rutas, en este caso no hay que cambiar nada, pero es importante tener en cuenta que aquí se guarda la configuración del Directorio. 
  Luego se continúa dando clic en Siguiente hasta la instalación</p>
<img width="758" height="552" alt="image" src="https://github.com/user-attachments/assets/4718f3a8-6e0d-41fa-8d65-d6493c059cc7" />

<p> 7. Una vez finalizada la instalación la máquina se reinicia, y entonces una manera de reconocer que se tiene el servicio de Active Directory 
  correctamente levantado es con el dominio junto al nombre del usuario</p>
<img width="989" height="741" alt="image" src="https://github.com/user-attachments/assets/b68555e2-fcd9-426a-aa0c-146e05195a1c" />

