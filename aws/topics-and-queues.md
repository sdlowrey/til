To count queues in an account (for the default region):

`alias sqslist='aws sqs list-queues | jq .QueueUrls[]'`

Count topics:

`alias snslist='aws sns list-topics | jq .Topics[].TopicArn'`

Handy summary:

```
echo -e "queues: $(sqslist|wc -l)\ntopics: $(snslist|wc -l)"
```
