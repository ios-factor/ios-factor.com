**La versión y el número de compilación trabajan juntos para identificar de manera única el despliegue de una aplicación en la App Store:**

- Versión (`CFBundleShortVersionString`) - visto como `Version` en Xcode, también conocido como _marketing version_: Es la versión visible al usuario final, ésta debe ser incrementada en cada publicación al App Store
- Número de compilación (`CFBundleVersion`) - visto simplemente como `Build` en Xcode: Es el número incremental a través del versionamiento tradicional de software (SemVer)

Hoy en dia en los procesos de desarrollo iOS, no hay razón alguna para manipular estos números manualmente. En cambio, se procura tener un sistema automatizado confiable que se encargue de mantener las versiones actualizadas.

No hay necesidad de usar herramientas externas, Xcode ya cuenta con una herramienta llamada `agvtool`. ([más detalles](https://developer.apple.com/library/content/qa/qa1827/_index.html))

Después de la habilitación inicial del sistema de versionamiento (`Versioning System`) en el proyecto de Xcode, se puedan utilizar los siguientes comandos:

```sh
# Actualizar la versión (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# Incrementar el número de compilación (CFBundleVersion)
agvtool next-version -all
```

Si se utiliza la herramienta de despliegue [fastlane](https://fastlane.tools) se pueden usar las acciones [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) e [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/) para automatizar el incremento de la versión como un paso más en el proceso de despliegue.

Ejemplo de `Fastfile`:

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
