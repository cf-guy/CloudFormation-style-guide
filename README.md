# CloudFormation-style-guide
A style guide for AWS CloudFormation templates 

Guiding principles
===

- Be considerate to yourself and to other humans when writing software, and in this respect, CloudFormation templates are no different
- Aim for clarity and consistency, over brevity
- Good names serve to document the purpose

Naming
====

- The notation that the CloudFormation service follows for `Type`, `Properties`, etc. is strictly camelCase, with names that begin with uppercase letters. We may follow the same convention, to the extent possible, for names that are to be chosen by template authors (such as the names of parameters, logical names for resources, names for mappings, conditions, etc.)

For example, the public IP address for an EC2 instance is the return value `PublicIp` (and not -`PublicIP`-)

```yaml
!Sub ${instance.PublicIp}

```
Resources
=====

- Logical names for resources begin with lowercase

Parameters
=====

- `Parameter` names begin with uppercase
- When a `Parameter` will be used directly (or closely) as the value of a resource `Property`, choose the parameter name to match the property name
- When the `Property` name does not communicate the intent, enhance the name of the `Parameter` to indicate the purpose

For example:

```yaml

Parameters:
  DesiredCapacity:
    Description: the desired capacity for the Auto Scaling Group configured for the fleet
    Type: Number

  ...
    
  Resources:
    autoScalingGroup:
      Type: AWS::AutoScaling::AutoScalingGroup
      Properties:
        DesiredCapacity: !Ref DesiredCapacity
    
  ... 

```

Contributing
====

- For new content: When contributing a new style guideline (or an example to an existing style guideline), simply make the change inline to this `README.md` and submit a pull request
- For changes to content: If you wish to propose a change to the style guideline or a correction to an example, create an issue with a description indicating the guideline to modify, and provide the changed style guideline and any examples in the body of the issue 
