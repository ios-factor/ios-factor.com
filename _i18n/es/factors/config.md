La configuración de una aplicación es lo que cambia con mayor probabilidad entre despliegues (App Store, TestFlight, desarrollo local) o también a través del tiempo sin cambios subyacentes en el código. Esto incluye:

- Claves de acceso de la API a los servicios back-end (tanto servicios internos como externos)
- Enlaces a recursos remotos (otras APIs utilizadas dentro de la aplicación)
- Activar/Desactivar características (_Feature toggles_)

Algunas veces las aplicaciones almacenan configuración en forma de constantes dentro del código. Esto es una violación a este factor iOS, el cual indica que **debe haber una separación estricta entre la configuración y el código**. La configuración varía sustancialmente a través de los despliegues, el código por su parte no.

La prueba de fuego para saber si una aplicación tiene toda su configuración completamente por fuera del código consiste en la posibilidad de publicar el código fuente como código abierto en cualquier momento, sin comprometer ninguna credencial.

Existen varias maneras de inyectar valores a la configuración en tiempo de compilación:

- Archivos de configuración (ej. JSON o YAML)
- [cocoapods-keys](https://github.com/orta/cocoapods-keys) para ocultar de manera adecuada las claves existentes e inyectarlas a una aplicación iOS durante la etapa de compilación
- Soluciones personalizadas pre-fabricadas (ej. utilizar una _build phase_ en Xcode)

Dado que los despliegues en la plataforma iOS son significativamente más lentos que los despliegues en servidor, se podría considerar una alternativa _Over-the-Air (OTA)_ para actualizar la configuración de manera ágil y reaccionar rapidamente a los inconvenientes.

Las actualizaciones en configuración _OTA_ son extremadamente útiles y permiten de manera instantanea:

- Correr tests A/B para habilitar ciertas características o cambios en la interfaz gráfica sólo para un grupo específico de usuarios activos.
- Rotación de claves de la API.
- Actualizar dominios web u otros enlaces que han cambiado.
- Deshabilitar características u ocultar botones de manera remota.

Sin actualizaciones _Over-the-Air_ es necesario esperar alrededor de un dia para que la aplicación sea aceptada en la revisión. Cada entrega incrementa además el riesgo de que la aplicación sea rechazada y una posible publicación urgente se vea retrasada.

Al mismo tiempo, se desea tener compatibilidad retroactiva, es decir, los usuarios que no pueden actualizar el sistema operativo a la versión más actual de iOS tampoco deberían poder volver a actualizar la aplicación. Al proporcionar actualizaciones _OTA_ se puede seguir brindando soporte a versiones viejas de la aplicación.

Algunos posibles acercamientos a la implementación de actualizaciones _Over-the-Air_:

- Implementar una solución propia.
- Servicios web registrados como [Configuración Remota con Firebase](https://firebase.google.com/docs/remote-config/).
