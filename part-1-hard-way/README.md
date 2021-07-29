## Part 1 - The Waiting is the Hardest Part

### CloudFormation

    export CFN_STACK_NAME="TTTT-CFN"
    export CFN_S3=tttt-devel-cfn

###

    aws s3api create-bucket --bucket $CFN_S3 --region $AWS_DEFAULT_REGION

### Deploy

    aws cloudformation package \
      --template-file template.yaml \
      --s3-bucket $CFN_S3 \
      --output-template-file packaged.yaml

    aws cloudformation deploy \
      --template-file packaged.yaml \
      --stack-name $CFN_STACK_NAME \
      --capabilities CAPABILITY_IAM

### Test

    aws cloudformation describe-stacks \
      --stack-name $CFN_STACK_NAME \
      --query "Stacks[].Outputs[?OutputKey=='HelloWorldApi'].OutputValue[] | [0]"

    curl --request GETT https://APIGW_ID.execute-api.AWS_REGION.amazonaws.com/call

### Cleanup

    aws cloudformation delete-stack \
        --stack-name $CFN_STACK_NAME
