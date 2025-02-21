# Managing software, system and network

### Using `apt`, `apt-get`, `dpkg`, … manage package update, install, remove software (nginx, apache2, sql, …). 

Amazon Linux uses `yum`/`dnf`, thus this section will focus on that.

`dnf` automatically refreshes its update cache every time you interact with the package manager, so running `dnf update` is unnecessary. However, on other package managers, this is not a thing, so commands like `apt update` should be done before doing anything else. This report will include running an update check for clarity's sake.

- Refresh the update cache (unnecessary with `dnf`, included for clarity)

<img src=images/lab-2/image-1.png width=500>

- Check installed packages, `grep` to find a specific one

<img src=images/lab-2/image-2.png width=500>

- `nginx` is not installed, check available packages for nginx

<img src=images/lab-2/image-3.png width=500>

- Installing `nginx`. `-y` is optional and will skip confirmation.

<img src=images/lab-2/image-4.png width=500>

- Removing `nginx`

<img src=images/lab-2/image-5.png width=500>

- Updating a package (like `tree`)

<img src=images/lab-2/image-6.png width=500>

### Managing system (task, service, …) use tool: `ps`, `top`, `htop`, `kill`, `grep` process.

- Listing all running processes within current user's scope:

<img src=images/lab-2/image-7.png width=300>

- Listing all processes from all users that matches a keyword

<img src=images/lab-2/image-8.png width=500>

- Showing processes which are most system intensive at the moment

<img src=images/lab-2/image-9.png width=500>

- Alternatively with a more graphic, interactive menu using `htop`

<img src=images/lab-2/image-10.png width=500>

### Managing network (IP, port, display network, domain, …) use tool: `netstat`, ...

- Using `netstat` shows all internet, UNIX domain (internal) and Bluetooth connections. Focusing on the internet connections, there's the current ssh connection used to connect to this EC2 instance:

<img src=images/lab-2/image-11.png width=500>

- Showing the routing table

<img src=images/lab-2/image-12.png width=500>

- Showing interfaces and multicast groups

<img src=images/lab-2/image-13.png width=500>