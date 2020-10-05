#### aws iam 기본

aws에서 클라우드 리소스 사용자를 관리하는 시스템이다. EC2-support, EC2-admin, S3-support 그룹에 정책이 적용되어 있다. 예를 들면, 

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1399948319000",
            "Effect": "Allow",
            "Action": [
                "ec2:*"
            ],
            "Condition": {
                "StringEquals": {
                    "ec2:Region": "us-east-1"
                }
            },
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "Stmt1401047381000",
            "Effect": "Allow",
            "Action": [
                "autoscaling:*",
                "CloudFormation:*",
                "s3:*",
                "cloudwatch:*"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "Stmt1399948467000",
            "Effect": "Deny",
            "Action": [
                "ec2:AllocateHosts",
                "ec2:CreateCustomerGateway",
                "ec2:CreateInstanceExportTask",
                "ec2:CreatePlacementGroup",
                "ec2:CreateReservedInstancesListing",
                "ec2:PurchaseReservedInstancesOffering",
                "ec2:ModifyReservedInstances",
                "ec2:RequestSpotFleet",
                "ec2:CreateVpnConnection",
                "ec2:CreateVpnGateway",
                "ec2:ModifySpotFleetRequest",
                "ec2:RequestSpotInstances"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "Stmt1399948708000",
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:ApplySecurityGroupsToLoadBalancer",
                "elasticloadbalancing:AttachLoadBalancerToSubnets",
                "elasticloadbalancing:ConfigureHealthCheck",
                "elasticloadbalancing:CreateLoadBalancer",
                "elasticloadbalancing:CreateLoadBalancerListeners",
                "elasticloadbalancing:CreateLoadBalancerPolicy",
                "elasticloadbalancing:DeleteLoadBalancer",
                "elasticloadbalancing:DeleteLoadBalancerListeners",
                "elasticloadbalancing:DeleteLoadBalancerPolicy",
                "elasticloadbalancing:DeregisterInstancesFromLoadBalancer",
                "elasticloadbalancing:DescribeInstanceHealth",
                "elasticloadbalancing:DescribeLoadBalancerAttributes",
                "elasticloadbalancing:DescribeLoadBalancerPolicyTypes",
                "elasticloadbalancing:DescribeLoadBalancerPolicies",
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticloadbalancing:DetachLoadBalancerFromSubnets",
                "elasticloadbalancing:ModifyLoadBalancerAttributes",
                "elasticloadbalancing:RegisterInstancesWithLoadBalancer"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "DenyG2InstancesFromBeingCreated",
            "Effect": "Deny",
            "Action": [
                "ec2:RunInstances"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringEquals": {
                    "ec2:InstanceType": [
                        "g2.2xlarge",
                        "g2.8xlarge"
                    ]
                }
            }
        }
    ]
}
```

arn은 aws의 고유 식별자.

managed policy, inline policy는 마치 프로그래밍의 상속과 하드코딩의 차이같은 느낌. 

결론 : 리소스의 접근권한을 제어 -> 비용 관리