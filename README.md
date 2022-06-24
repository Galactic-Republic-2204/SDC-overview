# Backend System Desigin 

## Description

* Redesigned and scaled the backend of online retailer to handle 1M products with 10k RPS
* Designed and updated database schema for products information, product styles, products inforamtion, product photos and skus and updated tabels with indexing which improved 200% of RPS.
* Optimized PostgreSQL queries with aggregate functions and decreased queries timing to 30ms from 86ms.
* Achieved about 1000% RPS increment by identifying bottlenecks with k6 and loader.io, and horizontal scaling the backend with Nginx, catching and 3 AWS EC2 instances 


## Testing
Local Test: K6, chakram
Deployed: Loader.io

## Whole System Design

![Screen Shot 2022-06-23 at 8 55 39 PM](https://user-images.githubusercontent.com/78040879/175459187-cf6d19c9-6262-416e-bdfc-5dc44decc8b1.png)
