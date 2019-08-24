
## 查询数据
```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "system_id": 1
          }
        },
        {
          "range": {
            "create_time": {
              "from": "2018-12-31 00:00:00",
              "to": "2018-12-31 23:59:59"
            }
          }
        },
        {
          "nested": {
            "path": "records",
            "query": {
              "bool": {
                "must": [
                  {
                    "term": {
                      "records.intent_id": -1
                    }
                  }
                ]
              }
            }
          }
        }
      ]
    }
  },
  "_source": {
    "includes": [
      "id",
      "records.intent_id"
    ],
    "excludes": []
  },
  "sort": [
    {
      "create_time": {
        "order": "desc"
      }
    },
    {
      "_id": {
        "order": "desc"
      }
    }
  ],
  "aggs": {
    "records": {
      "nested": {
        "path": "records"
      },
      "aggs": {
        "query_count": {
          "value_count": {
            "field": "records.intent_id",
		        "min_doc_count": 0  # 最小为0 会将doc_count为0的也展示
          }
        }
      }
    }
  }
}
```

## 导出数据
### elasticdump
```bash
elasticdump --input=http://localhost:9200/edp_index_dev --output=C:\\Users\\liweiwei\\Desktop\\abc.json --searchBody "{\"query\":{\"bool\":{\"must\":[]}}}"
```