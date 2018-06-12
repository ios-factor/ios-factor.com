Nos últimos anos, alguns times de desenvolvimento começaram a usar abordagens que requerem menos trabalho de desenvolvimento, pagando o custo da experiência de uso do aplicativo ao mover mais lógica para um backend remoto e ter a app iOS como apenas um cliente simples que mostra resultados do servidor. Este approach resulta na frustração de usuários quando a app é utilizada em situações com uma conexão de internet não tão perfeitas assim (como em metrôs, elevadores ou uma WiFi irregular).

**Apps devem executar as regras de negócio e cálculos no aparelho sempre que possível** pelas mais variadas razões:

- Privacidade: evitar enviar dados para um servidor remoto
- Velocidade: enviar dados para um servidor e esperar por uma resposta requer tempo e pode falhar (ex: WiFi irregular)
- Utilização de dados: usuários muitas vezes tem limite de plano de dados
- Escala: se sua app viralizar, você precisa escalar os serviços de backend
- Vida útil da bateria: o uso de dados móveis é custoso para a vida útil da bateria
- Confiança na rede: Alguns países ainda possuem conexões LTE/3G não muito confiáveis

A maioria das apps iOS requer algum tipo de backend para determinadas tarefas, como autenticação, cálculos mais complexos ou armazenamento de dados.

**Reduza o número de tafefas que rodam no backend para melhorar a experiência do usuário e proteger sua privacidade.**

Todas as partes da app que não necessariamente **precisam** de uma conexão com a internet (ex: login) devem ser capazes de funcionar sem conexão com a internet:

- A tela de início da sua app, ou _launch screen_, ([que a propósito não deveria existir](https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/launch-screen/)), nunca deve esperar pela primeira resposta de sucesso da internet, pois isso gera uma experiência ruim para o usuário com uma conexão inconsistente
- Se sua app requer conexão de internet para tudo (ex: app de rede social ou de carona compartilhada), sua app deve ainda assim funcionar (de modo passivo) sem uma conexão com a internet para acessar dados históricos (ex: caronas recentes, mensagens recentes).
- Toda funcionalidade da sua app que precise de uma conexão funcional com a internet deve mostrar uma mensagem de erro clara de que não foi possível se conectar ao servidor.
- Dado que hotspots WiFi podem requerer um login ou uma confirmação de algum tipo (ex: hotel ou aeroporto), requisições HTTPS irão ficar travadas com frequência e darão time-out após cerca de 1 minuto. Até que a Apple resolva esse problema a nível de sistema, nós como desenvolvedores temos que garantir que estamos tratando essas situações da forma correta.
- Nunca assuma que um usuário possui uma conexão com a internet funcionando na primeira vez que abre a app. O usuário pode instalar sua app e não abrí-la, até o momento em que o faz e não tem uma conexão. Você é responsável por entregar sua app num estado que ela funciona com os recursos mais atuais durante o momento do deploy. Isso tem relação direta com os lançamentos semanais dos trens descritos no fator [deployment](/deployment).
