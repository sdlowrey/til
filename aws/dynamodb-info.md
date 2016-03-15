Using the AWS CLI and `jq`:

Assume `alias ddb = 'aws dynamodb'` in these examples

*  List tables
```
aws dynamodb list-tables
```
* Get the number of items in a table
```
aws dynamodb describe-table --table-name my-table | jq .Table.ItemCount
```
