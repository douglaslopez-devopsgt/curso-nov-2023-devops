### Cómo Crear una Pull Request en GitHub Usando Gitflow


#### 1. **Inicializar Gitflow:**
   - Navega al directorio del repositorio clonado en tu máquina local.
     ```bash
     cd repositorio
     ```
   - Inicializa Gitflow en tu repositorio.
     ```bash
     git flow init
     ```

#### 4. **Iniciar una Feature con Gitflow:**
   - Crea una nueva rama de feature utilizando Gitflow.
     ```bash
     git flow feature start nombre-de-la-funcion
     ```

#### 5. **Realizar Cambios:**
   - Agrega el codigo ejemplo con el siguiente comando
   ```
   aws s3 sync s3://devops-gt-nov2023-lab/codigo_ejemplo/ .
   ```

#### 6. **Hacer Commit de los Cambios:**
   - Añade los cambios al área de preparación.
     ```bash
     git add .
     ```
   - Realiza el commit de los cambios con un mensaje descriptivo.
     ```bash
     git commit -m "Agregar función o corregir error"
     ```

#### 7. **Terminar la Feature con Gitflow:**
   - Finaliza la rama de feature.
     ```bash
     git flow feature finish nombre-de-la-funcion
     ```

#### 8. **Subir Cambios a tu repositorio**
   - Sube tus cambios a tu repositorio fork.
     ```bash
     git push origin develop
     ```

#### 9. **Crear una Pull Request:**
   - Cambia a la rama `develop` que acabas de subir.
   - Haz clic en el botón "New Pull Request".
   - Selecciona el repositorio base y la rama base y la rama `develop``.
   - Revisa tus cambios y proporciona un título y una descripción significativos.
   - Haz clic en el botón "Create Pull Request".

#### 10. **Discutir y Revisar:**
   - Participa en discusiones con los mantenedores y colaboradores en tu pull request.
   - Realiza los cambios necesarios según los comentarios recibidos.

#### 11. **Fusionar la Pull Request:**
   - Una vez que tu pull request sea aprobada, el mantenedor del repositorio puede fusionarlo.
   - Si hay conflictos de fusión, resuélvelos localmente, realiza un commit con los cambios y vuelve a subirlos.

#### 12. **Eliminar tu Rama de Función (Opcional):**
   - Después de que tu pull request se haya fusionado, puedes eliminar la rama de feature.
     ```bash
     git branch -d nombre-de-la-funcion
     ```

¡Felicidades! Has creado con éxito una pull request utilizando Gitflow. Recuerda que Gitflow es una metodología flexible, y cada proyecto puede tener sus propias prácticas y configuraciones específicas. Asegúrate de revisar la documentación del proyecto para cualquier requisito o proceso adicional.