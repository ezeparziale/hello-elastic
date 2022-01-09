# 📊 Demo elastic search y Kibana

Versiones:

* Elastic: 7.15.0
* Kibana: 7.15.0

## 🏃‍♂️ Run

Para version simple sin autenticación:

```dockerfile
docker-compose -f "docker-compose_simple.yaml" up -d
```

Para version simple con autenticación (pide usuario y contraseña):

```dockerfile
docker-compose -f "docker-compose_secutity.yaml" up -d
```

## 🗺️ WebUI

```http
http://localhost:5601
```

## 💬 Querys

Se pueden correr en la consola para devs:  

```http
http://localhost:5601/app/dev_tools#/console
```

### ◽ INDEX

```json
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

### ◽ POST

```json
POST /jugadores/_doc/1
{
  "nombre": "Ronaldo",
  "club": "Manchester United"
}
```

```json
POST /jugadores/_doc/2
{
  "nombre": "Haaland",
  "club": "Dortmund"
}
```

```json
POST /jugadores/_doc/3
{
  "nombre": "Messi",
  "club": "Barcelona"
}
```

### ◽ GET

```json
GET /jugadores/_doc/3
```

### ◽ UPDATE

```json
POST /jugadores/_update/3
{ 
  "doc":
    {"club":"PSG"}
}
```

### ◽ GET ALL

```json
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

### ◽ BULK

```json
POST /_bulk
{ "index":{"_index": "jugadores", "_id": 4} }
{ "nombre":"De Bruyne", "club": "Manchester City" }
{ "index":{"_index": "jugadores", "_id": 5} }
{ "nombre":"Lewandowski", "club": "Bayern de Múnich" }
```

### ◽ FILTER

```json
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

### ◽ DELETE

```json
DELETE /jugadores/_doc/2
```

## 📚 Info API

```http
https://www.elastic.co/guide/en/elasticsearch/reference/current/docs.html
```
