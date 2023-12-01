
Para crear un workflow con GitHub Actions que realice un build de una aplicación Java siguiendo Gitflow, puedes seguir estos pasos:

1. **Crea un Archivo de Workflow:**
   - En el directorio `.github/workflows` de tu repositorio, crea un nuevo archivo YAML. Puedes nombrarlo, por ejemplo, `build.yml`.

2. **Define el Flujo de Trabajo:**
   ```yaml
   name: Java Build

   on:
     push:
       branches:
         - develop

   jobs:
     build:
       name: gitflow-build
       runs-on: ubuntu-latest

       steps:
       - name: Checkout
         uses: actions/checkout@v3

       - name: Set up JDK 17
         uses: actions/setup-java@v3
         with:
          java-version: 17
          distribution: 'corretto'
          cache: maven

       - name: Build with Maven
         run: mvn clean package
   ```

   - Este flujo de trabajo se activará en cada push a la rama `develop`.
   - Utiliza Ubuntu como entorno de ejecución.
   - Configura Java 11 utilizando el setup-java action.
   - Realiza un checkout del repositorio.
   - Ejecuta el build con Maven.




Agregar pruebas a un proyecto Java Spring Boot con Maven implica utilizar bibliotecas y herramientas específicas para escribir y ejecutar pruebas unitarias y de integración. A continuación, te proporcionaré una guía básica para agregar pruebas a tu proyecto:

### 1. Dependencias Maven
Asegúrate de tener las dependencias adecuadas en tu archivo `pom.xml` para pruebas. Agrega las siguientes dependencias dentro de la sección `<dependencies>`:

```xml
<dependencies>
    <!-- Dependencias para pruebas unitarias -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <!-- Dependencias para pruebas de integración (opcional) -->
    <!-- Agrega las dependencias según sea necesario, por ejemplo: -->
    <!-- <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
        <scope>test</scope>
    </dependency> -->
</dependencies>
```

### 2. Estructura del Proyecto
Asegúrate de tener una estructura de proyecto que siga las convenciones de Spring Boot. Las clases principales deben estar en el paquete base (por ejemplo, `com.example.myapp`). Las clases de prueba deben estar en la misma estructura de paquetes en el directorio `src/test/java`.

### 3. Escribir Pruebas
Crea clases de prueba para tus componentes, servicios, controladores, etc. Usa las anotaciones proporcionadas por JUnit y Spring Boot para definir las pruebas y configurar el contexto de la aplicación:

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
public class MyControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testControllerEndpoint() throws Exception {
        mockMvc.perform(get("/your-endpoint"))
               .andExpect(status().isOk());
    }
}
```

### 4. Ejecutar Pruebas
Utiliza Maven para ejecutar tus pruebas. Puedes ejecutar todas las pruebas con el siguiente comando:

```bash
mvn test
```

### 5. Cobertura de Pruebas (Opcional)
Si deseas medir la cobertura de tus pruebas, puedes usar herramientas como JaCoCo. Agrega el siguiente complemento a tu sección de `<build>` en el archivo `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.7</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
                <execution>
                    <id>report</id>
                    <phase>prepare-package</phase>
                    <goals>
                        <goal>report</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

Ejecuta el siguiente comando para generar un informe de cobertura:

```bash
mvn clean verify
```

El informe estará disponible en `target/site/jacoco/index.html`.

¡Con estos pasos, deberías poder agregar y ejecutar pruebas en tu proyecto Java Spring Boot con Maven! Recuerda adaptar las pruebas según las necesidades específicas de tu aplicación.