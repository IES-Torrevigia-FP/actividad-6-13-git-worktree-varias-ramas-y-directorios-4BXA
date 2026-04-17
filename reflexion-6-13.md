# Reflexión 6.13 - Git Worktree

## 1. Ventajas de usar worktrees

- **Frente a cambiar de rama en el mismo directorio**: Cambiar de rama a menudo requiere hacer `stash` de los cambios en progreso o hacer un commit temporal para no perderlos, y a veces implica reconfigurar entornos. Con worktrees, puedes tener ambas ramas activas simultáneamente en directorios separados sin interferencias, lo que es mucho más limpio y rápido.
- **Frente a clonar el repositorio varias veces**: Clonar el repositorio consume más espacio en disco porque duplica todo el historial (`.git/`) y requiere descargar todo de nuevo. Además, los clones están desconectados; lo que guardes en uno no está disponible en el otro a menos que hagas push/pull. Un worktree comparte el mismo directorio `.git/`, por lo que todos los cambios locales y objetos están inmediatamente disponibles en todos los worktrees de forma muy eficiente.

## 2. Situaciones reales de uso

1. **Revisión urgente de un Pull Request (PR)**: Estás en medio de una tarea compleja en tu rama `feature-x` y un compañero te pide que revises su PR urgente. En lugar de hacer `stash` o comprometer tu trabajo, simplemente creas un worktree para la rama de su PR, la revisas, la pruebas en su propio directorio y, cuando terminas, eliminas el worktree y vuelves a tu tarea sin interrupciones.
2. **Aplicar un hotfix en producción**: Mientras estás desarrollando una nueva característica, reportan un bug crítico en la rama `main` de producción. Puedes abrir un worktree basado en `main`, crear una rama `hotfix`, solucionar el problema, subir los cambios y luego eliminar el worktree para seguir con tu característica original.

## 3. Buenas prácticas

- **Nombrar directorios claramente**: Utilizar prefijos como `wt-` o ponerlos todos bajo una carpeta específica (ej. `../worktrees/feature-x`) ayuda a distinguirlos fácilmente del directorio principal del repositorio.
- **Limpieza periódica**: Una vez finalizada la tarea que motivó crear el worktree, es recomendable usar `git worktree remove` para eliminarlo.
- **Ejecutar prune ocasionalmente**: Usar `git worktree prune` para asegurarse de que las referencias a worktrees borrados manualmente desaparezcan del `.git/`.
- **Ubicación de worktrees**: Crearlos fuera o al mismo nivel del repositorio principal (ej. `../wt-feature`) para no ensuciar el directorio principal.
