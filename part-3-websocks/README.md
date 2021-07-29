## Part 3 - My socks are never clean, we gon burn the whole house down

### CloudFormation

    export CFN_STACK_NAME="TTTT-WebSocket"
    export CFN_S3=tttt-devel-cfn

### HelloWorld (for WebSockets)

    git clone https://github.com/aws-samples/simple-websockets-chat-app
    cd simple-websockets-chat-app

### Deploy

    sam validate --template template.yaml

    sam build --template template.yaml

    sam package --output-template-file packaged.yaml \
        --s3-bucket $CFN_S3 \
        --force-upload

    sam deploy --template-file packaged.yaml \
        --capabilities CAPABILITY_NAMED_IAM \
        --stack-name $CFN_STACK_NAME \
        --tags StackName=$CFN_STACK_NAME \
        --no-confirm-changeset

### Test

    aws cloudformation describe-stacks \
      --stack-name $CFN_STACK_NAME \
      --query 'Stacks[].Outputs[?OutputKey=='HelloWorldApi'].OutputValue[] | [0]'

    npm install -g wscat

    wscat -c wss://{YOUR-API-ID}.execute-api.{YOUR-REGION}.amazonaws.com/{STAGE}

    {"action":"sendmessage", "data":"hello world"}


### Cleanup

    aws cloudformation delete-stack \
        --stack-name $CFN_STACK_NAME
