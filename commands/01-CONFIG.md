## CONFIGURAÇÃO

Crie a pasta ```bin``` na raiz do user

    mkdir bin

crie o arquivo curl com o seguinte conteúdo

    #!/bin/bash
    /usr/bin/curl -H "Content-Type: application/json" "$@"

Para tornar o script executavel no Linux mudamos a permissão com o comando:

    chmod a+x curl
