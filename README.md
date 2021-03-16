# try-great-expectations
 
## get_started

Notes
1. If you were to connect to a database that requires connection credentials, those would be stored in `great_expectations/uncommitted/config_variables.yml`.
2. You can also configure Great Expectations to store Expectations to other locations, such as S3, Postgres, etc. 
3. Once you’ve configured and saved a Checkpoint, you can load and run it every time you want to validate your data.
4. With `query` paramters, you can run on a dataset "view".

To manually build query-based Batch Kwargs, create a dictionary:
```
batch_kwargs = {
    "datasource": "my_db",
    "query": "SELECT * FROM my_schema.my_table WHERE '1988-01-01' <= date AND date < '1989-01-01';
}
```
To use a Query Batch Kwargs Generator, call the build_batch_kwargs method:
```
batch_kwargs = context.build_batch_kwargs(
    "my_db",
    "queries",
    "movies_by_date",
    query_parameters={
        "start": "1988-01-01",
        "end": "1989-01-01"
    }
)
```

5. Result in JSON 
```json
 {
      "result": {
        "observed_value": "int64"
      },
      "meta": {},
      "exception_info": {
        "raised_exception": false,
        "exception_message": null,
        "exception_traceback": null
      },
      "success": true,
      "expectation_config": {
        "kwargs": {
          "column": "passenger_count",
          "type_list": [
            "INTEGER",
            "integer",
            "int",
            "int_",
            "int8",
            "int16",
            "int32",
            "int64",
            "uint8",
            "uint16",
            "uint32",
            "uint64",
            "INT",
            "TINYINT",
            "BYTEINT",
            "SMALLINT",
            "BIGINT",
            "IntegerType",
            "LongType",
            "DECIMAL"
          ],
          "result_format": {
            "result_format": "SUMMARY",
            "partial_unexpected_count": 20
          }
        },
        "meta": {},
        "expectation_type": "expect_column_values_to_be_in_type_list"
      }
    }
```