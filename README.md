# H8 Software: Metodologías de trabajo
En este documento voy a definir una serie de buenas prácticas y metodologías de trabajo que nos permitirán ahorrar tiempo en el desarrollo, mejorar la comunicación y el conocimiento obicuo dentro del equipo y facilitar el trabajo para todos. Si bien puede ser un poco engorroso o aturullante al principio, es de vital importancia que todos tengamos sigamos estas metodologías (os servirá profesionalmente si eso os motiva más).

<details open>
<summary><b>Índice</b></summary>

- [Introducción](#h8-software-metodologías-de-trabajo)
- [Control de versiones](#flujo-de-trabajo-para-el-control-de-versión)
- [Pull requests](#pull-requests)
- [Flujo de trabajo con Jira](#flujo-de-trabajo-con-jira)


</details>

## Flujo de trabajo para el control de versión
El estándar de flujo de trabajo más utilizado en el mundo empresarial es Git Flow (aunque hay más). El concepto es bastante sencillo: 

Tenemos una rama principal, ***master***, que es la que contiene la versión del código que se encuentra en producción, es decir, la versión que utiliza el usuario final. Esta rama no se debe tocar durante el desarrollo, solo para subir una nueva versión a producción (o para arreglar un error urgente en producción, pero esto es improbable que nos pase porque no tenemos un entorno de producción al uso). 

Luego, tenemos otra rama, ***develop***, que contiene el código que se está utilizando en el entorno de desarrollo, donde se prueba las nuevas versiones de la aplicación antes de subirlo a producción. 

Luego, están las ramas ***features***, que es donde se encuentra la salsa de esta metodología. Básicamente, cada vez que queremos desarrollar una nueva funcionalidad, creamos una nueva rama desde develop (esto es importante, se saca desde develop, no desde de master, porque en develop es donde están la última versión). Esta rama debe corresponder a una única tarea (no se pueden realizar mas de una tarea en la misma rama, aunque si se puede dividir una tarea en varias ramas feature). Los nombres de estas ramas deben corresponder con los identificadores de la tarea a la que pertenecen, por ejemplo, imaginemos que tengo que implementar esta tarea: `T-53: Implementar universal tag`, lo que haría sería lo siguiente:

1. Me sitúo en la rama develop y hago update, para traerme la última versión.
2. Creo una rama nueva desde develop con el nombre features/T-53.
3. Implemento lo que necesite, hago commits, etc.
4. Una vez que he terminado, hago push de la rama (hasta este momento el código se encuentra solo en local). Esto se puede ir haciendo mientras hacemos commits y desarrollamos, no necesariamente al final.
5. Una vez que he pusheado mi rama con la funcionalidad hecha, creo un Pull Request, para que los demás reviséis mi trabajo.
6. Una vez validado el PR (Pull Request), se hace merge de la rama con develop (otra vez, NO se toca master). En este punto, el código ya se encuentra en el entorno de desarrollo, listo para hacer pruebas a full antes de subir a producción.
7. Cuando se han agrupado unas cuantas funcionalidades en develop, se mergea a master, y aquí entra el maravilloso mundo del CI/CD.

Finalmente, están las ramas ***hotfix***, que básicamente se utilizan para arreglar bugs urgentes en producción (lo he mencionado antes). Estas ramas son un poco peculiares, porque no se sacan desde develop, si no que se hace desde master, esto es porque queremos arreglar un error de producción. Pero a la hora de mergearlo, se abren dos PRs, uno para mergear en master, y otro para mergear en develop (para que la versión de master y de devel cuadren).

Hay empresas que utilizan otra rama intermedia entre master y develop, que se llama ***release***, que se utiliza, como su nombre indica, para hacer releases de versiones antes de subirlas a master, pero para nosotros no merece la pena utilizarlas.

![](Docu/gitglow.png)

## Pull requests
Los PRs son solicitudes que se hacen para mergear una rama en otra. Cuando se ha terminado una funcionalidad y se ha pusheado la rama, se abre un PR. Ese PR tiene que tener un título específico con el siguiente formato: **[NO MERGE][PRNº] ID-Tarea Descripción**. El [NO MERGE] solo se pone si ese PR no se puede mergear por algún motivo, pero quieres que el resto del equipo lo vaya validando. El [PRNº] se pone en caso de que una tarea sea muy grande y se haya divido en varios PRs. Por ejemplo: **T-53 Implement universal tag**, **[PR1] T-54 Create endpoint for can matrix**, **[PR2] T-54 Implement CanMatrixRetriever**, **[NO MERGE] T-124 Implement night mode**.

Los PRs no se pueden mergear hasta que se hayan validado por todos los miembros del equipo, esto permite que todos estemos enterados del código que se está implementando aunque no sea nuestra tarea, y hace que las dailys sean más rápidas. Si se encuentra un error o un posible problema, se escribe un comentario en el PR y se marca como revisión.

### Crear PR
Para crear un PR se puede hacer desde GitHub Web o desde la aplicación de escritorio de GitHub. Yo lo suelo hacer desde la GH Desktop, pero esto va a gustos.

![GitHub Desktop](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.30.54.png)

![GitHub Web](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.31.25.png)

Cuando se abre un PR, hay que poner el título siguiendo el formato que he mencionado anteriormente, un comentario si se desea (es recomendable subir capturas o algo que demuestre el funcionamiento de la feature) y, muy importante, añadir los miembros de equipo a los reviewers (creo que GH se puede configurar para que los reviewers aparezcan directamente).

![Abrir PR](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.35.25.png)

![Añadir reviewer](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.36.16.png)

![Reviewer](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.37.34.png)

Una vez hecho esto, se crea el PR y se espera a que los demás miembros lo validen. Lo que el reviewer tiene que hacer es entrar a GitHub Web y entrar a los PRs abiertos. Una vez hecho eso, se hace click en Añadir review

![Validar](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.39.43.png)

![Añadir](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.40.05.png)

Cuando se revise el PR, se acepta o se solicita la revisión

![Revisar](Docu/Captura%20de%20Pantalla%202022-09-09%20a%20las%2022.41.43.png)

Cuando todos los usuarios validan el PR, es la hora de mergearlo.


## Flujo de trabajo con Jira
Puede ser con Jira, Trello, Asana o herramientas similares. Estas aplicaciones sirven para mantener un flujo de trabajo ordenado y organizar las tareas dentro del equipo. 

Básicamente es un tablero kanban con varias columnas: **Pendiente**, **Bloqueado**, **En proceso**, **Pull Request** y **Terminado**. Las tareas que van surgiendo se van colocando en la columna Pendiente. Cuando una persona empieza una tarea, se la asigna a si mismo y la coloca en la columna En proceso. Ahora pueden pasar dos cosas, que la persona complete la tarea, en cuyo caso se movería a Pull Request mientras los PRs de la tarea están abiertos, o bien que la tarea no se pueda completar por cualquier motivo, en cuyo caso se mueve a la columna Bloqueado y se expone en un comentario el motivo por el cuál no se ha podido terminar.

Una vez todos los PR han sido validados y mergeados, y se haya testeado que se cumplen los requisitos de la tarea, esta puede pasarse a Terminado
