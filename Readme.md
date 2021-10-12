# Demo elastic search y Kibana

Versiones:
* Elastic: 7.15.0
* Kibana: 7.15.0

## Run

```
docker-compose up -d
```

## WebUI

```url
http://localhost:5601
```

## Querys

Se pueden correr en la consola para devs:  
```
http://localhost:5601/app/dev_tools#/console
```

### INDEX

```
PUT jugadores 
{
   "mappings":{
      "dynamic":"strict",
      "properties":{
         "nombre":{
            "type":"text"
         },
         "club":{
            "type":"text"
         }
      }
   }
}
```

### POST

```
POST /jugadores/_doc/1
{
  "nombre": "Ronaldo",
  "club": "Manchester United"
}
```

```
POST /jugadores/_doc/2
{
  "nombre": "Haaland",
  "club": "Dortmund"
}
```

```
POST /jugadores/_doc/3
{
  "nombre": "Messi",
  "club": "Barcelona"
}
```

### GET

```
GET /jugadores/_doc/3
```

### UPDATE

```
POST /jugadores/_update/3
{ 
  "doc":
    {"club":"PSG"}
}
```

### GET ALL

```
GET /jugadores/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      }
    }
  }
}
```

### BULK

```
POST /_bulk
{ "index":{"_index": "jugadores", "_id": 4} }
{ "nombre":"De Bruyne", "club": "Manchester City" }
{ "index":{"_index": "jugadores", "_id": 5} }
{ "nombre":"Lewandowski", "club": "Bayern de Múnich" }
```

### FILTER

```
GET /jugadores/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      },
      "filter": {
        "term": {
          "nombre": "ronaldo"
        }
      }
    }
  }
}
```

### DELETE

```
DELETE /jugadores/_doc/2
```

## Info API

```url
https://www.elastic.co/guide/en/elasticsearch/reference/current/docs.html
```