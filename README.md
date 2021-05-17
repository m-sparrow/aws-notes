# AWS Notes

## Commonly Used Services
1. EC2 - Virtual Server | **Compute**
2. ECS - Container Engine for running containerised apps | **Compute**
3. Lambda - Function as a Service | **Compute** | **Serverless**
4. Elastic Beanstalk - Platform as a Sevice | **Compute**
5. AWS Batch - ?
6. EKS - Kubernetes Paltform | **Compute**

7. S3 - Object Storage | Often used to store docs, files, images and videos | **Storage**
8. EBS - Block Storage | Used as Hard Drive | **Storage**
9. EFS - File System | Used as Network File System | **Storage**
10. Storage Gateway - Mostly used to have application on premesis and data on cloud | **Storage**

11. RDS - Relational Database Solution | **Database**
12. Aurora - ?
13. DynamoDB - Something similar to MongoDB where data is saved in key-value pairs | **Database**
14. Keyspaces - NoSQL DB | Similar to Cassandra | **Database**
15. Neptune - Graph DB | Similar to Neo4J | **Database**

16. ElastiCache - Cache Implemntation | Redis or Memcache | **Cache** | **Database**
17. Redshift - ?

18. ElastiSearch - Implemtation of ELK STACK | **Application Logging** | **Analytics**
19. Secrets Manager - Manage secrets such as credentials | *Key Rotation** | **Keystore** | **Securtiy and Compliance** | **Cryptography**
20. Certificate Manager - Manage SSL certificates | Certificates generated through ACM works only within AWS network | Do not confuse with public certificate obtained from CA | **Security and Compliance**
21. IAM - Manage Users, User Groups, Roles, Policies (Trust Policy and Permission Policy) | **Security and Compliance**

22. VPC - Virtual Netwok within AWS account | **Networking**
23. Subnets - Sub networks within VPC | **Networking**
24. Security Groups - Logical firewall over EC2 instances | **Networking**
25. NACL - Logical firewall over Subnets | **Networking**
26. Internet Gateway - To connect to Internet | **Networking**
27. VPN - Enable private network between VPC and services such as S3 | The connectivity is established within AWS private network and not public internet | **Networking**
28. ELB - Loadbalancer Sevice | **Networking**
29. Route53 - DNS service | **Networking**
30. API Gateways - Often used with Lambda | Authentication is controlled through Cognito | **Networking**
31. CloudFront - Content Delivery Service | Something like Akamai | **Networking**
32. DirectConnect - Securely connect on premises network to VPC | **Networking**

33. ClouWatch - What happened (events) within services | **Monitoring**
34. CloudTrail - Who triggered (events) upon services | **Monitoring**

35. CloudFormation - IAC

36. Cognito - User Sign Up for web and mobile apps | **Authentication**

36. SNS - Pub-Sub Notifications | SMS | eMail | Mobile Push Notifications | **App Integration**
37. SES - Managed eMail Service | **App Integration**
38. SQS - Managed Queue Service | ActiveMQ | RabbitMQ | **App Integration**
39. MQ - Message Broker | Deploy MQ on cloud as it is without code changes | **App Integration**

40. SWF - Workflow service like JBPM or Drools | **App Integration**
41. Step Functions - Implement State Machines | **App Integration**

42. Kinesis - ?
43. Glue - ?
44. App Flow - ?
45. App Mesh - ?
46. Athena - ?
47. Config - ?
48. Shield - ?
49. WAF - ?
50. Audit Manager - ?
51. Firewall Manager - ?
52. Security Hub - ?
53. Macie - ?
54. License Manager - ?
55. Cloud HSM - ?
56. KMS - ?
57. App Config - ?
58. Health - ?
59. Systems Manager - ?
60. Cloud Map - ?
61. Event Bridge - Collects stream of data from various sources and pass in to other resources | Previously known as CloudWatch Events | **App Integration**

## How to create resources in AWS
Resources can be created through one of the following methods
1. Through AWS Management Console
2. Using AWS Client utility
3. Using AWS SDK
4. Using IAC tools such as CloudFormation, Terraform or similar IAC tools

## How to establish connectivity within AWS Resources
Connectivity can be classified into two types 
1. Connectivity between resources such as EC2 connecting to S3 or Lambda connecting to DynamoDB. Such connectivity is often achieved via IAM Roles.
2. Application running within a resource connecting to another resource. Such as a SpringBoot application running in EC2 connecting to RDS. It is often achieved through AWS SDK and user credentials.

## Credential provider chain
https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html

## Spring Boot, RDS, Secrets Manager, AWS SDK
https://github.com/aws/aws-secretsmanager-jdbc
 
## JBoss EAP on AWS Cloud
https://aws.amazon.com/de/blogs/germany/elastic-jboss-as-7-clustering-in-aws-using-ec2-s3-elb-and-chef/

## Key Repositories 
https://github.com/aws
https://github.com/awslabs

## How to manage Keystore and Truststore
It can be uploaded to AWS Secrets Manager depending on the size of JKS file. Best approach would be to upload the JKS file to private S3 bucket and it's password to AWS Secrets Manager. Then, download the JKS file from S3 Bucket into instance file system using aws client before starting the application.

## How to restart an EC2 instance when application goes hung resulting in high memory usage
1. Create a shell script which 
- takes thread dump 
- upload the thread dump to private S3 bucket using aws client
- Finally terminates the EC2 instance
2. Attach AutoScaling to bring replacement for terminated EC2 instance
3. Configure event for EventBridge which triggers RUN COMMAND from AWS Systems Manager
4. From AWS Systems Manager trigger the shell script (point 1)












