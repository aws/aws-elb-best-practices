# Security Assurance

## Automated security and compliance checks

Cloud environments are dynamic by nature. Having automated security checks is important to make sure the existing and new load balancers will adhere to the controls defined by your organisation.

Both [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/){:target="_blank"} and [AWS Security Hub](https://aws.amazon.com/security-hub/){:target="_blank"} offers security and best practices [checks specific for ELBs](https://docs.aws.amazon.com/securityhub/latest/userguide/elb-controls.html){:target="_blank"}.

For example, you can enable AWS Security Hub to validate whether your ALBs have proper desync mitigation mode with the rule ["Application Load Balancer should be configured with defensive or strictest desync mitigation mode"](https://docs.aws.amazon.com/securityhub/latest/userguide/elb-controls.html#elb-12){:target="_blank"}



!!! tip "Best Practice"
--8<-- "alb-bp-sec19.md"

!!! abstract "References and Further Reading"

    [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/){:target="_blank"}

    [AWS Security Hub](https://aws.amazon.com/security-hub/){:target="_blank"}

    [AWS Security Hub - ELB Controls](https://docs.aws.amazon.com/securityhub/latest/userguide/elb-controls.html){:target="_blank"}

