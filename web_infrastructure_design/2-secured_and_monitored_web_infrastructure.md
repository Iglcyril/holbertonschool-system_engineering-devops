
<img width="701" height="646" alt="Copie d&#39;écran_20260603_112147" src="https://github.com/user-attachments/assets/8c9b3c3a-f982-47dc-9bc3-b47d590c81f3" />


Why each element is added
Three firewalls are added to filter and control incoming and outgoing traffic, one in front of the load balancer and one in front of each server. An SSL certificate is added to encrypt traffic between the user and the website. Three monitoring clients are added, one per machine, to collect metrics and send them to Sumologic.
What firewalls are for
Firewalls filter network traffic based on rules. They block unauthorized access, protect servers from attacks, and only allow legitimate traffic on defined ports (443 for HTTPS, etc).
Why traffic is served over HTTPS
HTTPS encrypts the data exchanged between the user's browser and the server using SSL/TLS. This prevents attackers from intercepting sensitive data such as passwords or personal information.
What monitoring is used for
Monitoring tracks the health, performance, and availability of each component. It sends alerts when something fails or behaves abnormally, allowing engineers to react quickly.
How the monitoring tool collects data
Each monitoring client runs as an agent on its server. It collects metrics (CPU, memory, logs, request counts) and sends them to Sumologic where they are aggregated and visualized.
How to monitor web server QPS
Configure the monitoring client to read Nginx access logs or expose Nginx status metrics. Set up a dashboard in Sumologic that counts the number of requests per second and triggers an alert if QPS exceeds a defined threshold.

Issues with this infrastructure

Terminating SSL at the load balancer means traffic between the load balancer and the backend servers is unencrypted. If an attacker gains access to the internal network, they can read the data in plain text.
Having only one MySQL server capable of accepting writes is a SPOF for all write operations. If the Primary goes down, no data can be written until a Replica is manually promoted.
Having all components (web server, app server, database) on the same machines means a resource spike in one component (e.g. the database) affects all others on the same server. It also makes scaling individual components impossible without scaling everything.
