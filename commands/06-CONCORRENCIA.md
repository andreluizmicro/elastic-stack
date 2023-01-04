## CONCORRENCIA: O PROBLEMA

Concorrencia é um problema que ocorre em sistemas distribuidos. Imagine que dois clientes tentam atualizar o mesmo documento ao mesmo tempo.

<br>

### EXEMPLO REAL

<img src="../public/concorrencia.png"> <br><br>

### SOLUÇÃO: CONTROLE DE CONCORRÊNCIA OTIMISTA

A imagem abaixo ilustra a solução do problema de concorrência, observe que quando duas ou mais pessoas tentar atualizar ao mesmo tempo, apenas um terá sucesso, e o próprio elasticserch vai retornar um erro.

    Use retry_on_conflict=N npara tentar novamente automaticamente

<img src="../public/concorrencia-solucao.png">

### PRÁTICA

Vamos pedir ao elasticserch para retornar um documento e vamos observar o retorno:

    curl -XGET 127.0.0.1:9200/movies/_doc/109487?pretty

    Retorno:
    {
        "_index": "movies",
        "_type": "_doc",
        "_id": "1924",
        "_version": 2,
        "result": "updated",
        "_shards": {
            "total": 2,
            "successful": 1,
            "failed": 0
        },
        "_seq_no": 12,
        "_primary_term": 1
    }

    _version: É a versão do documento
    _seq_no: Número de sequência
    _primary_term: termo primário

### ATUALIZAÇÃO

Usando o documento acima de referência podemos fazer uma atualização desse documento utilizando o ```_seq_no e _primary_term``` isso garante que se houver um conflito ou problema de concorrencia a atualização vai falhar.

No caso abaixo ele vai fazer a atualização se o número de sequencia for 7 e o termo primário for 1

    curl -XPUT "127.0.0.1:9200/movies/_doc/109487?if_seq_no=7&if_primary_term=1" -d '
    {
        "genres": [
            "IMAX",
            "Sci-fi"
        ],
        "title": "Interestellar foo",
        "year": 2014
    }'


### ATUALIZAÇÃO AUTOMÁTICA

Também podemos fazer com que o proprio eslasticsearch faça uma nova tentativa em caso de conflito, No exemplo abaixo vamos tentar por 5 vezes

    curl -XPOST 127.0.0.1:9200/movies/_doc/109487/_update?retry_on_conflict=5 -d '
    {
        "doc": {
            "title": "Interestellar typo"
        }
    }'