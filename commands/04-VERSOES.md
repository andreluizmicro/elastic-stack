## ATUALIZAÇÃO DE DOCUMENTOS NO ELASTICSEARCH

    - Documentos são imutáveis
    - Todo documento tem um campo _version
    - Quando você atualiza um documento:
        - Um novo documento é criado e a versão é incrementada
        - O documento antigo é marcado para exclusão
    
### PODEMOS ATUALIZAR UM DOCUMENTO DE DUAS FORMAS:

    - Inserindo o documento novamente, com todos os campos.
    - Usando a api Update, definindo apenas o que mudou.

## Update api:

    curl -XPOST 127.0.0.1:9200/movies/_doc/109487/_update -d '
    {
        "doc": {
            "title": "Interstellar"
        }
    }'
    
### INSERINDO O DOCUMENTO NOVAMENTE ESTAMOS SOBRESCREVENDO O MESMO

    curl -XPUT 127.0.0.1:9200/movies/_doc?109487/pretty -d '
    {
        "genres": ["IMAX", "Sci-fi"],
        "title": "Interstellar foo",
        "year": "2014"
    }'

### RECUPERANDO UM FILME ESPECÍFICO VIA CURL

    curl -XGET 127.0.0.1:9200/movies/_doc/109487?pretty

### ATUALIZAÇÃO PARCIAL

    curl -XPOST 127.0.0.1:9200/movies/_doc/109487/_update -d '
    {
        "doc": {
            "title": "Interstellar"
        }
    }'

## EXCLUSÃO

Para deletar um movie vamos usar o método DELETE

    curl -XDELETE 127.0.0.1:9200/movies/_doc/58559

