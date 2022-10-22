Nos últimos anos, alguns times de desenvolvimento começaram a usar abordagens que requerem menos trabalho de desenvolvimento, às custas da experiência de uso do aplicativo, ao mover mais lógica para um backend remoto e ter o aplicativo iOS sendo apenas um cliente simples que mostra resultados do servidor. Esse approach resulta na frustração de usuários quando o aplicativo é utilizado em situações com uma conexão de internet não tão perfeitas assim (como em metrôs, elevadores ou uma rede WiFi irregular).

**Aplicativos devem executar regras de negócio e cálculos no aparelho sempre que possível** pelas mais variadas razões:

- Privacidade: evitar enviar dados para um servidor remoto
- Velocidade: enviar dados para um servidor e esperar por uma resposta requer tempo e pode falhar (ex: WiFi irregular)
- Utilização de dados: usuários muitas vezes têm um plano de dados limitado
- Escala: se seu aplicativo viralizar, você precisa escalar os serviços de backend
- Vida útil da bateria: o uso de dados de celular é custoso para a vida útil da bateria
- Garantia de boa conexão: Alguns países ainda possuem conexões LTE/3G não muito confiáveis

A maioria dos aplicativos iOS requer algum tipo de backend para determinadas tarefas, como autenticação, cálculos mais complexos ou armazenamento de dados.

**Reduza o número de tafefas que rodam no backend para melhorar a experiência do usuário e proteger sua privacidade.**

Todas as partes do aplicativo que não necessariamente **precisam** de uma conexão com a internet (o que não é o caso do login, por exemplo) devem ser capazes de funcionar sem conexão com a internet:

- A tela inical do aplicativo, ou _launch screen_, ([que a propósito nem deveria existir](https://developer.apple.com/design/human-interface-guidelines/patterns/launching/)), nunca deve esperar pela primeira resposta de sucesso do servidor, pois isso gera uma experiência ruim para o usuário com uma conexão inconsistente
- Se seu aplicativo requer conexão de internet para tudo (ex: aplicativo de rede social ou de carona compartilhada), ele deve ainda assim funcionar (de modo passivo) sem uma conexão com a internet para acessar dados históricos (ex: caronas recentes, mensagens recentes).
- Toda funcionalidade do aplicativo que precise de uma conexão funcional com a internet deve mostrar uma mensagem de erro clara de que não foi possível se conectar ao servidor.
- Dado que hotspots WiFi podem requerer um login ou uma confirmação de algum tipo (ex: hotel ou aeroporto), requisições HTTPS irão ficar travadas com frequência e darão time-out após cerca de 1 minuto. Até que a Apple resolva esse problema a nível de sistema, nós como desenvolvedores temos que garantir que estamos tratando essas situações da forma correta.
- Nunca assuma que um usuário possui uma conexão com a internet funcionando na primeira vez que abre o aplicativo. O usuário pode instalá-lo e não abrí-lo, até o momento em que o faz e não tem uma conexão. Você é responsável por entregar seu aplicativo num estado que ele funciona com os recursos mais atuais durante o momento de distribuição. Isso tem relação direta com os lançamentos semanais dos trens descritos no fator [distribuição](/pt_BR/deployment).
