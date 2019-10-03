# ElasticCace Redis Cluster Setup

This article will give over view of setting up Elasticcache-Redis cluster in AWS.

AWS-Elastic cache will support two caching services.

  1.  **Redis Cahce**
  2.  **Memcache**
  
Redis Cache  can be used as in-memory cache or database or message broker based on need.But its
specifically well known for in-memory cache implementation. It's used for most of the enterprise high
demand websites world wide.

<B>In AWS Redis Cluster is designed in such a way that it can be accessed from EC2 instance which is running on same
VPC in which Redis is created. So we need to make sure both Redis Cache and our EC2 instances are in same VPC.</B>

We can still access Redis cache from out side of EC2 and outside of AWS throug NAT instance/gateway but this kind of setup
is not recommanded.

Make sure you select specific region in which Redis needs to be created.

To setup follow below steps.

  1. Create/Launch an EC2 instance.
  2. Create a Redis cache from Elasticcache.
  3. Connect Redis cache from EC2 thorugh Redic-cli.

## 1. Create/Launch an EC2 instance

To Create/Launch an EC2 instance refer page below.

[Create/Launch EC2 instance] (https://github.com/uthircloud/aws/blob/master/EC2/README.md)

