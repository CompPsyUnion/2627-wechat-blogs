# Website Not Loading? Understand DNS Resolution Over a Cup of Coffee

You’ve built a personal website and bought an easy-to-remember web address. Yet after sending the link to a friend, they tell you: "It won't load." Before rushing to fix your web pages, remember this: just because your website is built doesn't mean others know where to find it. **DNS resolution** (Domain Name System resolution) is what helps everyone locate it.

## Websites Need an "Address" Too

Imagine inviting a friend to a newly opened coffee shop. If you only give them the shop's name, they still need to look up the street address to get there. Visiting a website works much the same way: `example.com` is a human-friendly name, while the server's IP address is the information a device uses to locate the destination. The system that helps devices look up this information is called DNS.

![A domain name is like a shop name; an IP address is like a street address](img/domain-and-address.png)

This analogy has a limit: DNS is only responsible for answering "What records exist for this domain name?"—it does not build or host the website itself. Knowing a coffee shop's address doesn't guarantee it's open for business; similarly, resolving a website's IP address doesn't guarantee the webpage will load.

## What Happens After You Type a URL?

When you enter a web address into your browser, your device asks DNS: "What is the IP address mapped to this domain name?" DNS returns the answer to your device, which then attempts to connect to the web server. If your device or its DNS resolver has cached (saved) the answer previously, the lookup may be faster.

![After entering a URL, the device queries the address first, then connects to the website](img/dns-resolution.png)

You don't need to memorize all the servers working behind the scenes. As a website owner, just keep two things in mind: **your domain name must have the correct DNS records, and your web server itself must be running properly.** Next, let's walk through an example to configure these records.

## Before You Start, Prepare Two Things

First, you need the domain name you purchased; second, you need the "connection details" provided by your web hosting platform. If you manage your own server, the platform will typically give you a server IP address; if you use a managed website builder or hosting service, the platform may ask you to point your domain to another hostname it provides. Always check your hosting platform's custom domain documentation first to confirm what values are required, and then go to your DNS management console to configure them. **Do not copy addresses from someone else's tutorial into your own DNS records.**

You also need to decide which URL format your visitors will type: the main domain `example.com`, or the `www` address `www.example.com`? Although they look similar, DNS treats them as two distinct hostnames. If you want both to work, you must configure DNS records for each one separately and verify that both are bound in your hosting platform. You can choose one as your preferred address; whether the other redirects to it is a separate setting configured within your web hosting platform.

## Add Two DNS Records for Your Domain

Suppose your domain name is `example.com` and your web server's IP address is `192.0.2.10`. **These are reserved for documentation and educational purposes only—do not use them for your actual website.** When configuring your own site, replace them with your actual domain name and the real address provided by your hosting provider.

Open the management console of your DNS provider and navigate to "DNS Management" or "DNS Records". If you bought your domain from one company but another company manages its DNS, add the records at the company managing DNS. If you're unsure, check the "DNS Management" instructions at your domain registrar to verify where your records should be configured.

First, configure your main domain. This is called an **A record**, which maps a domain name to an IP address like `192.0.2.10`—technically known as an IPv4 address. Most DNS consoles use `@` to represent the main domain `example.com`:

- **Type**: A
- **Name / Host**: `@`
- **Value / Points to**: Your own server's IPv4 address

Next, consider whether visitors might type `www.example.com`. Because `www.example.com` and `example.com` are two separate names, if you want the `www` address to work as well, you can add a **CNAME record**. A CNAME record essentially says, "Please look up the records of this other hostname instead":

- **Type**: CNAME
- **Name / Host**: `www`
- **Target / Value**: `example.com`

![Use an A record for the main domain, and a CNAME record for www pointing to the main domain](img/record-example.png)

Now let's trace the resolution path for your friend: he types `www.example.com`, and DNS sees the CNAME record for `www`, knowing it needs to look up `example.com` next; the main domain's A record then returns the server's IP address. His device uses that IP address to connect to the web server, and the page can load if the website responds properly. If he types `example.com` directly, the lookup starts right at the main domain's A record. The arrows in the diagram illustrate these two resolution paths.

Some DNS consoles require you to enter the full domain name rather than shorthand like `@` or `www`; follow the prompts on your provider's interface. Also, if `www` already has an A record, do not add a CNAME record for `www` alongside it—the two record types will conflict.

## Still Not Loading After Saving? Here's How to Troubleshoot

**1. Check if both hostnames are configured.** Configuring only `example.com` does not automatically make `www.example.com` work, and vice versa. Return to your DNS console and verify the records for both the main domain and `www`.

**2. Give cached DNS records time to expire.** DNS lookup results are temporarily cached, much like a friend keeping an old coffee shop address saved on their phone. Even after you update your records, the DNS resolvers others use might still be serving the old cached answer. In your DNS console, there is a "cache duration" setting called **TTL (Time to Live)**—for initial setup, you can leave it at its default value; note that TTL is not a synchronized alarm clock that refreshes everyone's cache at the exact same moment. Once you've confirmed your records are accurate, waiting a little while before retrying is far more effective than repeatedly clicking "Save".

**3. Check the website and server itself.** If your domain already resolves to the correct IP address but the page still won't load, the problem may be with your web server or web application. If the browser displays a "Connection is not secure" warning, you also need to check your website's HTTPS (SSL/TLS) certificate. DNS only gives directions; once you arrive at the street address, someone still has to open the door.

To narrow down the issue, try visiting both the `www` and non-`www` URLs separately to see if only one of them fails; you can also test accessing the site via mobile data versus Wi-Fi to see if the results differ. While these tests alone won't pinpoint the exact root cause, they will help you decide whether to double-check a specific DNS record, wait for old cached answers to expire, or inspect your web hosting platform. Writing down the exact symptoms and error messages makes troubleshooting much easier than simply saying "it won't load".

Next time you encounter a "website not loading" issue, troubleshoot in this order: **Is the domain name spelled right? Are the DNS records configured properly? Has the DNS cache updated? Is the web server itself up and running?** Checking step by step spares you from blaming everything on a "broken domain."

## References

1. ICANN, *Authoritative Name Server*: https://www.icann.org/en/icann-acronyms-and-terms/authoritative-name-server-en
2. Cloudflare, *DNS record types*: https://developers.cloudflare.com/dns/manage-dns-records/reference/dns-record-types/
3. Cloudflare, *Manage DNS records*: https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/
4. Cloudflare, *Time to Live (TTL)*: https://developers.cloudflare.com/dns/manage-dns-records/reference/ttl/
5. IANA, *Example Domains*: https://www.iana.org/help/example-domains
6. IETF, *RFC 5737: IPv4 Address Blocks Reserved for Documentation*: https://www.rfc-editor.org/info/rfc5737/
