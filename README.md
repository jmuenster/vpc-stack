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

[ <img src="https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png" alt="Launch stack image" style="height: 10;"/> ](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=vpc-stack&templateURL=https://s3-us-west-2.amazonaws.com/jmuenster-public-templates/vpc-stack/template.json)

Or as a nested stack:

```javascript
"NetworkStack": {
  "Type": "AWS::CloudFormation::Stack",
   "Properties": {
     "Parameters": { "CidrBlockPrefix": "10.10.10" },
     "TemplateURL": "https://s3-us-west-2.amazonaws.com/jmuenster-public-templates/vpc-stack/template.json",
     "TimeoutInMinutes": "10"
  }
},
```

A few caveats:

- This doesn't work in regions with two availability zones, for obvious reasons
- Availability zone are mapped on a [per account(https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions-availability-zones)] basis, so you won't always have an a, b and c AZ name.  If this is the case, use the ZoneId parameters to override the default settings

