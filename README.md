# CloudFormation-style-guide
A style guide for AWS CloudFormation templates 

Guiding principles
===

- Be considerate to yourself and to other humans when writing software, and in this respect, the style considerations for CloudFormation templates are no different (in spirit) than the considerations for other kinds of software
- Aim for clarity and consistency, over brevity
- Good names serve to document the purpose

Template formats
===

- `YAML` shines over `JSON` in terms of expressiveness, and brevity. Here are some examples of [YAML wins!](examples/yaml_wins.md). OTOH, here are some examples of [JSON wins!](examples/json_wins.md)
- When in doubt, the easy availability of a capable text editor wins the argument. Having said that, most editors will _NOT_ flag indentation issues in a YAML template, whereas every JSON editor worth its salt _WILL_ flag a malformed JSON template!

Naming
====

- The notation that the CloudFormation service follows for `Type`, `Properties`, etc. is strictly [PascalCase](http://wiki.c2.com/?PascalCase), with names that begin with uppercase letters. We may follow the same convention, to the extent possible, for names to be chosen by template authors (such as the names of parameters, logical names for resources,  mappings, conditions, etc.)

For example, the public IP address for an EC2 instance is the return value `PublicIp` (and not ~~`PublicIP`~~)

```yaml
!Sub ${instance.PublicIp}

```

- Names for `Resources`
    - Logical names for resources begin with lowercase

- Names for `Parameters`
    - `Parameter` names begin with uppercase letters
    - When a `Parameter` will be used directly (or closely) as the value of a resource `Property`, choose the parameter name to match the property name

For example:

```yaml

Parameters:
  DesiredCapacity:
    Description: the desired capacity for the Auto Scaling Group configured for the fleet
    Type: Number

    
Resources:
  autoScalingGroup:
    Type: AWS::AutoScaling::AutoScalingGroup
    Properties:
      DesiredCapacity: !Ref DesiredCapacity

```

    - When the `Property` name does not communicate the intent, enhance the name of the `Parameter` to indicate the purpose

For example:

```yaml

Parameters:
  BucketName:
    Description: the name for the S3 bucket
    Type: String
    
Resources:
  bucket:
    Type: AWS::S3::Bucket
    Properties:
      Name: !Ref BucketName

```

- [work-in-progress]

Contributing
====

- For new content: When contributing a new style guideline (or an example to an existing style guideline), simply make the change inline to this `README.md` and submit a pull request
- For changes to content: If you wish to propose a change to the style guideline or a correction to an example, create an issue with a description indicating the guideline to modify, and provide the changed style guideline and any examples in the body of the issue
- All example CloudFormation snippets should be valid templates (or parts of valid templates)  
