De acordo com os guias da Apple, armazenar dados e configurações é fundamental para o ciclo de vida de seu aplicativo, especialmente quando se trata de sincronização com o iCloud, troca de telefone ou restauração de um telefone a partir de um backup.

Certifique-se de seguir o [Guia de armazenamento de dados](https://developer.apple.com/icloud/documentation/data-storage/index.html) oficial da Apple:

- `Documents`: Use esse diretório para conteúdos gerados pelo usuário. Ele será incluído em backups
- `Caches`: Use esse diretório para dados que possam ser regerados
- `tmp`: Use esse diretório para arquivos temporários
- Faça uso do atributo `do not back up` em arquivos

Nunca armazene informações sensíveis ao usuário (como senhas ou sessões) nesses diretórios. Ao invés disso, use a API do Keychain.

A API do Keychain lhe dá o controle de como o dado está sendo armazenado no aparelho. Certifique-se de que você tem um bom entendimento de como os [diversos atributos](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values) afetam o ciclo de vida de seu aplicativo.

Um questionamento muitas vezes ignorado que você deve se fazer é: quando o usuário fizer um upgrade para um novo aparelho, o dado (ex: sessão de login) deve ser migrado também?

Se você usa [`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly), o dado não será incluído no backup do iCloud ou do iTunes, o que significa que o usuário irá perder o dado quando fizer o upgrade do aparelho.