---
canonicalUrl: 'https://forge.laravel.com/docs/1.0/sites/ssl.html'
---
# SSL

[[toc]]

## Overview

Forge supports installing custom SSL certificates and using Let's Encrypt to generate free certificates for your websites.

## Let's Encrypt

[Let's Encrypt](https://letsencrypt.org) provides free SSL certificates that are recognized across all major browsers.

If you need to install Let's Encrypt for multiple domains, you may separate multiple domains using commas.

:::warning Cloning a Let's Encrypt Certificate

Because of the Let's Encrypt renewal process, it is not possible to clone Let's Encrypt certificates to other sites. You should simply issue a new Let's Encrypt certificate for that site.
:::

### Renewing Let's Encrypt Certificates

Forge will **automatically** renew your Let's Encrypt certificates within 21 days or less before expiration. Renewal will take place at a random day and time to avoid overwhelming the Let's Encrypt servers.

If something goes wrong while renewing a certificate, Forge will notify the server owner via email.

:::warning Active Subscription Required

You must have an active Laravel Forge subscription in order for your Let's Encrypt certificates to automatically renew.
:::

### Wildcard Subdomain Let's Encrypt Certificates

To install a Let's Encrypt certificate with support for wildcard subdomains, you will need to list both the wildcard subdomain and the root domain in your domain list: `*.domain.com, domain.com`. Let's Encrypt only supports the `dns-01` challenge type when issuing wildcard certificates, so you will need to provide API credentials for your DNS provider.

Forge currently supports the following Let's Encrypt wildcard DNS providers:

- Cloudflare
- DNSimple
- DigitalOcean
- Linode
- OVH
- Route53

#### Cloudflare API Token

If you are using [Cloudflare](https://cloudflare.com) to manage your DNS, your Cloudflare API token must have the `Zone.Zone.Read` and `Zone.DNS.Edit` permissions. In addition, the token must have permissions on **all** zones attached to your Cloudflare account.

#### Cloudflare Universal SSL Certificates

Cloudflare provides [free SSL certificates](https://developers.cloudflare.com/ssl/edge-certificates/universal-ssl/enable-universal-ssl/) to all connected domains and all their first-level subdomains. These certificates are automatically enabled on all domains and subdomains that have Cloudflare's proxy functionality enabled. However, if you have multiple nested subdomains (e.g. `staging.api.example.com`), this universal certificate will not cover those domains and may cause an `ERR_SSL_VERSION_OR_CIPHER_MISMATCH` error. If your application requires multiple nested subdomains, we recommend you disable Cloudflare proxying and use a traditional SSL certificate for your Forge site.

#### Route53 User Policy

If you are using [Route53](https://docs.aws.amazon.com/Route53/latest/APIReference/Welcome.html) to manage your DNS, your IAM user must have the `route53:ChangeResourceRecordSets` permission on your domain's hosted zone. In addition, the user must have the `route53:GetChange` and `route53:ListHostedZones` permissions. 

## Circle Permissions

You may grant a circle member authority to create and manage SSL certificates by granting the `site:manage-ssl` permission.
