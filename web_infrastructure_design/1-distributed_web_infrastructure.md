
<img width="605" height="505" alt="Copie d&#39;écran_20260603_111805" src="https://github.com/user-attachments/assets/53016d0c-d694-4637-b42b-51f4c5120f99" />


Why each element is added
The load balancer (HAproxy) is added to distribute incoming traffic across multiple servers, avoiding overload on a single machine and improving availability. The two servers are added to handle requests in parallel and eliminate the single server SPOF from the previous infrastructure. The Primary-Replica database setup is added to separate read and write operations and protect data in case of a server failure.
Load balancer distribution algorithm
HAproxy is configured with Round Robin. Each incoming request is forwarded to the next server in order, cycling equally between server 1 and server 2. This ensures an even distribution of the load.
Active-Active vs Active-Passive
In our Active-Active setup, both servers are running and handling requests simultaneously. In an Active-Passive setup, one server handles all traffic while the second stays on standby and only takes over if the first one fails. Active-Active is more efficient but requires both servers to stay in sync.
How a Primary-Replica database cluster works
The Primary node receives all write operations (INSERT, UPDATE, DELETE). It then replicates the data to the Replica node in real time. The Replica node handles read-only queries (SELECT) to reduce the load on the Primary. If the Primary fails, the Replica can be manually promoted to become the new Primary.
Difference between Primary and Replica for the application
The application sends all write queries to the Primary node. Read queries can be sent to the Replica node to distribute the load. The Replica cannot accept writes — any attempt to write to it will fail.
Issues with this infrastructure

SPOF: the HAproxy load balancer is itself a single point of failure. If it goes down, the entire website becomes unreachable even though both servers are still running.
No firewall: the servers are directly exposed to the internet with no traffic filtering, making them vulnerable to attacks.
No HTTPS: traffic between the user and the website is not encrypted, meaning sensitive data can be intercepted.
No monitoring: there is no alerting system in place to detect failures, overload, or abnormal behavior on any component.
