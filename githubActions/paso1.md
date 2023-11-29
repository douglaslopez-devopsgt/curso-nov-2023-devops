Eneste paso  crearemos un GitHub Action. Los GitHub Actions son flujos de trabajo automatizados que puedes configurar directamente en tu repositorio de GitHub. En este ejemplo, crearemos un flujo de trabajo simple que se ejecutará cada vez que se realice un push en la rama `master` y mostrará un mensaje en la consola.

### Paso 1: Crear un archivo de flujo de trabajo

En tu repositorio de GitHub, crea un directorio llamado `.github/workflows` si no existe. Luego, dentro de ese directorio, crea un archivo YAML que describa tu flujo de trabajo. Por ejemplo, `master.yml`.

```yaml
name: Mi Primer GitHub Action

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout código
      uses: actions/checkout@v2

    - name: Mostrar mensaje
      run: echo "¡Hola, este es mi primer GitHub Action!"
```

Este flujo de trabajo se ejecutará cada vez que se realice un push en la rama `master`.

### Paso 2: Cometer y hacer push

Agrega y haz commit del nuevo archivo `.github/workflows/master.yml` en tu repositorio.

```bash
git add .github/workflows/master.yml
git commit -m "Añadir GitHub Action básico"
git push origin master
```

### Paso 3: Verificar el flujo de trabajo en GitHub

Visita la sección "Actions" de tu repositorio en GitHub. Deberías ver tu nuevo flujo de trabajo en ejecución o completado. Puedes hacer clic en los detalles para ver la salida de cada paso.

Este es un ejemplo muy básico, pero los flujos de trabajo de GitHub Actions son extremadamente flexibles y puedes hacer cosas más avanzadas, como ejecutar pruebas, implementar en servidores, notificar en Discord, entre muchas otras opciones.

Personaliza el archivo YAML según tus necesidades y revisa la [documentación oficial de GitHub Actions](https://docs.github.com/en/actions) para obtener más detalles sobre cómo aprovechar al máximo esta potente herramienta de automatización.