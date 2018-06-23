Almacenar información y configuración de acuerdo a los lineamientos de Apple es crucial para el ciclo de vida de la aplicación, en particular cuando se refiere a la sincronización con iCloud, renovación del dispositivo telefónico y restauración de una copia de seguridad en el teléfono.

Asegurarse de seguir los lineamientos oficiales de Apple para [almacenamiento de información en iOS](https://developer.apple.com/icloud/documentation/data-storage/index.html):

- `Documents`: Usar este directorio para contenido generado por el usuario, para éste será generada copia de respaldo
- `Caches`: Usar este directorio para información que puede ser regenerada
- `tmp`: Usar este directorio para archivos temporales
- Hacer uso del atributo `no respaldar` (_do not back up_) en archivos

Jamás almacenar información confidencial del usuario (como contraseñas o sesiones de usuario) en estos directorios. En cambio hacer uso del _Keychain API_.

El _Keychain API_ ofrece control sobre cómo la información debe ser guarda en un dispositivo. Asegurarse de tener un buen entendimiento de cómo [diferentes atributos](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values) afectan el ciclo de vida de la aplicación.

Una pregunta frecuentemente pasada por alto que debería ser planteada: Cuando el usuario renueva su dispositivo iOS a uno más reciente, se debería también migrar la información (ej. inicio de sesión)?

Si se utiliza [`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly) esta información no será incluida en los respaldos de iCloud o iTunes, es decir, el usuario perderá los datos cuando cambie de dispositivo.
