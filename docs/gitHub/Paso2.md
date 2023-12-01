Para agregar una llave SSH desde tu cuenta personal de GitHub a una instancia de Amazon Linux, sigue estos pasos:

### Paso 1: Generar una nueva llave SSH en la terminal de cloud9

Si aún no tienes una llave SSH, puedes generar una usando el siguiente comando en tu terminal local. Asegúrate de reemplazar el correo electrónico con el que te registraste en GitHub.

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@ejemplo.com"
```

Este comando generará una nueva llave SSH y te pedirá que ingreses una ubicación para guardarla. La ubicación predeterminada suele ser `~/.ssh/id_rsa`. Puedes presionar Enter para aceptar la ubicación predeterminada.

### Paso 2: Agregar la llave SSH a ssh-agent

Si no tienes el agente SSH en funcionamiento, puedes agregar la llave SSH recién generada usando el siguiente comando:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### Paso 3: Copiar la llave SSH al portapapeles

Utiliza el siguiente comando para mostrar tu llave pública y copiala al portapapeles:

```bash
cat  ~/.ssh/id_rsa.pub
```


### Paso 4: Agregar la llave SSH a tu cuenta de GitHub

1. Inicia sesión en tu cuenta de GitHub.
2. Haz clic en tu avatar en la esquina superior derecha y selecciona "Settings" (Configuración).
3. En el menú de la izquierda, haz clic en "SSH and GPG keys" (Claves SSH y GPG).
4. Haz clic en "New SSH key" (Nueva clave SSH).
5. En el campo "Title" (Título), agrega un nombre descriptivo para la nueva clave.
6. En el campo "Key" (Clave), pega la llave SSH que copiaste anteriormente.
7. Haz clic en "Add SSH key" (Agregar clave SSH).


¡Eso es todo! Ahora deberías poder autenticarte en tu instancia de Amazon Cloud9 utilizando tu llave SSH asociada con tu cuenta de GitHub.