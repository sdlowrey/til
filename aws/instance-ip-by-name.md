You have an instance with a "Name" tag and you want to get the public IP addr.

```
aws --output json ec2 describe-instances \
  --filters "Name=tag:Name,Values=My Inst" |
  jq .Reservations[0].Instances[0].PublicIpAddress
```

see `utils/getip` for realz
