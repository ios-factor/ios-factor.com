Como descrito no fator [Dependências](/dependencies), o repositório do código deve incluir todas as dependências que são necessárias para fazer o build, testar e submeter a app iOS.

Assim que sua app preencher esse requisito, você pode lançar novas atualizações da app de **qualquer** máquina que rode macOS.

Num mundo ideal, para lançar uma atualização de uma app, você:

- criaria um container temporário, completamente vazio
- automaticamente instalaria todas dependências (ex: Xcode e [CocoaPods](https://cocoapods.org))
- rodaria o script de deploy (ex: [fastlane](https://fastlane.tools))

Infelizmente, devido ao fato que o Xcode precisa rodar no macOS e virtualização de macOS implica em desafios técnicos e até mesmo legais, não podemos utilizar essa abordagem ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)). Uma ferramenta de terceiros que torna possível ter ambientes macOS consistentes é a [Veertu](https://veertu.com/).

Nos últimos anos, containers descartáveis (ou _disposable containers_) ganharam popularidade pelos mais variados motivos:

- builds completamente reproduzíveis com zero dependência do sistema operacional que o hospeda
- roda em qualquer máquina (sua máquina local ou qualquer servidor na nuvem)
- um build limpo, com somente as dependências mais necessárias

Atualmente, a melhor abordagem que nós desenvolvedores iOS podemos seguir é:

- Automatizar a instalação do Xcode usando o [xcode-install](https://github.com/krausefx/xcode-install)
- Usar um [arquivo .xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) para especificar a versão exata do Xcode
- Definir todas as dependências em arquivos de configuração (ver fator [Dependências](/dependencies))
- Automatizar o processo completo de deploy utilizando uma ferramenta como o [fastlane](https://fastlane.tools)
- Automatizar a assinatura do código (ou _code signing_) (ex: [codesigning.guide](https://codesigning.guide))
- Fazer deploys com frequência, idealmente ao menos uma vez por semana

Muitas empresas usam o conceito de Trens de Lançamento (ou _Release Trains_): uma data/horário na qual uma nova versão da sua app é lançada. Todo código que foi integrado na sua banch principal (ex: `master` ou `release`) no momento que um trem de lançamento "parte", será enviado para a App Store. Essa abordagem é implementada pela maioria das apps iOS grandes.