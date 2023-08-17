## Cloud Computing

![[Cloud Computing]]
## Pricing

- AWS pricing fundamentals:
    - **Compute**
    - **Storage**
    - **Data transfer** - pay only for data transferred *out* of the cloud
## Shared Responsibility Model

> [!quote] Shared Responsibility Model
> Security and Compliance is a shared responsibility between AWS and the customer.

![Shared Responsibility Model](Assets/Images/aws.shared-responsibility-model.jpg)
- **Source**: [AWS](https://aws.amazon.com/compliance/shared-responsibility-model/) 
## Concepts

### Regions

- Cluster of data centers
- Most AWS services are region-scoped.

**What determines where to launch a new service?**
- ==Compliance== - Data never leaves a region w/o explicit permission
- ==Customer Proximity== - Reduced latency
- ==Service Availability== - Not all services are available in every region 
- ==Pricing== - Varies from region to region

### Availability Zones (AZ)

- Within each region, there are several separate yet connected availability zones, usually anywhere from 3 to 6.
- Each AZ contains one or more data centers, each with redundant power, networking and connectivity.
- AWS Region: Sydney (ap-southeast-2)
    - ap-southeast-2a, ap-southeast-2b, ap-southeast-2c
### Points of Presence (Edge Locations)

- Deliver content to end users with low latency. 
- 400+ in 90+ cities across 40+ countries.


## Services

- **Global**: IAM, Route 53, CloudFront, WAF
- **Regional**: EC2, Elastic Beanstalk, Lambda, Rekognition
### Global
#### Identity and Access Management (IAM)

- Root account is created by default and associated with an organization.
- Users
    - People within an organization 
    - Can be grouped
    - Can belong to multiple groups
    - Don't necessarily have to be part of a group
- Groups
    - Only contain users, not other groups
- Policies
    - JSON documents that define permissions
    - Assigned to users (Inline) or groups 
    - **Policy Structure**
        - `Version` - Policy language version (2012-10-17)
        - `Id` - Optional Policy identifier
        - `Statement` - One or more (required)
            - `Sid` - Optional statment identifier
            - `Effect` - '`Allow`' or '`Deny`' access
            - `Principal` - account/user/role to which the policy is applied
            - `Action` - list of allowed or denied actions
            - `Resource` - list of resources the actions apply to
            - `Condition` - Optional conditions that determine when the policy is in effect

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AttachVolume",
                "ec2:DetachVolume"
            ],
            "Resource": "arn:aws:ec2:*:*:instance/*",
            "Condition": {
                "StringEquals": {"aws:ResourceTag/Department": "Development"}
            }
        }
        ...
    ]
}
```


## Further

### Learn 🧠

- [AWS Cloud Solutions Architect Professional Certificate - Coursera](https://www.coursera.org/professional-certificates/aws-cloud-solutions-architect)

- [Ultimate AWS Certified Developer Associate 2023 NEW DVA-C02](https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/)

- [Ultimate AWS Certified Solutions Architect Associate SAA-C03 - Udemy](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/)