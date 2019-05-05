## **Exporting Stack Output Values**

To share information between stacks, export a stack's output values. Other stacks that are in the same AWS account and region can import the exported values. For example, you might have a single networking stack that exports the IDs of a subnet and security group for public web servers. Stacks with a public web server can easily import those networking resources. You don't need to hard code resource IDs in the stack's template or pass IDs as input parameters.

To export a stack's output value, use the Export field in the Output section of the stack's template. To import those values, use the Fn::ImportValue function in the template for the other stacks.


**[parent.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/parent.json)** - Launches two nested stacks [child_asg.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/child_asg.json)n and [child_alb.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/child_alb.json).

**[child_alb.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/child_alb.json)** - Creates a [Application Load Balancer](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-loadbalancer.html) with [Target Group](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-targetgroup.html) and [Listener](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-listener.html) on port 80.

**[child_asg.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/child_asg.json)** - Creates a [Autoscaling Group](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-as-group.html), [Launch Configuration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-as-launchconfig.html) and a [Security Group](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-security-group.html) for the Instances to be launched via the AutoScaling Group. Also this stack imports the TargetGroup ARN and Load Balancer Security Group from the [child_alb.json](https://github.com/prshntattri1/CloudFormation/blob/master/Nested%20Stacks/using_export_import/child_alb.json) stack to associate the instances launched by the AutoScaling Group.


AWS Documentation
Exporting Stack Output Values - https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-exports.html
