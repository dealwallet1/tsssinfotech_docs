# Meilisearch info

Index Creation
```sh
curl --location 'https://meilisearch.dealwallet.com/indexes' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer KEY' \
--data '{
    "uid": "products",
    "primaryKey": "id"
}'
```

Embeddings creation
```sh
curl --location --request PATCH 'https://meilisearch.dealwallet.com/indexes/products/settings' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer KEY' \
--data '{
    "embedders":
    {
"default": {
        "source": "ollama",
        "url":"http://ollama.dealwallet.com/api/embeddings",
        "model":"nomic-embed-text:v1.5"
        
              }
    }
}'
```

Hybrid search
```sh
curl --location 'https://meilisearch.dealwallet.com/indexes/products/search' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "q":"give me redmi mobiles",
    
        "hybrid":
        {
          "semanticRatio":0.5,
          "embedder":"default"  
        }
    
}'
```

