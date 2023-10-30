# Data Protection

Data protection is one of the areas of the [Security Pillar of the AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/data-protection.html){:target="_blank"}. It recommends encrypting all data in transit. This section outlines recommendations for using TLS (with NLB) or HTTPS (with ALB) to ensure data is protected while in transit.

TLS stands for 'Transport Layer Security' and it is a sucessor of the SSL (Secure Sockets Layer). Both TLS and SSL terms are often used interchangeably, in this guide we will be using the term TLS to refer to both. HTTPS stands for 'Hypertext Transfer Protocol Secure'. It is the HTTP protocol trasmitted over a TLS session.

---

## TLS Listeners

[Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security){:target="_blank"} is a cryptographic protocol that secures internet communications. Implementing TLS for your application ensures that data remains confidential while in transit. By using an HTTPS or TLS listener on your load balancer, you offload the computational overhead and the security aspects of this encryption to the load balancer itself. When using HTTPS/TLS listeners, both ALB and NLB implement TLS  termination and negotiation on the front-end connection, which is from the client to the load balancer. From the load balancer to the target, you can opt for either HTTPS for end-to-end encryption or plain HTTP if you intend to offload TLS to the load balancer.

!!! tip "Best Practice"
--8<-- "alb-bp-sec01.md"

**(ALB only)**
If you need to provide a HTTP endpoint, the recommended approach is to create a redirection rule from HTTP to HTTPS for your plain HTTP listener. This avoids the need to enable plain HTTP on your targets.
!!! tip "Best Practice"
--8<-- "alb-bp-sec02.md"


!!! abstract "References and Further Reading"

    [Create an HTTPS listener for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-https-listener.html){:target="_blank"}

    [TLS listeners for your Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-tls-listener.html){:target="_blank"}

    [AWS Config rule alb-http-to-https-redirection-check](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html){:target="_blank"}

    [Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](https://docs.aws.amazon.com/securityhub/latest/userguide/elb-controls.html#elb-1){:target="_blank"}

---

### Security Policy for TLS Listeners
Security policies are configured for TLS listeners and determine which TLS protocols and ciphers are supported.

During a TLS handshake, both clients and the load balancer provide a list of ciphers and protocols in order of preference. The first cipher on the server’s list, defined by the security policy, that matches any of the client’s cipher is selected for communication.

There are several different security policies for both ALB and NLB. When using the AWS CLI to create a load balancer, the default policy is 'ELBSecurityPolicy-2016-08' which aims to maximize compatibility.

From a security perspective, it is recommended to remove any protocols and ciphers that are not in use in order to reduce the attack surface. Especially if you have control over the clients, you could configure them to use the latest TLS protocol (version 1.3) and a strict security policy in the load balancer such as 'TLS13-1-3-2021-06'. Conversely, if you don't have control over the clients connecting to the load balancer, which is commonly the case for public websites, it is recommended that you regularly review which protocols and ciphers are being used by legitimate clients and look for opportunities to deprecate old protocols. You can leverage [ALB Access Logs](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-access-logs.html){:target="_blank"} or [NLB TLS Access Logs](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-access-logs.html){:target="_blank"} to find the TLS version used in each request and, for example, search if outdated protocols, like TLS 1.0, are in use.

!!! tip "Best Practice"
--8<-- "alb-bp-sec04.md"

!!! abstract "References and Further Reading"

    [ALB Security Policies](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-https-listener.html#describe-ssl-policies){:target="_blank"}

    [NLB Security Policies](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-tls-listener.html#describe-ssl-policies){:target="_blank"}

    [Step by step for Log Analysis with Amazon Athena](https://github.com/aws/elastic-load-balancing-tools/blob/master/amazon-athena-for-elb){:target="_blank"}

    [CDK & CloudFormation samples for Log Analysis with Amazon Athena](https://github.com/aws/elastic-load-balancing-tools/blob/master/log-analysis-elb-cdk-cf-template){:target="_blank"}
---

## TLS Certificates

When using HTTPs or TLS listeners in your load balancer, you are required to provide a TLS certificate. Certificates consist of a public and private key. ELB integrates with AWS Certificate Manager which simplifies the creation and management of TLS certificates. This integration ensures private key protection and facilitates auditing for certificate use.

!!! tip "Best Practice"
--8<-- "alb-bp-sec03.md"

!!! abstract "References and Further Reading"

    [Implement secure key and certificate management](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_protect_data_transit_key_cert_mgmt.html){:target="_blank"}

    [AWS Config Rule elbv2-acm-certificate-required](https://docs.aws.amazon.com/config/latest/developerguide/elbv2-acm-certificate-required.html){:target="_blank"}
---

## TLS at the targets

Offloading TLS from targets to the load balancer it is a good practice from performance efficiency stand point. From the security perspective, if your targets are running inside the same VPC, the communication path is in a private network.

For cases where targets operate outside the VPC or for customers with compliance needs, end-to-end encryption might be beneficial. For that, customers can configure the Target Group with HTTPS(ALB) and TLS(NLB) protocols and set up TLS/HTTPS in the targets.

!!! tip "Best Practice"
--8<-- "alb-bp-sec05.md"

!!! abstract "References and Further Reading"

    [Infrastructure security in Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/infrastructure-security.html){:target="_blank"}