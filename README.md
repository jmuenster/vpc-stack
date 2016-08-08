# AWS Vpc Cloudformation Stack

This template creates the following:

- a /24 vpc
- 3 * /26 private subnets
- 3 * /28 public subnets
- 3 * nat gateways
- an internet gateway
- an s3 endpoint
- the plumbing to connect the above

It can be used standalone: 
[ <img src="https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png" alt="Launch stack image" style="height: 10;"/> ](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=jenkins-stack&templateURL=https://s3-us-west-2.amazonaws.com/jmuenster-public-templates/jenkins-stack/template.json)

Or as a nested stack:

```javascript
"NetworkStack": {
  "Type": "AWS::CloudFormation::Stack",
   "Properties": {
     "Parameters": {
       "FirstOctet": "10",
       "SecondOctet": "10",
       "ThirdOctet": "120"
     },
     "TemplateURL": "https://s3-us-west-2.amazonaws.com/jmuenster-public-templates/vpc-stack/template.json",
     "TimeoutInMinutes": "10"
  }
},
```

