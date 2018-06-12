O projeto iOS-factor foi inspirado pelo famoso framework de apps [twelve-factor](https://www.12factor.net/), que é uma metodologia para escrever serviços web de alta qualidade. O projeto usa a mesma estrutura e princípos similares, reescritos e aplicados aos processos de desenvolvimento de apps iOS.

## Contexto

Nos últimos 10 anos, o processo de desenvolvimento para iOS mudou drasticamente:

- de suportar um único aparelho para uma vasta lista de iPhones e iPads rodando iOS e outras plataformas como tvOS e watchOS
- de manualmente incluir _git submodules_ para usar gerenciadores de dependência
- de apps iOS em sua maioria rodando localmente no aparelho, para apps iOS que dependem profundamente de serviços de backend
- de processos de revisão de mais de 2 semanas para menos de um dia
- de instalar apps no seu telefone usando o iTunes, para distribuir apps através de um canal oficial (TestFlight)
- de subir 5 screenshots por idioma para o iTunes Connect, para 110 por idioma, bem como preview de apps
- de apps puramente escritas em Objective-C/C++ para uma mistura de linguagens, incluindo JavaScript
- de entregas lentas sempre quando algo estava pronto, para lançamentos semanais
- de entregas de versões completas para testes A/B, entregas graduais e detecção automática de regressão

## O que é o iOS-factor?

O iOS-factor é um projeto experimental iniciado em maio de 2018. Ele tem o objetivo de prover uma coleção de melhores práticas para a construção de aplicações iOS de alta qualidade. Cada tópico é coberto por um `fator`, que descreve o estado ideal de como uma certa categoria do processo de desenvolvimento de apps iOS deveria ser.

Devido a certas limitações (como o Xcode rodar só no macOS) nem todos os requisitos podem ser preenchidos. Este projeto tem o intuito de definir objetivos, assim como as atuais melhores abordagens para resolver alguns dos desafios com os quais nos deparamos.

O iOS-factor é sobre decisões de arquitetura e processos de desenvolvimento de apps iOS num nível mais amplo, e por isso não cobre nenhum desafio específico de linguagem.

Este é um projeto em constante desenvolvimento, mantido pela comunidade de desenvolvedores iOS. Você pode encontrar o código fonte completo no [GitHub](https://github.com/ios-factor/ios-factor.com) e atualizar páginas já existentes ou adicionar novos fatores.

-----
