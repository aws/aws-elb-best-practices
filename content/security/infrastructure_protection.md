# Infrastructure Protection

Infrastructure protection is one of the areas of the [Security Pillar of the AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/infrastructure-protection.html){:target="_blank"}. It ensures that systems and services within your workload are protected against unintended and unauthorized access, and potential vulnerabilities. This section outlines recommendations for [Distributed Denial of Service (DDoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack){:target="_blank"} resilience and security groups.

---

## Distributed Denial of Service (DDoS) Protection

Every ELB is automatically protected by AWS Shield standard, which is a managed distributed denial of service (DDoS) protection service. AWS Shield Standard provides protection against the most common and frequently occurring infrastructure (layer 3 and 4) attacks, such as  SYN/UDP floods, reflection attacks, and others to support high availability of your applications on AWS.

Additionally, Application Load Balancer (ALB) also provides additional protection at layer 7 when using HTTP/HTTPS listeners:

- They will not forward mal-formed HTTP Requests (don’t meet HTTP RFC specification).
- They offer protection against certain types of HTTP slow attacks.

Furthermore, ELB also :

- Reduce the risk of overloading your application by distributing traffic across many target instances.
- Automatically scales based on traffic received, and than can include DDoS traffic. Customers should plan for target scaling, see [Plan for Scale](/security/infrastructure_protection/#plan-for-scale).
- [Can integrate with Shield Advance](/security/infrastructure_protection/#consider-using-aws-shield-advanced)
- [Can integrate with AWS WAF](/security/infrastructure_protection/#consider-using-aws-waf-alb-only)

!!! abstract "References and Further Reading"

    [Best practices for DDoS mitigation](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/best-practices-for-ddos-mitigation.html#elastic-load-balancing-bp6){:target="_blank"}

    [AWS Best Practices for DDoS Resiliency](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/welcome.html){:target="_blank"}

---

### Consider using AWS Shield Advanced

By default, ALB comes with AWS Shield Standard, which provides all AWS customers with protection against common and most frequently occurring infrastructure (layer 3 and 4) attacks like SYN/UDP floods, reflection attacks, and others to endure high availability of your applications on AWS.

Some customers are regularly targeted by DDoS attacks or may have strict compliance requirements to mitigate attacks. For customers requiring enhanced protection against more sophisticated, frequent and larger attacks, it is suggested enabling [AWS Shield Advanced](https://aws.amazon.com/shield/){:target="_blank"}. 

AWS Shield Advanced offers advanced attack mitigation, 24x7 access to the Shield Response Team (SRT) and cost protection for scaling.

!!! tip "Best Practice"
--8<-- "alb-bp-sec07.md"

!!! abstract "References and Further Reading"

    [AWS Shield Advanced](https://aws.amazon.com/shield/){:target="_blank"}

---

### Security Group - Flow tracking (ALB only)

Security groups attached to the ALB use connection tracking to monitor traffic to and from the load balancer. Enhance the DDoS resilience of your load balancer by configuring it to not require EC2 connection tracking. If a security group rule allows TCP or UDP flows from all traffic (0.0.0.0/0 or ::/0) to the listening port (80, 443, etc.), and there is a matching rule in the opposite direction that permits all response traffic (0.0.0.0/0 or ::/0) for all ports (0-65535) on both TCP and UDP, then that flow of traffic is not tracked. This helps to prevent potential negative effects of this feature on the load balancer’s packet throughput, enabling it to detect and scale based on the increase in traffic during a DDoS event.

Example of a security group allowing untracked flows for connections to the port 443:

|**Ingress Rule**|||
|:---|:---|:---|
|Protocol|Port|Source|
|TCP|443|0.0.0.0/0|
|**Egress Rule**|||
|Protocol|Port|Destination|
|TCP|0-65535|0.0.0.0/0|


!!! tip "Best Practice"
--8<-- "alb-bp-sec08.md"

!!! abstract "References and Further Reading"
    [Best practices for DDoS mitigation - Elastic Load Balancing (BP6)](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/best-practices-for-ddos-mitigation.html#elastic-load-balancing-bp6){:target="_blank"}


    [Security group connection tracking](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-connection-tracking.html){:target="_blank"}


    [Security group - Untracked connections](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-connection-tracking.html#untracked-connections){:target="_blank"}

---

### Know normal behavior (Traffic pattern, user agents, demographics)

In the event of a DDoS attack, distinguishing between normal and abnormal traffic is crucial. To do so, an understanding of what constitutes ‘normal’ is essential.

To profile typical traffic, consider the following aspects:

- **Traffic patterns:** What are the typical fluctuations in your traffic throughout the day? For instance, a food delivery company may see a surge in traffic around lunch time and significantly less activity in the early hours of the day. 
- **User agents:** What are the usual user agents connecting to your load balancer? These could be common web browsers or specific applications.
- **Demographics:** Where are the clients accessing your load balancer typically located?

Significant deviation from these norms could indicate a potential attack, providing valuable information for mitigation strategies. For example, you could use [AWS WAF](/security/infrastructure_protection/#consider-using-aws-waf-alb-only) to block access from some specific countries if you identify unusual traffic from those locations.

!!! tip "Best Practice"
--8<-- "alb-bp-sec09.md"

!!! abstract "References and Further Reading"

    [Access Logs](https://w.amazon.com/bin/view/ELB/Teams/CSET/ELB_Best_Practices_Guides/Security/#HAccessLogs){:target="_blank"}

    [Monitor your Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-monitoring.html){:target="_blank"}

    [Monitor your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-monitoring.html){:target="_blank"}

    [Best practices for DDoS mitigation - Metrics and alarms](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/metrics-and-alarms.html){:target="_blank"}

---

### Plan for Scale

Scaling to absorb is one of the mitigation techniques that can be used against a DDoS attack. While the ELB will automatically scale to manage the additional traffic, you will need to configure your targets for the same. Using an [Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html){:target="_blank"}, you can set scaling policies based on resource usage of your EC2 instance targets, and integrate with ELB to automatically register the new instances with the load balancer. 

It’s important to ensure you have enough free IP addresses in both ELB and target subnets to accommodate scaling, and that you have sufficient EC2 quota to launch the desired number of EC2 instances.

!!! tip "Best Practice"
--8<-- "alb-bp-sec10.md"

!!! abstract "References and Further Reading"

    [What is Amazon EC2 Auto Scaling?](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html){:target="_blank"}

    [Use Elastic Load Balancing to distribute traffic across the instances in your Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html){:target="_blank"}

---

### Consider using AWS WAF (ALB only)

ALB can be integrated with [AWS WAF (Web Application Firewall)](https://aws.amazon.com/waf/){:target="_blank"} , allowing you to filter and block requests based on specific request signatures. With WAF, you can create Web Access Control Lists (ACLs) with custom rules, and also utilize AWS Managed rules. For instance, the [Amazon IP Reputation List rule](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-ip-rep.html){:target="_blank"} group includes rules based on Amazon's internal threat intelligence, allowing for further protection of your applications against potential threats.

!!! tip "Best Practice"
--8<-- "alb-bp-sec11.md"

When using WAF, implement rate-based rules for better protection against Layer 7 HTTP flood attacks. The blog post ["The three most important AWS WAF rate-based rules"](https://aws.amazon.com/blogs/security/three-most-important-aws-waf-rate-based-rules/){:target="_blank"} is a great reference based on the learnings of AWS’ Shield Response Team (SRT).

!!! tip "Best Practice"
--8<-- "alb-bp-sec12.md"


!!! abstract "References and Further Reading"

    [Application layer defense](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/application-layer-defense-bp1-bp2.html){:target="_blank"}

    [AWS Web Application Firewall](https://aws.amazon.com/waf/){:target="_blank"}

    [Amazon IP Reputation List rule](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-ip-rep.html){:target="_blank"}

    [The three most important AWS WAF rate-based rules](https://aws.amazon.com/blogs/security/three-most-important-aws-waf-rate-based-rules/){:target="_blank"}

    [AWS Config Rule alb-waf-enabled](https://docs.aws.amazon.com/config/latest/developerguide/alb-waf-enabled.html){:target="_blank"}

---

### Consider using Amazon CloudFront or AWS Global Accelerator

ELB can integrate with [Amazon CloudFront](https://aws.amazon.com/cloudfront/){:target="_blank"} or [AWS Global Accelerator](https://aws.amazon.com/global-accelerator/){:target="_blank"}, which can serve as entry points for your web application.

Both Amazon CloudFront and AWS Global Accelerator uses [AWS Edge locations](https://aws.amazon.com/cloudfront/features/?p=ugi&l=ap&whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc){:target="_blank"}. These edge locations provide an additional layer of network infrastructure and can increase your ability to optimize latency and throughput to users, but also enhances your application resilience against DDoS attacks.

!!! tip "Best Practice"
--8<-- "alb-bp-sec13.md"

!!! abstract "References and Further Reading"
    
    [Amazon CloudFront](https://aws.amazon.com/cloudfront/){:target="_blank"}
    
    [AWS Global Accelerator](https://aws.amazon.com/global-accelerator/){:target="_blank"}

    [AWS Global Edge locations](https://aws.amazon.com/cloudfront/features/?p=ugi&l=ap&whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc){:target="_blank"}

    [Use AWS Edge locations for scale](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/use-aws-edge-locations-for-scale-bp1-bp3.html){:target="_blank"}

---

### When using CloudFront, restrict the direct access to the load balancer

Prevent users from bypassing [Amazon CloudFront](https://aws.amazon.com/cloudfront/){:target="_blank"} and accessing your load balancer directly. You can configure Amazon CloudFront and your Application Load Balancer to prevent users from directly accessing the load balancer by [configuring CloudFront to add a custom HTTP header](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/restrict-access-to-load-balancer.html){:target="_blank"} to the requests that it sends to your origin. In the ALB you then configure a rule to validate the existance of the header.

This allows users to access the Application Load Balancer only through CloudFront, ensuring that you get the benefits of using CloudFront.

!!! tip "Best Practice"
--8<-- "alb-bp-sec21.md"

Additionally, you should [lock down the security group associated with the load balancer used as the origin](https://aws.amazon.com/blogs/networking-and-content-delivery/limit-access-to-your-origins-using-the-aws-managed-prefix-list-for-amazon-cloudfront/), ensuring it accepts connections only from CloudFront.

!!! tip "Best Practice"
--8<-- "alb-bp-sec22.md"


!!! abstract "References and Further Reading"
    [Restricting access to Application Load Balancers](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/restrict-access-to-load-balancer.html){:target="_blank"}
    
    [Limit access to your origins using the AWS-managed prefix list for Amazon CloudFront](https://aws.amazon.com/blogs/networking-and-content-delivery/limit-access-to-your-origins-using-the-aws-managed-prefix-list-for-amazon-cloudfront/){:target="_blank"}
---

## Target Security Groups

To ensure your targets receive traffic exclusively from the load balancer, restrict the security group(s) associated with your targets to accept traffic solely from the load balancer. This can be achieved by setting the load balancer's security group as the source in the ingress rule of the target's security group.

!!! tip "Best Practice"
--8<-- "alb-bp-sec06.md"
