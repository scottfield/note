### rest APIs
#### get cluster setting
```shell
curl 'localhost:9200/_cluster/settings?pretty'
```

#### create index
```shell
curl -X PUT 'localhost:9200/customer' 
```

#### add document to existing index
```shell
curl -X PUT "localhost:9200/customer/_doc/2" -H 'Content-Type: application/json' -d '
{
  "name": "John Doe",
  "age": 20
}'
```

### bulk add documents to index(it boost performance by reduce network round trip)
```
curl -H "Content-Type: application/json" -X POST "localhost:9200/bank/_bulk?pretty&refresh" --data-binary "@accounts.json"
```

#### get document by ID
```shell
curl "localhost:9200/customer/_doc/2?pretty"
```



#### get index info
```shell
 curl "localhost:9200/_cat/indices?v"
```
#### search data, by default ES only return first 10 documents in hits section
```shell
curl -X GET "localhost:9200/bank/_search" -H 'Content-Type: application/json' -d '
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}'
```

#### search by pagination
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ],
  "from":10,
  "size":10
}'

```

#### use match to search field contains special word
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "query": { "match": {"address":"lane mill"} },
  "sort": [
    { "account_number": "asc" }
  ]
}'
```

#### use match-phrase to search field contains special phrase
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "query": { "match_phrase": {"address":"mill lane"} },
  "sort": [
    { "account_number": "asc" }
  ]
}'
```
#### use bool to combine multiple search criteria
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ],
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}'
```
#### do aggregation search
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}'
```
#### do nested aggregation search
```shell
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d '
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword",
        "order": {
          "average_balance": "desc"
        }
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}'
```