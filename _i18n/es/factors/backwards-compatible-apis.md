Mientras la mayoría de usuarios finales actualizan a la versión más reciente al cabo de unas pocas semanas, siempre habrá un grupo de usuarios que no lo harán, esto debido a múltiples razones. A menudo está relacionado a la versión de iOS que estén corriendo, ya que la actualización del sistema operativo puede depender de la antigüedad de dicho dispositivo.

Se puede instalar y hacer uso de Facebook Messenger en un iPad primera generación (2010). Si bien las más recientes características no son compatibles, el núcleo de funcionalidades estará disponible gracias al versionamiento de la API.

El concepto básico consiste en no actualizar una API existente, sino añadir una nueva y permitir el funcionamiento de ambas de manera simultanea.

```
https://your-api.com/1.0/drivers.json
https://your-api.com/1.1/drivers.json
```

Eventualmente hay que desactivar o cambiar ligeramente la semántica de una API. Aún cuando una empresa está completamente comprometida a la estabilidad, hay razones de fuerza mayor que obligan a este tipo de cambios de vez en cuando. Por lo tanto, se debería exponer un punto de acceso (endpoint) en el cual se pueda consultar el estado de una versión de la API.

```
https://your-api.com/1.0/status.json
https://your-api.com/1.1/status.json
```


El estado de la API debería incluir información tal como:

 - Cuál es el ambiente de la API? (ej. pruebas, beta, producción)
 - Está la API obsoleta (deprecated)? Si es así, en que fecha está programada su desactivación?
 - Está la API dada de baja / desactivada (offline)? Dado el caso, permanecerá así o se trata de una desactivación temporal?
