**Idealmente, una aplicación iOS-factor nunca depende de la existencia implicita de paquetes globales del sistema.** Se deben declarar todas las dependencias, completamente y de manera precisa a través de un manifesto de declaración de dependencias. Éste debe incluir las versiones exactas de [Xcode](https://developer.apple.com/xcode), [CocoaPods](https://cocoapods.org) y [fastlane](https://fastlane.tools).

El principal beneficio de la declaración explicita de dependencias es la simplificación de la configuración por parte de programadores nuevos en la aplicación, además de contar con un sistema de compilación confiable que es capaz de correr versiones anteriores de forma reproducible. Un nuevo desarrollador podría descargar el código fuente en su máquina y solo necesitaría instalados el lenguaje de ejecución y el gestor de dependencias como pre-requisitos. Éstos estarán en capacidad de generar el entorno adecuado para correr el código de la aplicación a través de un comando de compilación determinado.

**Al especificar las dependencias exactas se puede re-lanzar una versión que tiene 6 meses de antigüedad, teniendo la certeza de una compilación exitosa** ya que se hace uso de las mismas versiones de Xcode, CocoaPods y Swift.

Dado que el desarrollo iOS no puede ser encapsulado en contenedores como es el caso del desarrollo web, estamos limitados a herramientas externas que tratan de satisfacer este requerimiento hasta que Apple provea una solución oficial ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)).

Por ahora, se puede hacer uso de varias herramientas de terceros para declarar explicitamente esas dependencias.

#### Herramientas basadas en Swift

Apple proporciona una excelente guia del [Swift Package Manager](https://swift.org/package-manager).

#### Especificación de la versión de Xcode

Se puede utilizar un archivo de versionamiento de Xcode ([.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) file) en la raiz del proyecto para definir la versión exacta que debe ser usada para cierta aplicación iOS.

De esta manera se puede configurar un sistema de integración continua (_CI-system_) para la instalación y utilización automática de una versión dada de Xcode. Si se desea cambiar la versión de Xcode (asumiendo que ya se tenga instalada), se puede utilizar una herramienta como [chxcode](https://github.com/klaaspieter/chxcode).

Para automatizar la instalación de Xcode, se puede usar la herramienta externa [xcode-install](https://github.com/krausefx/xcode-install) hasta que Apple proporcione una herramienta  propia que mediante linea de comandos permita la instalación de Xcode ([rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480)).

#### Herramientas basadas en Ruby

Ruby utiliza [bundler](https://bundler.io) para definir de manera exacta las dependencias a ser usadas en cierta compilación en el llamado `Gemfile`:

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

El archivo `Gemfile` y el archivo generado de manera automatica `Gemfile.lock` deben ser persistidos en el control de versiones. Cualquier sistema puede entonces correr `bundle install` para instalar todas las dependencias que Ruby requiere.

#### Herramientas basadas en JavaScript

Las aplicaciones iOS basadas en JavaScript (ej. React Native) hacen uso del archivo `package.json`, el cual define todas las dependencias necesarias.

```json
{
  ...
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start",
    "test": "jest"
  },
  "dependencies": {
    "react": "15.4.2",
    "react-native": "0.42.3",
    ...
  }
}
```

El archivo `package.json` debe ser agregado en el control de versiones para reproducir dichas compilaciones.
