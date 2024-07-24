## Storage decisions

There are two key decision problems to host files/videos/images

1. The storage needs to be scalable, reliable, available and cheap. That's why no one stores files in their own servers. It is a naive approach which convinced me that AllPeep does not have a strong engineering team. Services such as AWS S3 ensures data is replicated enough to ensure 99.99% uptime

2. Spam protection is a huge concern. Cloud services have built in protection rules which saves development and management cost.

Note: IPFS cannot be used for persistence. It works more like a CDN, data will be lost if not frequently used. Availability is another issue. To solve this many companies host their own Nodes (IPFS servers) which has the same problem of developing and managing your own cloud server. It would be very costly to develop and manage.
