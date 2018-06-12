**Idealmente, uma app iOS-factor nunca depende da existência implícita de pacotes a nível de sistema**. Ela declara todas dependências, completamente e exatamente através de um manifesto de declaração de dependências. Isso inclui as versões exatas do [Xcode](https://developer.apple.com/xcode), [CocoaPods](https://cocoapods.org) e [fastlane](https://fastlane.tools).

O benefício da declaração explícita de dependências é que isso simplifica a configuração inicial do app para novos desenvolvedores, assim como ajuda a ter um sistema de build confiável que também é capaz de executar builds antigos novamente de uma forma que seja reproduzível. Um novo desenvolvedor pode baixar o código fonte da app na sua máquina, tendo somente o _runtime_ da linguagem e o gerenciador de dependências instalados como os únicos pré-requisitos.

**Ao especificar as dependências exatas, você consegue regerar um build de 6 meses atrás, sabendo que vai dar certo** dado que vai usar a mesma versão do Xcode, CocoaPods e do Swift.

Dado que o desenvolvimento pra iOS não consegue ser tão encapsulável como é o caso do desenvolvimento para web, estamos limitados à ferramentas de terceiros pra preencher essa necessidade enquanto a Apple não disponibiliza uma solução oficial ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)).

Por enquanto, você pode usar variadas ferramentas de terceiros pra declarar explicitamente essas dependências.

#### Ferramentas para Swift

A Apple fornece um guia excelente sobre o [Swift Package Manager](https://swift.org/package-manager).

#### Especificando uma versão do Xcode

Você pode usar um arquivo [.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) na raiz do seu projeto iOS para declarar a versão exata do Xcode a ser usada para uma dada app iOS.

Dessa forma, você pode configurar seu sistema de integração contínua para instalar automaticamente e usar uma determinada versão do Xcode. Para trocar a versão do Xcode (assumindo que você já o tem instalado), você pode usar uma ferramenta como o [chxcode](https://github.com/klaaspieter/chxcode).

Para automatizar a versão do Xcode, você pode usar uma ferramenta chamada [xcode-install](https://github.com/krausefx/xcode-install) até a Apple fornecer uma ferramenta de linha de comando para instalar o Xcode ([rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480)).

#### Ferramentas para Ruby

Ruby usa o [bundler](https://bundler.io) para definir as dependências exatas a serem usadas em um build através de um arquivo chamado `Gemfile`:

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

O `Gemfile` e o automaticamente gerado `Gemfile.lock` devem ser versionados na sua ferramenta de controle de versão. Qualquer sistema de build pode então ser capaz de rodar `bundle install` e instalar as dependências em Ruby.

#### Ferramentas para JavaScript

Apps iOS feitas em JavaScipt (ex: React Native) fazem uso de um arquivo chamado `package.json` que define todas as dependências necessárias.

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

O `package.json` deve ser versionado para que se tenha builds reproduzíveis.