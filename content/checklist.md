The section contains all best practices mentioned in the guide.

## Security

### Data Protection
- [x] 
--8<-- "alb-bp-sec01.md"
[(more details)](/aws-elb-best-practices/security/data_protection/#tls-listeners)

- [x] 
--8<-- "alb-bp-sec02.md"
[(more details)](/aws-elb-best-practices/security/data_protection/#tls-listeners)

- [x] 
--8<-- "alb-bp-sec04.md"
[(more details)](/aws-elb-best-practices/security/data_protection/#security-policy-for-tls-listeners)

- [x] 
--8<-- "alb-bp-sec03.md"
[(more details)](/aws-elb-best-practices/security/data_protection/#tls-certificates)

- [x] 
--8<-- "alb-bp-sec05.md"
[(more details)](/aws-elb-best-practices/security/data_protection/#tls-at-the-targets)

### Incident Response

- [x] 
--8<-- "alb-bp-sec15.md"
[(more details)](/aws-elb-best-practices/security/incident_response/#access-logs)

- [x] 
--8<-- "alb-bp-sec16.md"
[(more details)](/aws-elb-best-practices/security/incident_response/#access-logs)

- [x] 
--8<-- "alb-bp-sec20.md"
[(more details)](/aws-elb-best-practices/security/incident_response/#access-logs)

- [x] 
--8<-- "alb-bp-sec17.md"
[(more details)](/aws-elb-best-practices/security/incident_response/#events)

- [x] 
--8<-- "alb-bp-sec18.md"
[(more details)](/aws-elb-best-practices/security/incident_response/#engage-aws-security)

### Infrastructure Protection

- [x] 
--8<-- "alb-bp-sec07.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#consider-using-aws-shield-advanced)

- [x] 
--8<-- "alb-bp-sec08.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#security-group-flow-tracking-alb-only)

- [x] 
--8<-- "alb-bp-sec09.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#know-normal-behavior-traffic-pattern-user-agents-demographics)

- [x] 
--8<-- "alb-bp-sec10.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#plan-for-scale)

- [x] 
--8<-- "alb-bp-sec11.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#consider-using-aws-waf-alb-only)

- [x] 
--8<-- "alb-bp-sec12.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#consider-using-aws-waf-alb-only)

- [x] 
--8<-- "alb-bp-sec13.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#consider-using-amazon-cloudfront-or-aws-global-accelerator)

- [x] 
--8<-- "alb-bp-sec21.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#when-using-cloudfront-restrict-the-direct-access-to-the-load-balancer)

- [x] 
--8<-- "alb-bp-sec22.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#when-using-cloudfront-restrict-the-direct-access-to-the-load-balancer)

- [x] 
--8<-- "alb-bp-sec06.md"
[(more details)](/aws-elb-best-practices/security/infrastructure_protection/#target-security-groups)

### Security Assurance
- [x] 
--8<-- "alb-bp-sec19.md"
[(more details)](/aws-elb-best-practices/security/security_assurance/#automated-security-and-compliance-checks)

### Vulnerability Management

- [x] 
--8<-- "alb-bp-sec14.md"
[(more details)](/aws-elb-best-practices/security/vulnerability_management/#desync-mitigation-alb-only)

# Reliability

## Failure Management

- [x] 
--8<-- "alb-bp-rel09.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#health-check-depth)

- [x] 
--8<-- "alb-bp-rel10.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#health-check-interval-and-timeout)

- [x] 
--8<-- "alb-bp-rel11.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#fail-fast)

- [x] 
--8<-- "alb-bp-rel12.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#retrying-failed-requests-with-exponential-back-off-and-jitter)

- [x] 
--8<-- "alb-bp-rel07.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#use-dns-to-deliver-traffic-to-load-balancers)

- [x] 
--8<-- "alb-bp-rel08.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#use-dns-to-deliver-traffic-to-load-balancers)

- [x] 
--8<-- "alb-bp-rel13.md"
[(more details)](/aws-elb-best-practices/reliability/failure_management/#use-amazon-route-53-application-recovery-controller-for-zonal-shift)

## Workload Achitecture

- [x] 
--8<-- "alb-bp-rel01.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#use-multiple-availability-zones)

- [x] 
--8<-- "alb-bp-rel06.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#use-multiple-availability-zones)

- [x] 
--8<-- "alb-bp-rel02.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#availability-zone-independence-azi)

- [x] 
--8<-- "alb-bp-rel03.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#static-stability)

- [x] 
--8<-- "alb-bp-rel04.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#use-aws-global-accelerator)

- [x] 
--8<-- "alb-bp-rel05.md"
[(more details)](/aws-elb-best-practices/reliability/workload_architecture/#isolate-applications)
