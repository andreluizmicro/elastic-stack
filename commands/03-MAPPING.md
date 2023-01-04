### DEFININDO MAPPING

    curl -XPUT 127.0.0.1:9200/movies/_doc/109487 -d '
    {
        "mappings": {
            "properties": {
                "year": {
                    "type": "date"
                }
            }
        }
    }'


### PEGANDO O MAPPING CRIADO

    curl -XGET 127.0.0.1:9200/movies/_mapping


### INSERT MOVIE

    curl -XPOST 127.0.0.1:9200/movies/_doc/109487 -d '
    {
        "mappings": {
            "properties": {
                "genre": ["IMAX", "Sci-Fi"],
                "title": "Interstellar",
                "year": "2014"
            }
        }
    }'

### GET MOVIE

    curl -XGET 127.0.0.1:9200/movies/_search?pretty