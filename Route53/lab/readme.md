
# Create a health check
  * give your EC2 IP address 
  * give your hostname(domain)
  * give path e.g. /html or /php
  
# Bootstrap for Ec2
change x for your region of each EC2
```
#!/bin/bash
yum update -y
yum install httpd -y
chkconfig httpd on
service httpd start
cd /var/www/html
echo "<html><h1>Hello Cloud Gurus! This is the X Web Server</h1></html>" > index.html
```

# 1. Simple Routing Policy

  1. Goto Route 53
  2. Register a domain
  3. create three Ec2 instances in different regions
  4. in route53, goto hosted zones
  5. Goto record sets
  6. create record set
  7. enter your public IPs(3 Ec2 intances)
  8. Press Create
  
# 2. Weighted Routed Policy
  1. Goto Route 53
  2. goto hosted zones
  3. delete the A Record set
  4. Create three record sets with weights(20/30/50) and type weighted, reduce the TTL to one minute
  
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/4%20-%20weighted.PNG)
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/5%20-%20weighted.PNG)
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/6%20-%20weighted.PNG)

# 3. Latency Routed Policy
  1. Goto Route 53
  2. goto hosted zones
  3. delete the A Record set
  4. Create two record sets with different regions, reduce the TTL to one minute
  5. you can use a VPN Client to change location and test it
  
![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/7%20-%20Latency.PNG)
![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/8%20-%20Latency.PNG)


# 4. Failover Routed Policy
  1. Goto Route 53
  2. goto hosted zones
  3. delete the A Record set
  4. Create two record sets one primary and other secondary, reduce the TTL to one minute
  5. Assign a health check with each
  5. you can stop primary EC2 and test secondary will be up
  
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/9%20-%20Failover.PNG)
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/10%20-failover.PNG)

# 5. Geolocation Routed Policy
  1. Goto Route 53
  2. goto hosted zones
  3. delete the A Record set
  4. Create two record sets one europe and other north america, reduce the TTL to one minute
  5. Assign a health check with each
  5. you can stop primary EC2 and test secondary will be up
  
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/11%20-%20Geo.PNG)
  ![53](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/12%20-%20Geo.PNG)
  
 # 6. GeoProximity Routed Policy
   * you have to create a traffic flow(orchestration) 
   ![traffic](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/13%20-%20Traffic%20Flows.PNG)

 # 7. MultiValue Answer Policy
   * you have to create a traffic flow(orchestration) 
   
   ![traffic](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/14%20-%20Weighted.PNG)
   ![traffic](https://github.com/jawad1989/aws-solution-architect/blob/master/Route53/images/15%20-%20Weighted.PNG)
