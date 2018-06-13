A configuração de um aplicativo é tudo que é passível de mudança entre as formas de distribuição (App Store, TestFlight, ambiente local) ou que muda com o tempo sem que o código em si tenha sido alterado. Isso inclui:

- Chaves de API para serviços de backend (tanto serviços internos quanto externos)
- URLs para recursos remotos (as APIs que seu aplicativo usa)
- Habilidade de ligar/desligar funcionalidades

Algumas vezes, aplicativos guardam configurações como valores constantes no código. Isso é uma violação do iOS-factor, que requer **separação rígida de configurações do código**. Configurações variam substancialmente entre os tipos de distribuição. Código não.

Um teste final para saber se o aplicativo tem todas as suas configurações separadas do código, é quando seu código fonte está pronto para poder ser aberto a qualquer momento, sem comprometer nenhuma credencial.

Existem diversas formas de como você pode injetar configurações em tempo de compilação:

- Arquivos de configuração (ex: arquivos JSON ou YAML)
- [cocoapods-keys](https://github.com/orta/cocoapods-keys) para melhor esconder as chaves e aplicá-las ao seus aplicativos iOS durante tempo de compilação
- Soluções customizadas já prontas (ex: usando comandos no `Build Phase`)

Dado que os processos de distribuição pra plataforma iOS são significantemente mais lentos do que para servidores, é provável que você queira uma forma de rapidamente atualizar configurações remotamente (_over the air - OTA_) para reagir a problemas o quanto antes.

Atualizações de configuração OTA são poderosas e instantaneamente lhe permitem:

- Rodar testes A/B para habilitar certas funcionalidades ou mudanças de interface somente para um grupo dos seus usuários ativos
- Rotacionar chaves de API
- Atualizar _web hosts_ ou outras URLs que foram atualizadas
- Desabilitar funcionalidades remotamente ou esconder botões

Sem atualizações OTA você tem que esperar mais ou menos um dia para o processo de revisão de apps aprovar seu aplicativo. Todo envio também inclui o risco de ser rejeitado, atrasando o lançamento de um potencial envio urgente.

Da mesma forma, você pode querer continuar dando retrocompatibilidade, o que significa que usuários que não podem atualizar pra versão mais nova do iOS provavelmente não conseguirão instalar nenhuma atualização do seu aplicativo. Disponibilizando atualizações OTA, você consegue continuar dando suporte a versões mais antigas do seu aplicativo.

Algumas abordanges comuns quando se está implementando atualizações de configuração OTA:

- Implementar sua própria solução
- Serviços proprietários como a [Configuração Remota do Firebase](https://firebase.google.com/docs/remote-config/)
