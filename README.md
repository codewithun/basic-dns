# Basic DNS — Custom Domain Configuration

## Overview

This project documents how to configure a custom domain using Rumahweb DNS Management, connect a website to GitHub Pages, and point a subdomain to an Nginx web server running on a Helipod VPS.

## Project Details

- **Domain:** `formapi.online`
- **DNS Provider:** Rumahweb
- **Static Website Hosting:** GitHub Pages
- **VPS Provider:** Helipod
- **VPS Operating System:** Ubuntu 24.04
- **Web Server:** Nginx

## Domain Architecture

| Domain | Purpose | Target |
|---|---|---|
| `github.formapi.online` | GitHub Pages website | `codewithun.github.io` |
| `server.formapi.online` | VPS-hosted website | `169.58.223.6` |

## 1. Configure DNS Records

DNS records were configured through Rumahweb DNS Management.

### GitHub Pages

| Field | Value |
|---|---|
| Type | CNAME |
| Hostname | `github` |
| Target | `codewithun.github.io` |

### Helipod VPS

| Field | Value |
|---|---|
| Type | A |
| Hostname | `server` |
| Target | `169.58.223.6` |

A TXT record was also created to verify domain ownership through GitHub.

## 2. Configure GitHub Pages

1. Create a GitHub repository and enable GitHub Pages.
2. Open the repository's **Settings → Pages**.
3. Enter `github.formapi.online` in the Custom domain field.
4. Save the configuration.
5. Configure the corresponding CNAME record in Rumahweb.
6. Wait for DNS propagation and HTTPS provisioning.

Website: https://github.formapi.online

## 3. Configure the VPS

The static website was deployed to an Ubuntu 24.04 VPS running Nginx.

The Nginx document root is:

`/var/www/static-site`

The website files include:

- `index.html`
- `style.css`
- `images/`

The Nginx server block serves the website from `/var/www/static-site`.

The domain `server.formapi.online` points to the VPS public IP address. The HTTP service is exposed through external port `32080`, mapped to internal port `80`.

Website: http://server.formapi.online:32080

## 4. Verify DNS Resolution

DNS resolution was checked using the `dig` command.

### GitHub Pages

```bash
dig github.formapi.online CNAME +short
```

Expected result:

```text
codewithun.github.io.
```

### VPS

```bash
dig server.formapi.online A +short
```

Expected result:

```text
169.58.223.6
```

Both DNS records resolved to their expected targets during testing.

## 5. Results

- The custom domain was verified through GitHub.
- The GitHub Pages website was accessible through its custom subdomain.
- The VPS subdomain resolved to the Helipod VPS public IP.
- The Nginx website was accessible through the VPS subdomain and external HTTP port.

## Conclusion

This project demonstrates how DNS records connect custom domains to different hosting platforms. It covers domain ownership verification, CNAME and A records, GitHub Pages custom domains, and VPS-based website hosting.

## References

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Custom Domain Documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Rumahweb](https://www.rumahweb.com/)
- [roadmap.sh — Basic DNS](https://roadmap.sh/projects/basic-dns)
