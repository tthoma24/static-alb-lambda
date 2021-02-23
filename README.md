This function checks the DNS records for an internal Application Load Balancer IP addresses.
It populates a Network Load Balancer's target group with Application Load Balancer's IP addresses

WARNING: This function perform multiple DNS looks per each invocation. It is not guaranteed that all
Application Load Balancer IP will be detected by a single invocation. However, the result converges
when more invocations are triggered. This function perform registration aggressively
and deregistration cautiously.

Configure these environment variables in your Lambda environment (CloudFormation Inputs)
1. ALB_DNS_NAME - The full DNS name of the internal Application Load Balancer
2. ALB_LISTENER - The traffic listener port of the internal Application Load Balancer
3. S3_BUCKET - Bucket to track changes between Lambda invocations
4. NLB_TG_ARN - The ARN of the Network Load Balancer's target group
5. MAX_LOOKUP_PER_INVOCATION - The max times of DNS look per invocation
6. INVOCATIONS_BEFORE_DEREGISTRATION  - Then number of required Invocations before a IP is deregistered
7. CW_METRIC_FLAG_IP_COUNT - The controller flag that enables CloudWatch metric of IP count

Credit: https://aws.amazon.com/blogs/networking-and-content-delivery/using-static-ip-addresses-for-application-load-balancers/