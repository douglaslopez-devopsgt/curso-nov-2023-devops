Agregar pruebas unitarias a una aplicación Spring Boot es una excelente práctica para garantizar la calidad del código y facilitar la detección temprana de posibles problemas. A continuación, te proporcionaré un manual básico sobre cómo agregar pruebas unitarias a una aplicación Spring Boot utilizando JUnit y Mockito.

### Paso 0: Crea tu branch de trabajo

Crea una nueva branch con tu trabajo corriendo este comandos

```
git checkout -b feature/agregar-tests
```

### Paso 1: Configuración del Proyecto

Asegúrate de que tu proyecto Spring Boot tenga las dependencias adecuadas en tu archivo `pom.xml` para JUnit y Mockito. Puedes agregar estas dependencias:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

### Paso 2: Crear Clases de Pruebas

**Agregar un contolodar rest**

   crear en el folder `/src/main/java/com/example/demo` el archivo DemoController con el siguiente contenido:

   ```java
package com.example.demo;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @RequestMapping("/")
    String hello() {
        return "Hello World";
    }

}

   ```

**Prueba de Controladores:**

   crear en el folder `src/test/java/com/example/demo` el archivo DemoApplicationTests.java con el siguiente contenido:

   ```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

import static org.hamcrest.Matchers.equalTo;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;


@SpringBootTest
@AutoConfigureMockMvc
public class DemoApplicationTests {

    @Autowired
    private MockMvc mvc;

    @Test
    public void welcome_ok() throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("Hello World, Spring Boot!")));
    }

}

   ```
   
### Paso 3: Crear el workflow de pruebas
   
Crear un flujo de GitHub Actions para ejecutar los tests de un proyecto Maven y fallar si alguna prueba no pasa es bastante sencillo. A continuación, te proporcionaré un ejemplo básico de un archivo YAML para lograr esto.

1. En tu repositorio de GitHub, crea un archivo llamado `.github/workflows/tests.yml` y agrega el siguiente contenido:

```yaml
name: Maven Build and Test

on:
  push:
    branches:
      - 'releases/**'

jobs:
  tests:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up JDK 17
      uses: actions/setup-java@v3
      with:
        java-version: 17
        distribution: 'corretto'
        cache: maven

    - name: Build with Maven
      run: mvn -B clean verify

    - name: Check Test Results
      run: |
        if [ -f target/surefire-reports/*.xml ]; then
          echo "Test results found."
        else
          echo "No test results found. Failing the build."
          exit 1
        fi
```

Este archivo YAML define un flujo de trabajo que se ejecuta en cada push y pull request. Utiliza Maven para limpiar y construir el proyecto, y luego verifica si se generaron informes de pruebas (surefire-reports). Si no se encuentran informes de pruebas, el flujo de trabajo fallará.

### Paso 4: Configuracion de reporte

Asegúrate de que tu proyecto Maven tenga el plugin Surefire configurado en el `pom.xml`. Debería verse algo así:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
            <configuration>
                <!-- Configuración adicional si es necesario -->
            </configuration>
        </plugin>
    </plugins>
</build>
```

### Paso 5: Actualiza tus cambios

 Haz un commit y un push de tu archivo YAML en el paso 1 a tu repositorio de GitHub.

Ahora, cada vez que realices un push o abres un pull request, GitHub Actions ejecutará automáticamente este flujo de trabajo. Si algún test falla, el flujo de trabajo también fallará. 


