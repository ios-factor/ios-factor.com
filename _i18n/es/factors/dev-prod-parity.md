Historicamente, han habido brechas sustanciales entre el ambiente de desarrollo (donde un desarrollador hace modificaciones en tiempo real a la aplicación en su máquina local) y producción (donde los usuarios finales pueden acceder a la aplicación ya desplegada en el App Store). Estas brechas se manifiestan en 3 vacíos:

- **La brecha temporal:** Un desarrollador podría trabajar en código que puede tomar días, semanas o incluso meses para salir a producción.
- **La brecha de personal:** Todos los desarrolladores iOS escriben código, más sólo una persona sabe cómo desplegar la aplicación.
- **La brecha en herramientas:** Los desarrolladores podrían estar usando un servidor de staging que corre una versión diferente a la existente en el servidor productivo. También podrían usar versiones diferentes de Xcode a la usada para programar

**Una aplicación factor-iOS está diseñada para el [despliegue continuo](https://avc.com/2011/02/continuous-deployment/) al mantener la brecha entre el ambiente de desarrollo y el productivo lo más pequeña posible.** Observando los 3 vacíos mencionados anteriormente se debe considerar:

- Acortar la brecha temporal: un desarrollador podría escribir código y desplegarlo tan solo unos pocos días despues
- Reducir la brecha de personal: los desarrolladores que escriben código deben estar involucrados de cerca en su despliegue y comportamiento en producción. Ésto se hace posible en mayor medida al automatizar completamente el proceso de publicación de la aplicación iOS y plasmar el conocimiento fundamental (_know-how_) de la automatización en declaraciones de código en vez de documentación.
- Reducir la brecha en herramientas: mantener los ambientes de desarrollo y producción tan similares como sea posible. Seguir los principios de el factor de [Dependencias](/es/dependencies) haciendo uso de un archivo `.xcode-version` y definiendo el resto de dependencias de manera explicita.

Resumiendo lo anterior en una tabla:

|          | Aplicaciones iOS tradicionales | Aplicación factor-iOS |
|----------|--------------------------------|-----------------------|
| Tiempo entre despliegues | Meses  | Días           |
| Autor del código vs publicadores del código | Sólo una persona sabe como desplegar | El despliegue está automatizado, idealmente en un servidor |
| Ambientes de desarrollo vs producción | Divergentes |  Tan similares como sea posible |
