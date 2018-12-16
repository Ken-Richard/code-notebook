1. Create AWS Profile called home

Or tweak the commands below

2. Create Stack (Initial Deploy)

aws cloudformation create-stack --stack-name code-notebook-stack --template-body file://stack.yml  --capabilities CAPABILITY_IAM --profile home

3. Update Stack (Update Deploy)

aws cloudformation update-stack --stack-name code-notebook-stack --template-body file://stack.yml  --capabilities CAPABILITY_IAM --profile home

4. Test

Get the ID for the Gateway

```
API_ID=$(aws apigateway get-rest-apis --profile home --query 'items[?name==`code-notebook`]["id"][0]' --output text)
```

Test the endpoint
```
curl -X POST https://$API_ID.execute-api.us-east-1.amazonaws.com/call
```

