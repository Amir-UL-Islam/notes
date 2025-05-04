
### SFTP & FTP

- FTP dose not encrypt user credential SFTP dose

### VPS & Shared Web Host

- In VPS you can get your own copy of OS
- VPS use Hypervisor
- You get Some Slice of Hardware that no one have access [But the system admin/owner of the VPS service company always can access your data] AWS ec2 is most popular
    - If you want more than that. Your have the option to set up personal server instead.

### Vartical Vs Horizontal Scaling

|Vartical|Horizontal|
|---|---|
|- Add More Resource li RAM, CPU etc.|- Architect the program accepting that our Resource is limit or hit the pic of budget.|
|- SATA drive < SAS drive < SSD|- Instead of Using Expensing Blazing fast Hardware Resource use cheap Hardware and share the traffic to multiple server|

### HTTP & DNS

|HTTP|DNS|
|---|---|
|It forms the basis for how web pages communicate from the web server to the client’s browser.|Domain Name System (DNS) plays a crucial role in the whole HTTP request process, as it allows us to call a webpage by typing a simple domain name, [www.medium.com](http://www.medium.com) instead of 104.16.121.127 every time you want to access the site.|
|Machines recognize the location of webpages by IP Addresses.|Without DNS, We need to remember every IP Addresses for every single website we use!|

### Load Balancer[ Man in the Middle]

Instead of retuning the Ip address from DNS return the IP Address of Load Balancer. And the Load Balancer will return the Ip Address of the Server that is free now.

- Load balancer have public Ip address[A public IP address is an address provided that is provided by your internet service provider (ISP) to your network.]

|Public IP|Private IP|
|---|---|
|A public IP address is an address provided that is provided by your internet service provider (ISP) to your network. On the internet, it recognizes your device. The internet is accessed through your router's public IP address. Public IP addresses are commonly used by publicly accessible enterprises such as websites, DNS, and VPN servers because they can be accessed from anywhere in the world. You can not go online without having your public IP address, which identifies your device on the internet. Your router is an intermediate between your computer and the internet on a typical home network.|A private IP address, also known as the local IP address, is the IP address your network router allocates to your device. This address is only visible within your network, so it is unavailable on the internet. Each device on the same network is assigned a unique private IP address that allows them to communicate with other devices. The device in your home can have the same private IP address as your neighbors' device or anyone else's all over the world, with private IP addresses. This is due to the non-routable nature of private addresses.|
|curl [http://ifconfig.me/](http://ifconfig.me/)|ipconfig getifaddr en0|

### Load Balancing Algorithm

- Software
    - Elastic Load Balancer
    - HAproxy
    - LVS
- Hardware
    - Barracuda
    - Cisco
    - Citrix

Algorithms

- Round Robin
    - Cons
        - By the nature of Round Robin will sequentially send used to server thought there might one server have exceed its’ limit.
- Session
    - Cons
        - Sessions are Server Specific. So let’s say server 1 have some session stored in (typically in tmp directory). But when Round Robin send you to server 2 or server X that server may not have your Session. So you might need to re login.
- RAID0, 1, 10, 5, 6

### MEMCache

### MySQL Query Cache
