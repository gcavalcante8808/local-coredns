<h1 align="center"><code>Local CoreDNS</code></h1>
<div align="center">
  <a href="https://www.buymeacoffee.com/gcavalcante8808">
    <img src="https://img.shields.io/badge/-buy_me_a%C2%A0coffee-gray?logo=buy-me-a-coffee" alt="buy me a coffee">
  </a>
</div>

A local coredns docker-compose stack. I use it mainly to block ads and cache DNS on my machines.

### Requirements

Docker/Podman and docker-compose installed and running. I use a rootless docker on my daily operations but it should work with docker daemon too.

### How to Install/Use

1. Clone the repository to a local directory - Personally I prefer to clone it directly to `/etc/coredns`;
2. Enter in the directory and run the command `docker compose up -d`;
3. [SYSTEMD USERS ONLY] Update the file `/etc/systemd/resolved.conf` DNS Configuration as following:

```
[Resolve]
DNS=127.0.0.253
```

4. Run `systemctl restart systemd-resolved`;
5. Check if the changes were applied by running the command `systemctl-resolve --status`:
   
   ```
   Global
            Protocols: LLMNR=resolve -mDNS -DNSOverTLS DNSSEC=no/unsupported
     resolv.conf mode: stub
   Current DNS Server: 127.0.0.253
          DNS Servers: 127.0.0.253 127.0.0.253
   
   ```
   
   

#### Useful notes

a. You can see the queries issued by checking the logs of the coredns container using the command `docker logs coredns`.

b. There are some nice metrics available at `http://127.0.0.1:9153/metrics`.

If you're like me and prefer to use the DNS to block ads and other stuff, you can write any hosts that you want to **block** into the hosts file that lies in the same directory as the docker-compose.

> My preferred deny list is the `StevenBlack/hosts` lists that can be downloaded from `https://github.com/StevenBlack/hosts`.

#### Author

Author: Gabriel Abdalla Cavalcante Silva (gabriel.cavalcante88 at gmail.com)


