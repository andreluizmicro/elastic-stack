## JSON BULK IMPORT

    _bulk : Informa ao Elasticsearch que estamos fazendo uma inserção em Lote

    curl -XPUT 127.0.0.1:9200/_bulk –d ‘
        
        { "create" : { "_index" : "movies", "_id" : "135569" } }
        { "id": "135569", "title" : "Star Trek Beyond", "year":2016 , "genre":["Action", "Adventure", "Sci-Fi"] }
        { "create" : { "_index" : "movies", "_id" : "122886" } }
        { "id": "122886", "title" : "Star Wars: Episode VII - The Force Awakens", "year":2015 , "genre":["Action", "Adventure", "Fantasy", "Sci-Fi", "IMAX"] }
        { "create" : { "_index" : "movies", "_id" : "109487" } }
        { "id": "109487", "title" : "Interstellar", "year":2014 , "genre":["Sci-Fi", "IMAX"] }
        { "create" : { "_index" : "movies", "_id" : "58559" } }
        { "id": "58559", "title" : "Dark Knight, The", "year":2008 , "genre":["Action", "Crime", "Drama", "IMAX"] }
        { "create" : { "_index" : "movies", "_id" : "1924" } }
        { "id": "1924", "title" : "Plan 9 from Outer Space", "year":1959 , "genre":["Horror", "Sci-Fi"]
    }'


### INSERINDO EM LOTE ATRAVÉS DE ARQUIVO JSON

    curl -XPUT 127.0.0.1:9200/_bulk?pretty --data-binary @movies.json

### REALIZANDO UMA CONSULTA APÓS INSERÇÃO

Fazendo uma consulta de todos os ```filmes``` que estão no nosso ```índice movies```

    curl -XGET 127.0.0.1:9200/movies/_search?pretty