## Preguntas sobre Maven y GitHub

### a. ¿Qué es un arquetipo (Archetype) en Maven?
Un **Archetype** es una plantilla o modelo predefinido para la creación de proyectos. En términos simples, es un "molde" que genera la estructura de directorios, archivos de configuración (como el `pom.xml`) y clases iniciales necesarias para un tipo específico de aplicación, permitiendo que todos los proyectos sigan un estándar común desde el inicio.

### b. ¿Para qué sirve el arquetipo maven-archetype-quickstart?
Es el arquetipo más básico y común de Maven. Se utiliza para generar la estructura de una **aplicación Java simple (J2SE)**. Crea un proyecto con:
* Una carpeta de código fuente (`src/main/java`).
* Una carpeta de pruebas (`src/test/java`).
* Un archivo `pom.xml` básico con JUnit como dependencia de prueba.

### c. ¿Cuál es el comando con el cual se puede crear un proyecto basado en un arquetipo maven?
El comando principal es:
```bash
mvn archetype:generate
```

### d. ¿Qué es un pull request en GitHub?
Un Pull Request (PR) es una petición formal para fusionar cambios de una rama de trabajo hacia una rama principal (como main o develop). Es el eje central de la revisión de código, donde otros desarrolladores pueden comentar, sugerir mejoras y aprobar los cambios antes de que formen parte del código oficial.

### e. ¿Cómo se crea un pull request en GitHub?
Realiza los cambios en una rama local y súbelos al repositorio: git push origin nombre-de-tu-rama.

Ve a la página del repositorio en GitHub.com.

Haz clic en el botón verde "Compare & pull request" que aparecerá en la parte superior.

Describe tus cambios en el formulario y pulsa "Create pull request".

### f. ¿Cómo se aprueba un pull request en GitHub?
Abre el Pull Request específico.

Ve a la pestaña "Files changed" para revisar las diferencias.

Haz clic en el botón "Review changes".

Selecciona la opción "Approve" y escribe un comentario opcional.

Haz clic en "Submit review".

--

* Apache Software Foundation. (2024). Maven – Introduction to Archetypes. Recuperado de https://maven.apache.org/guides/introduction/introduction-to-archetypes.html

* GitHub Docs. (2024). About pull requests. Recuperado de https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests

* Sommerville, I. (2011). Software Engineering (9th ed.). Pearson Education.