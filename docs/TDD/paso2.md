Para automatizar la creación de una pull request a la rama `develop` cuando el trabajo (job) de prueba (test) es exitoso, puedes utilizar GitHub Actions y la funcionalidad de acciones condicionales. A continuación, te proporcionaré un ejemplo básico de un archivo YAML para lograr esto:

1. En tu repositorio de GitHub, modifica el  archivo llamado `.github/workflows/test.yml` y agrega el siguiente contenido al final:

```yaml


  merge:
    needs: tests
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.event_name != 'pull_request' && github.ref == 'refs/heads/main' && success()

    steps:
    - name: Checkout code
      uses: actions/checkout@v2
      
    - name: Install GitHub CLI
      run: |
        sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key C99B11DEB97541F0
        sudo apt-add-repository https://cli.github.com/packages
        sudo apt-get update
        sudo apt-get install gh

    - name: Set up Git
      run: |
        git config --global user.email "actions@github.com"
        git config --global user.name "GitHub Actions"

    - name: Create Pull Request
      run: |
        git checkout -b auto-merge-branch
        git push origin auto-merge-branch
        gh pr create --base develop --head auto-merge-branch --title "Auto Merge to Develop" --body "Auto-generated pull request from successful tests."
```

Este archivo YAML define dos trabajos (jobs) en un flujo de trabajo. El primero (`test`) ejecuta las pruebas de tu proyecto Maven. El segundo (`merge`) crea una pull request a la rama `develop` si el trabajo de prueba fue exitoso.


2. Crea tu PR y haz merge de tu trabajo