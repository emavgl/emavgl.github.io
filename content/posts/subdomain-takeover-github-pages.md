+++
authors = ["Emanuele Viglianisi"]
title = "How My Domain Got Hijacked Without Anyone Touching It"
date = "2026-08-24"
description = "A GitHub Pages subdomain takeover story: how an attacker served spam on ftp.viglianisi.eu without ever accessing my DNS."
tags = ["security", "dns", "github-pages", "subdomain-takeover", "seo-spam"]
categories = ["security"]
+++

Some time ago, I received a security alert from Google: a new owner had verified one of the subdomains of my domain in their own Google Search Console. I do not remember having given anybody permission to do that, so I started investigating.

After a few minutes of digging, the picture was clear: someone was serving an Indonesian online gambling site on `ftp.viglianisi.eu`, a subdomain of *my* domain.

```
$ curl -s http://ftp.viglianisi.eu/
<title>POWERPLAY128 Bandar SV388 Agen Judi Sabung Ayam</title>
...
Server: GitHub.com
```

Served by GitHub.com, on my domain. My first reaction was to check everything: passwords, active sessions, account activity. Nothing. Nobody had hacked me. Not my GitHub account, not my OVH account, not my Google account. So how was that possible?

I have to admit it: I immediately jumped to an AI assistant and started asking questions - what could allow a third party to serve content on my subdomain without accessing any of my accounts? The AI was surprisingly helpful: within a few exchanges we walked through the DNS records together, ruled out the classic attack vectors one by one (compromised accounts, DNS hijacking at the registrar), and it pointed me towards something I had never heard of before: subdomain takeover. It even explained how GitHub Pages decides which repository serves which hostname, which turned out to be the missing piece of the puzzle.

With that lead, understanding the rest of the story took only minutes.

My website is hosted on GitHub Pages with a custom domain:

```
viglianisi.eu  ->  A  ->  185.199.108.153   (GitHub Pages)
```

Years ago, when I configured the domain at OVH, the panel had automatically created a bunch of default DNS records for common subdomains. Among them there was this one:

```
ftp.viglianisi.eu  ->  CNAME  ->  viglianisi.eu
```

I never used FTP. I never thought about it. That record just sat there for years, silently pointing an unused subdomain at GitHub's servers. This kind of record is called a *dangling DNS record*: a name that points to a service you don't actually control, or never did.

Here comes the part the AI helped me discover: GitHub Pages routes incoming requests by looking at the `Host` header. When a browser asks for `ftp.viglianisi.eu`, GitHub looks for a repository that has claimed that hostname as its custom domain. None of my repositories did - so whoever claimed it first, wins.

The attacker's procedure was as simple as creating a repository with spam content, adding a `CNAME` file containing `ftp.viglianisi.eu` and setting it as custom domain in the Pages settings. Since my forgotten DNS record already pointed the subdomain at GitHub's servers, the verification succeeded, and from that moment the attacker's content was served under my name. No phishing, no leaked credentials, no brute force. Just an abandoned DNS record and a hosting platform that trusts DNS as proof of ownership.

Interestingly, HTTPS partially saved me: visiting the subdomain over HTTPS produced a certificate error, because GitHub had not issued a valid certificate for that hostname under my control. But plain HTTP worked fine - and for SEO spam purposes, HTTP is all an attacker needs. Googlebot indexes over HTTP without complaining.

You might wonder why an attacker would bother claiming somebody else's sleepy subdomain instead of using their own domain. Search engines trust established domains more than freshly registered ones, so spam hosted under a clean, years-old `.eu` domain gets indexed faster and ranks better. Spam filters and email scanners are suspicious of new domains, while a legitimate-looking subdomain passes through undetected. And above all, this technique is free and scalable: attackers scan the internet for dangling CNAMEs pointing to popular services (GitHub Pages, Heroku, AWS S3, Azure...) and claim them in bulk.

In my case they even tried to register the subdomain in Google Search Console and submitted AMP pages pointing to their real landing page (`mobilesv388.pages.dev`). Google flagged the mismatch ("AMP page domain mismatch") - which is exactly what triggered the alert email that exposed the whole thing. A nice reminder that automated security systems sometimes work for you even when you don't know they are watching.

Once I understood the problem - and I have to thank the AI for accelerating that part enormously - the fix took minutes. First, I removed the dangling `ftp` CNAME from the OVH zone: without DNS pointing at GitHub, the attacker's claim became worthless and the site stopped resolving altogether. Then, to prevent it from ever happening again, I verified my domain on GitHub (*Settings → Pages → Domains*), which requires publishing a TXT challenge record in the DNS zone:

```
_github-pages-challenge-emavgl.viglianisi.eu  TXT  "<challenge-token>"
```

Once the domain shows as verified, GitHub refuses any custom-domain claim on `viglianisi.eu` or any of its subdomains coming from accounts that don't own it. The attack path is permanently closed. Lastly, I reported the abusive repository via [GitHub Abuse Reports](https://github.com/contact/report-abuse), including the response headers proving the content was served by `Server: GitHub.com`. The attacker's Google Search Console verification died on its own, since their HTML verification file lived on the hijacked page, which no longer resolves.

The irony is not lost on me: I wrote no insecure code, reused no weak passwords, clicked no suspicious link. The vulnerability was a single default checkbox ticked by a hosting panel years before the attack. If you host anything yourself, take five minutes today to audit your DNS zone: every record pointing to a service you don't actively use is a liability, especially registrar defaults like `ftp`, `mail` or `webmail`. In the eyes of platforms that verify ownership via DNS, a stale record *is* proof of ownership - treat it like an API key you forgot to revoke.

If this story helps you catch a dangling record before somebody else does, then writing it down was worth it!
