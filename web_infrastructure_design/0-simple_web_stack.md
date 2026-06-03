<img width="164" height="150" alt="simple_web_stack_0" src="https://github.com/user-attachments/assets/c1ecbbc3-5ffa-4fae-b994-e1df7b111330" />


What is a server?
A device or program that provides services/resources to other machines called clients.
Role of the domain name
foobar.com is a human-readable alias. Without it, users would need to type 8.8.8.8 directly. It maps a name to an IP address.
What type of DNS record is www?
It's an A record — it maps the hostname www.foobar.com to the IPv4 address 8.8.8.8.
Role of the web server (Nginx)
Receives incoming HTTP requests. Serves static files directly (HTML, CSS, images). Forwards dynamic requests to the application server.
Role of the application server
Executes the application logic (e.g. PHP, Python, Ruby). Processes the request, queries the database if needed, and returns a dynamic response to Nginx.
Role of the database (MySQL)
Stores, organizes, and retrieves persistent data (users, posts, orders…). The app server queries it via SQL.
Protocol used to communicate with the user's computer
HTTP (or HTTPS) over TCP/IP.

Issues with this infrastructure:

SPOF (Single Point of Failure) — there is only one server. If it crashes, the entire website goes down.
Downtime on maintenance — deploying new code requires restarting Nginx/the app server, making the site temporarily unavailable.
Cannot scale — if traffic spikes, a single server has a hard ceiling on CPU/RAM. There is no load balancer or second server to distribute the load.
