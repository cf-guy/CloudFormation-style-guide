- When bootstrapping an EC2 instance using a script in `UserData`:

Example:

```yaml

Resources:
  webserver:
    Type: AWS::EC2::Instance
    Properties:
      ImageId:
      UserData:
        Fn::Base64:
          !Sub |
            #!/bin/bash -eux
            yum install -y aws-cfn-bootstrap
            /opt/aws/bin/cfn-init -r ${webserver} -s ${AWS::StackId} --region ${AWS::Region}

```

using JSON:

```json
"TBD"

```

