A configuração de uma app é tudo que é provável que mude entre deploys (App Store, TestFlight, ambiente local) ou que muda com o tempo sem que o código em si tenha sido alterado. Isso inclui:

- Chaves de API para serviços de backend (tanto serviços internos quanto externos)
- URLs para recursos remotos (as APIs que sua app usa)
- Habilidade de ligar/desligar funcionalidades

Algumas vezes, apps guardam configurações como constantes no código. Isso é uma violação do fator-iOS, que requer **separação rígida de configurações do código**. Configurações variam substancialmente entre deploys, código não.

Um teste final para saber se a app tem todas as suas configurações arquitetadas pra fora do código, é quando seu código fonte pode ser aberto a qualquer momento, sem comprometer nenhuma credencial.

Existem diversas formas de como você pode injetar configurações em tempo de compilação

- Arquivos de configuração (ex: arquivos JSON ou YAML)
- [cocoapods-keys](https://github.com/orta/cocoapods-keys) para melhor esconder as chaves e aplicá-las às suas apps iOS durante tempo de compilação
- Soluções customizadas já prontas (ex: usando comandos no `Build Phase`)

Dado que deploys pra plataforma iOS são significantemente mais lentos do que deploys para servidores, é provável que você queira uma forma de rapidamente atualizar configurações remotamente (_over the air - OTA_) para reagir a problemas o quanto antes.

Atualizações de configuração OTA são poderosas e instantenamente lhe permitem

- Rodar testes A/B para habilitar certas funcionalidades ou mudanças de interface somente para um grupo dos seus usuários ativos
- Rotacionar chaves de API
- Atualizar _web hosts_ ou outras URLs que foram atualizadas
- Desabilitar funcionalidades remotamente ou esconder botões

Sem atualizações OTA você tem que esperar mais ou menos um dia para o processo de revisão de apps aprovar sua app. Todo envio de apps também inclui o risco dela ser rejeitada, atrasando o lançamento de um potencial envio urgente.

Da mesma forma, você pode querer continuar dando retrocompatibilidade, o que significa que usuários que não podem atualizar pra versão mais nova do iOS provavelmente não conseguirão instalar nenhuma atualização de sua app. Disponibilizando atualizações OTA, você consegue continuar dando suporte a versões mais antigas do seu aplicativo.

Algumas abordanges comuns quando se está implementando atualizações de configuração OTA:

- Implementar sua própria solução
- Serviços proprietários como [Configuração Remota do Firebase](https://firebase.google.com/docs/remote-config/)
