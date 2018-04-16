- When bootstrapping an EC2 instance using a script in `UserData`:

Example:

```yaml

Parameters:
  ImageId: 
    Description: Amazon Machine Image Id for the webserver instance
    Type: AWS::EC2::Image::Id

Resources:
  webserver:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref ImageId
      UserData:
        Fn::Base64:
          !Sub |
            #!/bin/bash -eux
            yum install -y aws-cfn-bootstrap
            /opt/aws/bin/cfn-init -r ${webserver} -s ${AWS::StackId} --region ${AWS::Region}

```

using JSON:

```json
{
  "Resources": {
    "webserver": {
      "Type": "AWS::EC2::Instance",
      "Properties": {
        "ImageId": "",
        "UserData": {
          "Fn::Base64": {
            "Fn::Join": [
              "", [
                "#!/bin/bash -eux \n",
                "yum install -y aws-cfn-bootstrap \n",
                "/opt/aws/bin/cfn-init",
                " -r ", 
                {
                  "Ref": "webserver"
                },
                " -s ",
                {
                  "Ref": "AWS::StackId"
                },
                " --region ",
                {
                  "Ref": "AWS::Region"
                }
              ]
            ]
          }
        }
      }
    }
  }
}

```

