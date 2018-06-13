**Os números de versão e de build trabalham juntos para unicamente identificar um envio de um aplicativo para a App Store**

- Número da versão (`CFBundleShortVersionString`) - mostrado como `Version` no Xcode, também chamado de versão de mercado (ou _marketing version_): A versão que é visível para o usuário final, precisa ser incrementada a cada lançamento público na App Store
- Número do build (`CFBundleVersion`) - mostrado como `Build` no Xcode: um número incremental

Nos processos atuais de desenvolvimento para iOS, não existe motivo para que você altere esses números manualmente. Ao invés disso, você quer um sistema confiável e automatizado que seja responsável por manter esses números de versão atualizados.

Não existe necessidade para usar ferramentas de terceiros. O Xcode tem uma ferramenta chamada `agvtool` já embutida. ([mais detalhes](https://developer.apple.com/library/content/qa/qa1827/_index.html))

Após já ter habilitado o Sistema de Versionamento (ou `Versioning System`) no seu projeto do Xcode, você pode usar os seguintes comandos:

```sh
# Atualizar o número da versão (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# Atualizar o número do build (CFBundleVersion) para o próximo
agvtool next-version -all
```

Se você usa a ferramenta de distribuição [fastlane](https://fastlane.tools), pode usar as instruções [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) e [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/) para automatizar o passo de incremento de versão do seu processo de distribuição.

Exemplo de `Fastfile`:

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
