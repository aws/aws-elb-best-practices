# Incident Response

Incident response is one of the areas of the [Security Pillar of the AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/incident-response.html){:target="_blank"}. It emphasises the preparation required for security teams to operate effectively during an event. This section provides recommendations on logging that could be used for forensic purposes and how to engage with AWS during such events.

---

## Access Logs

Access logs offer detailed insights into the requests that reach the load balancer. These details are important during a troubleshooting or security event. Note that [ALB Access Logs](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-access-logs.html){:target="_blank"} or [NLB TLS Access Logs](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-access-logs.html){:target="_blank"} are not enabled by default, and enabling it will incur S3 storage costs.

!!! tip "Best Practice"
--8<-- "alb-bp-sec15.md"

The destination for the ALB or NLB logs is an S3 bucket. In multi-account environments, it’s recommended to consolidate the logs into a centralised account. This approach allows for the application of  security controls to protect the confidentiality and integrity of the logs.

!!! tip "Best Practice"
--8<-- "alb-bp-sec16.md"

Having the logs in a centralised location not only enhances security but also simplifies integration with tools for log analysis. From these logs, you can extract valuable insights such as Top Requesters, Average Request Size, and most-used TLS Ciphers.

!!! tip "Best Practice"
--8<-- "alb-bp-sec20.md"



!!! abstract "References and Further Reading"

    [Enable access logs for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/enable-access-logging.html){:target="_blank"}

    [Access logs for your Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-access-logs.html){:target="_blank"}

    [Application and Classic Load Balancers logging should be enabled](https://docs.aws.amazon.com/securityhub/latest/userguide/elb-controls.html#elb-5){:target="_blank"}

    [AWS Config Rule elb-logging-enabled](https://docs.aws.amazon.com/config/latest/developerguide/elb-logging-enabled.html){:target="_blank"}

    [Security OU and accounts - Log archive account](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/security-ou-and-accounts.html#log-archive-account){:target="_blank"}

    [Security OU – Log Archive account](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/log-archive.html){:target="_blank"}

    [Querying Application Load Balancer logs](https://docs.aws.amazon.com/athena/latest/ug/application-load-balancer-logs.html){:target="_blank"}

    [Querying Network Load Balancer logs](https://docs.aws.amazon.com/athena/latest/ug/networkloadbalancer-classic-logs.html){:target="_blank"}

    [Step by step for Log Analysis with Amazon Athena](https://github.com/aws/elastic-load-balancing-tools/tree/master/amazon-athena-for-elb){:target="_blank"}

    [CDK & CloudFormation samples for Log Analysis with Amazon Athena](https://github.com/aws/elastic-load-balancing-tools/tree/master/log-analysis-elb-cdk-cf-template){:target="_blank"}

---

## Events

ELB Service events and changes are notified via AWS Health. Customers should proactively monitor AWS Health in order to action whenever there is a communication from AWS. Also, consulting AWS Health Dashboard should be part of the playbook for incident response.

!!! tip "Best Practice"
--8<-- "alb-bp-sec17.md"

!!! abstract "References and Further Reading"

    [What is AWS Health?](https://docs.aws.amazon.com/health/latest/ug/what-is-aws-health.html){:target="_blank"}

    [Use a process for event, incident, and problem management](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_event_response_event_incident_problem_process.html){:target="_blank"}

---

## Engage AWS Security

Knowing how to engage AWS Security can help during an active security event. AWS has a variety of security channels that can be used:


* AWS Security: aws-security@amazon.com
* [AWS Customer Incident Response Team](https://aws.amazon.com/blogs/security/welcoming-the-aws-customer-incident-response-team/){:target="_blank"}
* [AWS Shield Response Team (SRT) / DDoS response support](https://docs.aws.amazon.com/waf/latest/developerguide/ddos-responding.html#ddos-responding-contact-support){:target="_blank"}
* [Vulnerability Reporting](https://aws.amazon.com/security/vulnerability-reporting/){:target="_blank"}
* [Abuse Reporting](https://support.aws.amazon.com/#/contacts/report-abuse){:target="_blank"}
* [AWS Compliance Information](https://pages.awscloud.com/compliance-contact-us.html){:target="_blank"}
* [Testing / Simulated Events Form](https://support.console.aws.amazon.com/support/contacts#/simulated-events){:target="_blank"}


!!! tip "Best Practice"
--8<-- "alb-bp-sec18.md"

!!! abstract "References and Further Reading"

    [AWS Customer Incident Response Team](https://aws.amazon.com/blogs/security/welcoming-the-aws-customer-incident-response-team/){:target="_blank"}

    [Understand AWS response teams and support](https://docs.aws.amazon.com/whitepapers/latest/aws-security-incident-response-guide/understand-aws-response-teams-and-support.html){:target="_blank"}
