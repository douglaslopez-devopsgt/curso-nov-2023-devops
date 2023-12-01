Crear un repositorio en GitHub es un proceso relativamente sencillo. A continuación, te proporcionaré un manual paso a paso para crear un repositorio en GitHub:

### Paso 1: Crea una cuenta en GitHub
Si aún no tienes una cuenta en GitHub, ve a [GitHub](https://github.com/) y regístrate. sigue las instrucciones en el [paso1.md](Paso1.md)

### Paso 2: Inicia sesión en tu cuenta
Una vez que tengas una cuenta, inicia sesión en GitHub con tus credenciales.

### Paso 3: Accede a tu panel de control
Después de iniciar sesión, serás dirigido a tu panel de control. Si no es así, haz clic en tu avatar en la esquina superior derecha y selecciona "Your repositories" para acceder al panel.

### Paso 4: Crea un nuevo repositorio
En tu panel de control, busca y haz clic en el botón "New" (Nuevo) ubicado en la esquina superior derecha.

### Paso 5: Completa la información del repositorio
Llena la información requerida para tu nuevo repositorio:

- **Repository name**: Elige un nombre para tu repositorio.
- **Description**: Proporciona una breve descripción de tu proyecto.
- **Public or Private**: Decide si deseas que tu repositorio sea público (visible para todos) o privado (acceso restringido).
- **Initialize this repository with a README**: Puedes seleccionar esta opción si deseas crear un archivo README. Un README es útil para proporcionar información sobre tu proyecto.

### Paso 6: Opciones adicionales
Puedes agregar un archivo de licencia (como LICENSE) y un archivo de ignorar (como .gitignore) si lo deseas. Estos archivos son opcionales pero pueden ser útiles para organizar tu proyecto.

### Paso 7: Crea el repositorio
Haz clic en el botón "Create repository" (Crear repositorio) cuando hayas completado todos los detalles.

### Paso 8: Clona el repositorio 
Si deseas trabajar en tu repositorio desde tu máquina local, puedes clonarlo usando el comando `git clone` en tu terminal. El enlace para clonar estará disponible en la página de tu repositorio en GitHub.

Haz click en Code (Codigo) y selecciona la opcion ssh y copia la dirrecion

Reemplaza  <git@github.com:nombre_usuario/nombre_repositorio.git> con la dirrecion copiada en el paso anterior


## Paso 9: Verificar la conexión
Para verificar que todo está configurado correctamente, intenta realizar un cambio y enviarlo de vuelta al repositorio:

Dentro de cloud9 crea un archivo con el nombre README.md en la carpeta de tu repositorio
Agrega el texto "Hola este mis proyecto de CICD" guarda el archivo


```
git add README.md
git commit -m "Añadir archivo hola.txt"
git push origin master
```
Si todo está configurado correctamente, este cambio se enviará a tu repositorio en GitHub.

¡Listo! Ahora has clonado un repositorio en GitHub utilizando SSH y has configurado la autenticación mediante claves SSH.
