## Part 2 - Hey, Shake and Bake!

### CloudFormation

    export CFN_STACK_NAME="TTTT-SAM"
    export CFN_S3=tttt-devel-cfn

### Initializer

    sam init \
        --no-interactive \
        --runtime python3.8 \
        --dependency-manager pip \
        --app-template hello-world \
        --name sam-app

### Local Development

    cd sam-app

    sam local invoke HelloWorldFunction --event events/event.json
    sam local start-api

    curl http://localhost:3000/

### Deployment

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
      --query "Stacks[].Outputs[?OutputKey=='HelloWorldApi'].OutputValue[] | [0]"

    curl --request POST https://APIGW_ID.execute-api.AWS_REGION.amazonaws.com/call

### Cleanup

    aws cloudformation delete-stack \
        --stack-name $CFN_STACK_NAME
