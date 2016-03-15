To count queues in an account (for the default region):

`alias sqscnt='aws sqs list-queues | jq .QueueUrls[] | wc -l'`

Count topics:

`alias snscnt='aws sns list-topics | jq .Topics[].TopicArn | wc -l'`

Handy summary:

```
echo -e "queues: $(sqscnt)\ntopics: $(snscnt)"
```
