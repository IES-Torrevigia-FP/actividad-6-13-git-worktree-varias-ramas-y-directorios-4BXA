# Reflexión sobre git worktree

1. Explica con tus palabras qué ventaja tienen los worktrees frente a:
- Cambiar de rama en el mismo directorio: La mayor ventaja es no tener que hacer `stash` o `commit` de cambios temporales antes de cambiar de contexto. Tienes ambos contextos de trabajo y los archivos en disco separados e intactos en carpetas distintas simultáneamente.
- Clonar el repositorio varias veces: La ventaja principal es que ambos directorios comparten el mismo directorio `.git` subyacente. Con esto evitas tener que descargar la historia completa dos veces y ahorras gran cantidad de espacio en el disco; además, las ramas locales siempre están sincronizadas sin hacer fetch.

2. Describe dos situaciones reales donde usarías `git worktree`:
- Situación A: Estás desarrollando una funcionalidad compleja y larga. De pronto, un compañero te pide revisar su Pull Request (PR) o hay un fallo crítico (hotfix) en `main` que debes solucionar rápidamente. Para no interrumpir tu trabajo en curso ni mezclar archivos compilados, abres un worktree en una carpeta separada, arreglas el fallo o revisas la PR y, cuando acabas, borras esa carpeta y retomas tu tarea principal donde la dejaste.
- Situación B: Quieres hacer una refactorización de código y deseas arrancar simultáneamente el servidor web con la rama actual (por ejemplo en el puerto 3000) y el servidor web con tu nueva rama de refactorización (en el puerto 3001) para comparar visualmente que el comportamiento de ambas aplicaciones es exactamente el mismo antes de dar por buena la tarea.

3. ¿Qué buenas prácticas seguirías para nombrar y organizar los directorios de worktrees?
Utilizar prefijos claros en las carpetas para identificarlas a simple vista, como por ejemplo `wt-` o `worktree-`, seguido del nombre de la rama en cuestión (ej. `wt-feature-login`). Además, es una buena práctica borrarlos tan pronto como ya no hagan falta usando `git worktree remove` para no acumular directorios inútiles, y colocar esos directorios justo al mismo nivel que la carpeta principal o en una carpeta de worktrees dedicada fuera del repositorio principal.
