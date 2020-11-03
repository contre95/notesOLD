

# Web Application Vulnerabilities

### OWASP

*https://owasp.org/*

The **Open Web Application Security Project** is an online community that produces freely-available articles, methodologies, documentation, tools, and technologies in the field of web application security

*Check OWASP Top 10*



## Tools and commands

### OWASP Juice Box

OWASP Juice Shop is probably the most modern and sophisticated insecure web application! It can be used in security trainings, awareness demos, CTFs and as a guinea pig for security tools! J

*https://github.com/bkimminich/juice-shop*

```shelll
docker run --rm -p 3000:3000 bkimminich/juice-shop
```



### Wapalyzer Docker

[Wappalyzer](https://wappalyzer.com/) is a cross-platform utility that uncovers the technologies used on websites. It detects [content management systems](https://wappalyzer.com/categories/cms), [ecommerce platforms](https://wappalyzer.com/categories/ecommerce), [web servers](https://wappalyzer.com/categories/web-servers), [JavaScript frameworks](https://wappalyzer.com/categories/javascript-frameworks), [analytics tools](https://wappalyzer.com/categories/analytics) and many more

```shell
docker run --rm wappalyzer/cli https://portal.antiplaganorte.com
```



### JSFuck

JSFuck is an esoteric and educational programming style based on the atomic parts of JavaScript. It uses only six different characters to write and execute code.

*http://www.jsfuck.com/*

**Some alternatives and similar tools to JSFuck are:**

- [Hieroglyphy](http://patriciopalladino.com/files/hieroglyphy/) (8 chars, browser only)
- [utf-8.jp](http://utf-8.jp/public/jsfuck.html) (broken)
- [JS-NoAlnum](http://discogscounter.getfreehosting.co.uk/js-noalnum.php) (broken)



### Nikto

*Source: https://github.com/sullo/nikto , https://cirt.net/Nikto2*

Nikto is a free software command-line vulnerability scanner that scans webservers for dangerous files/CGIs, outdated server software and other problems. It performs generic and server type specific checks. It also captures and prints any cookies received

```shell
docker run frapsoft/nikto -host https://lucascontre.site
```



### Enumerating Directories with Dirbuster

Discover directories for a given site.

```powershell
docker run --rm hypnza/dirbuster -u http://192.168.0.194 
```



### Enumerating  Ports and info with nmap

Get open ports (most commons are scanned) and more info about the host.

```bash
nmap -Pn 192.168.100.0/24
```

`-sP` flag skips port scanning.



### Enumerating SubDomains 

*Source: https://github.com/aboul3la/Sublist3r*

```
python sublist3r.py -d example.com -p 80,443
```



#### CVE detection using Nmap

```bash
nmap -Pn --script vuln <IP>
```

`-Pn` treats all hosts as online -- skip host discovery while `--script` executes a set of Nmap built-in scripts

#### Metasploit on docker

*Source: https://github.com/opsxcq/docker-metasploit*

```shell
docker run --rm -it --network host \
       -p 4444:4444 -p 80:80 -p 8080:8080 \
       -p 443:443 -p 441:441 -p 8081:8081 \
       strm/metasploit
```

