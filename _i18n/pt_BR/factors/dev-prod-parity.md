Historicamente, tem existido grandes diferenças entre os ambientes de desenvolvimento (um desenvolvedor fazendo edições constantes na sua máquina local) e de produção (uma app que está na App Store e que pode ser acessada pelos usuários finais). Essas diferenças se manifestam em três áreas.

- **Diferença de tempo:** Um desenvolvedor pode trabalhar num código que leva dias, semanas ou até mesmo meses para ir pra produção
- **Diferença de pessoas:** Todos desenvolvedores iOS escrevem código, somente um sabe como fazer o deploy da app
- **Diferença de ferramentas:** Desenvolvedores podem estar usando um servidor de _staging_ que está rodando uma versão diferente da de produção. Desenvolvedores podem estar usando uma versão diferente do Xcode da versão que está sendo utilizada para fazer o deploy

**Uma app iOS-factor é feita para [entrega contínua](https://avc.com/2011/02/continuous-deployment/) (ou _continuous deployment_) quando mantém as diferenças entre os ambientes de desenvolvimento e produção pequenas.** Olhando para as três diferenças descritas acima:

- Reduza as diferenças de tempo: um desenvolvedor deve ser capaz de escrever um código e fazer o deploy dele apenas poucos dias após
- Reduza as diferenças de conhecimento entre as pessoas: quem escreveu o código está mais envolvido em fazer o deploy e observar seu comportamento em produção. Isso é melhor feito ao automatizar o processo de lançamento da sua app, e colocar o conhecimento sobre como o fazer nas declarações do próprio código ao invés de documentação.
- Reduza as diferenças entre as ferramentas: mantenha os ambientes de desenvolvimento e produção o mais parecido possíveis. Siga os princípios do fator [Dependências](/dependencies) do iOS-factor e utilize um arquivo `.xcode-version` além de definir todas outras dependências explicitamente.

Resumindo o que foi descrito acima em uma tabela:

|          | app iOS tradicional | app iOS-factor |
|----------|---------------------|----------------|
| Tempo entre deploys | Meses  | Dias             |
| Quem escreve o código _vs_ quem faz o deploy | 1 pessoa sabe fazer o deploy | deploy automatizado, idealmente através de um servidor |
| Ambientes de dev e produção | Divergentes |  O mais parecido possíveis |
