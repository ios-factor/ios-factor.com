Apesar da maioria dos seus usuários atualizarem para a última versão dentro de poucas semanas, sempre existirá um grupo de usuários que não o fará. Isso pode ter inúmeras razões. Algumas vezes isso está relacionado com a versão do iOS que eles usam, versão essa que eles nem sempre podem atualizar dependendo do quão antigo o aparelho é.

Você pode instalar e usar o Facebook Messenger num iPad da primeira geração (2010). Apesar de novas funcionalidades não serem suportadas, a funcionalidade principal ainda é disponibilizada graças ao versionamento de APIs.

O conceito básico é que você não atualiza uma API existente, mas sim adiciona uma nova e deixa elas rodando em paralelo

```
https://your-api.com/1.0/drivers.json
https://your-api.com/1.1/drivers.json
```

Você até pode em algum momento precisar desligar ou fazer mudanças sutis na semântica de uma API. Mesmo se sua empresa tiver um compromisso profundo com estabilidade, em alguns casos assuntos de justiça forçam essa mudança. Isso significa que você deve criar um endpoint na sua API que indique o seu status.

```
https://your-api.com/1.0/status.json
https://your-api.com/1.1/status.json
```

The status API should include information such as

 - What's the stage of the API? (e.g. testing, beta, production)
 - Is the API deprecated? If so, what date is it scheduled to be turned off?
 - Is the API offline? If so, will it remain so or is it a temporary outage?

O status da API deve incluir informações tais como

 - Qual é o ambiente da API? (ex: teste, beta, produção)
 - A API está descontinuada? Se sim, que dia ela está agendada para ser desligada?
 - A API está desligada? Se sim, ela vai continuar assim ou é só uma queda temporária?