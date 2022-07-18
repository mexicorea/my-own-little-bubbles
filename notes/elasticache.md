---
tags: aws cache in-memory database redis memcached
---

# Elasticache

## warnings

1. 기본적으로 VPC 내부 사용으로 설정되어 있다. RDS instance 만들 때처럼 internet-facing option 같은 것 없음.
2. 외부에서 접근하는 게 아예 방법이 없는 건 아니지만, VPN을 이용해야 가능.

> Your Amazon ElastiCache instances are designed to be accessed through an Amazon EC2 instance.
> Elasticache is a service designed to be used internally to your VPC. External access is discouraged due to the latency of Internet traffic and security concerns. However, if external access to Elasticache is required for test or development purposes, it can be done through a VPN.
> - https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/accessing-elasticache.html
