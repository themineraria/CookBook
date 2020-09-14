# Finding subdomains

Finding subdomains is fundamental. The more subdomains you find, the bigger attack surface you have. Which means bigger possibility of success.

For now this seems to be a very comprehensive list of tools to find subdomains. [https://blog.bugcrowd.com/discovering-subdomains](https://blog.bugcrowd.com/discovering-subdomains)

Some tools find some stuff, other tools other stuff. So your best bet is to use a few of them together. Don't forget to brute-force recursively!

### recon-ng <a id="recon-ng"></a>

In order to find subdomains we can use the recon-ng framework. It has the same basic structure as metasploit. You can learn more about this tool in the tools-section.

```text
recon-ng

use use recon/domains-hosts/



show options

set source cnn.com
```

All these subdomains will be saved in `hosts`, which you can access though: `show hosts`

If some of these subdomains are not given IPs automatically you can just run

```text
use recon/hosts-hosts/resolve
run
```

And it will resolve all the hosts in the hosts-file.

### Google Dorks <a id="google-dorks"></a>

Using google we can also find subdomains.

This will only give us the subdomains of a site.

`site:msn.com -site:www.msn.com`

`site:*.nextcloud.com`

To exclude a specific subdomain you can do this:

`site:*.nextcloud.com -site:help.nextcloud.com`

### subbrute.py <a id="subbrutepy"></a>

The basic command is like this

`./subbrute.py -p cnn.com`

[https://github.com/TheRook/subbrute](https://github.com/TheRook/subbrute)

### Knock <a id="knock"></a>

I haven't tested this yet. [https://github.com/guelfoweb/knock](https://github.com/guelfoweb/knock)

### Being smart <a id="being-smart"></a>

You also have to look at what kind of system the target has. Some web-apps give their clients their own subdomains. Like github.

Check out the homepage Often companies brag about their clients. You can use this to guess the subdomains of some clients.

### Reverse DNS-lookup <a id="reverse-dns-lookup"></a>

If you manage to figure out the IP range that the target owns \(see section about nmap below\). You can see which machines are online. And then you can run a script to find out the domain-addresses of those machines. That way you might find something new.

The text-file onlyIps.txt is a textfile with one IP-address on each line.

```text
#!/bin/bash

while read p; do
  echo $p;
  host  $p
done 
```

`Here are some more tools that can do reverse lookup` [`http://www.cyberciti.biz/faq/how-to-test-or-check-reverse-dns/`](http://www.cyberciti.biz/faq/how-to-test-or-check-reverse-dns/)

### `Online tools` <a id="online-tools"></a>

#### `DNSDumpster` <a id="dnsdumpster"></a>

[`https://dnsdumpster.com/`](https://dnsdumpster.com/)

#### `Pentest-tools` <a id="pentest-tools"></a>

[`https://pentest-tools.com/information-gathering/find-subdomains-of-domain`](https://pentest-tools.com/information-gathering/find-subdomains-of-domain)

#### `Intodns` <a id="intodns"></a>

[`http://www.intodns.com/`](http://www.intodns.com/)

#### `DNSStuff` <a id="dnsstuff"></a>

`This tool doesn't enumerate subdomains per se. But it hands of a lot of information about domains.` [`http://www.dnsstuff.com/`](http://www.dnsstuff.com/)

## `Bypassing CloudFlare` <a id="bypassing-cloudflare"></a>

[`https://www.ericzhang.me/resolve-cloudflare-ip-leakage/`](https://www.ericzhang.me/resolve-cloudflare-ip-leakage/)

`This tool can be used to find old IPs. It could mean that the` [`http://toolbar.netcraft.com/site_report?url=lyst.com`](http://toolbar.netcraft.com/site_report?url=lyst.com)

### `Brute force dictionaries` <a id="brute-force-dictionaries"></a>

`If you try to brute force the domains it is a good idea to have a good dictionary. That can be found here:`

`Bitquark` [`https://github.com/bitquark/dnspop`](https://github.com/bitquark/dnspop)

`SecList` [`https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS`](https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS)

## `References` <a id="references"></a>

[`https://en.wikipedia.org/wiki/CNAME_record`](https://en.wikipedia.org/wiki/CNAME_record)

