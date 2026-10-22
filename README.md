# HTB Starting Point — Three (S3 Bucket Misconfiguration)

Writeup for the HackTheBox Starting Point machine **Three**, part of my cybersecurity homelab practice as I transition from a finance career into security.

## Summary

- **Target**: `thetoppers.htb` (10.129.227.248)
- **Difficulty**: Starting Point / Very Easy
- **Attack path**: Contact-page email reveals domain → DNS enumeration reveals an `s3` subdomain → site content is hosted on a misconfigured, publicly writable AWS S3 bucket → upload a PHP web shell to the bucket → remote code execution via the live website → flag read directly from the web server.
- **Core lesson**: a cloud storage misconfiguration (public S3 bucket with open `PutObject` permission) was the entire vulnerability — no OS-level exploit, no privilege escalation needed.

## Environment

- Attacking from HTB Pwnbox (Parrot-based), connected over the Starting Point VPN
- Tools used: `nmap`, `gobuster`, `ffuf`, `curl`, `awscli`

## Files

- [`recon.md`](./recon.md) — port scanning, site enumeration, domain/subdomain discovery
- [`exploitation.md`](./exploitation.md) — S3 bucket enumeration, PHP web shell upload, flag capture
- [`linkedin-post.md`](./linkedin-post.md) — lessons-learned post draft
- `screenshots/` — numbered screenshots referenced from `recon.md` and `exploitation.md`

## Flag

Captured at `/var/www/` on the target via the uploaded web shell.
