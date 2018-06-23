Como fue descrito en el factor de [Dependencias](/es/dependencies), el repositorio de código debería incluir todas las dependencias necesarias para la compilación, pruebas y distribución de la aplicación iOS.

Tan pronto como la aplicación cumpla con este requerimiento, se pueden publicar nuevas actualizaciones de ésta desde **cualquier** ordenador basado en macOS.

En un mundo ideal, publicar una actualización de la aplicación requeriría:

- crear un proyecto completamente vacío, un contenedor temporal
- instalar automaticamente todas las dependencias (ej. Xcode y [CocoaPods](https://cocoapods.org))
- correr el script de despliegue (ej. [fastlane](https://fastlane.tools))

Desafortunadamente, dado el hecho que Xcode tiene que correr sobre macOS, no podemos utilizar esta variante ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)). Además el uso de macOS en un ambiente virtual trae consigo desafíos tanto técnicos como legales. No obstante, existe una solución comercial (software privativo o _closed source_) externa llamada [Veertu](https://veertu.com/) que permite generar maquinas virtuales macOS en hardware de Apple.

En los últimos años, los contenedores desechables han ganado popularidad por una variedad de razones:

- compilaciones totalmente reproducibles sin ninguna dependencia hacia el sistema operativo anfitrión original
- corre en cualquier máquina (ordenador local o cualquier servidor en la nube)
- un archivo compilado totalmente limpio con sólo las dependencias necesarias

Actualmente, el mejor camino que podemos tomar como programadores iOS es:

- Automatizar la instalación de Xcode usando [xcode-install](https://github.com/krausefx/xcode-install).
- Hacer uso de un [archivo .xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) para especificar la versión exacta de Xcode.
- Definir todas las dependencias en archivos de configuración (véase el factor de [Dependencias](/es/dependencies)).
- Automatizar todo el proceso de despliegue usando herramientas de despliegue como por ejemplo [fastlane](https://fastlane.tools).
- Automatizar el firmado de código (ej. [codesigning.guide](https://codesigning.guide)).
- Desplegar frecuentemente, preferiblemente cada semana.

Muchas empresas hacen uso del concepto `Tren de releases (Release Train)`: Un horario en el cual una nueva versión de la aplicación es liberada. En el momento que el tren de releases "parte", todo el código que ha sido incorporado en la rama principal (ej. `master` o `release`) será liberado al App Store. Esta variante es implementada por la mayoria de aplicaciones iOS de gran envergadura.
