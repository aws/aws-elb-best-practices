# Home

This section provides best practices related to reliability and covers both [Application Load Balancer (ALB)](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html){:target="_blank"} and [Network Load Balancer (NLB)](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html){:target="_blank"}.

--8<-- "howtouse.md"


## Reliability Overview


Reliability is one of the pillares of the [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html){:target="_blank"}. To ensure reliability, a system must be resilient and designed to achieve its availability goals. This guide covers best practices for improved resilience against potential failures.

As with [Security](/aws-elb-best-practices/security), resilience is a shared responsibility between AWS and the customer. AWS is responsible for resilience at the load balancer level, while the customer is responsible for managing the targets. Customers are also responsible for configuring the load balancer and making design decisions to meet their availability goals.

At a high-level, the Elastic Load Balancing system will scale up/out the load balancer when needed, and automatically remove and replace any faulty nodes. Elastic Load Balancers are typically deployed to multiple EC2 Availability Zones, and utilize DNS to fail away from an impaired Availability Zone. This is because each ELB IP address has a Route 53 health check, that monitors the health of the load balancer nodes in the DNS record of the load balancer. This means that, if a node or AZ fails, the IP(s) will be removed from DNS.


!!! abstract "References and Further Reading"

    [Reliability Pillar - AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html){:target="_blank"}

    [Example implementations for availability goals](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/example-implementations-for-availability-goals.html){:target="_blank"}

    [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/){:target="_blank"}

## In this Guide

* [Failure Management](./failure_management)
* [Workload Architecture](./workload_architecture)

--8<-- "feedback.md"