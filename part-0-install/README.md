## Part 0 - Inside, I, I, stand alone!

### AWS CLI

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" \
        -o "awscliv2.zip"
    unzip awscliv2.zip

    ./aws/install \
        --update \
        -i ~/.local/lib/python3.8/site-packages/aws-cli \
        -b ~/.local/bin

    echo "AWS Version: $(aws --version)"
    # AWS Version: aws-cli/2.2.23

### AWS SAM CLI

    curl -L "https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip" \
        -o "aws-sam-cli-linux-x86_64.zip"
    unzip aws-sam-cli-linux-x86_64.zip -d sam

    ./sam/install \
        --update \
        -i ~/.local/lib/python3.8/site-packages/aws-sam-cli \
        -b ~/.local/bin

    echo "AWS SAM Version: $(sam --version)"
    # SAM CLI, version 1.27.2
