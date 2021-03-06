# letsencrypt-dns
Autonomous docker container responsible for issuing and renewing Letsencrypt certificates using DNS-challenge. This is a logical extension of Kyle Ondy's [dns-certbot](https://hub.docker.com/r/kyleondy/dns-certbot/), with added support for delegated domains (default Dehydrated hook does not support such configuration, see [discussion on GitHub](https://github.com/AnalogJ/lexicon/issues/80)).

# Usage

## Environment variables

* `PROVIDER=route53` - optional (defaults to `cloudflare`).
* `LEXICON_ROUTE53_ACCESS_KEY=<AWS IAM user Access Key ID>` - required
if PROVIDER is set to `route53`
* `LEXICON_ROUTE53_ACCESS_SECRET=<AWS IAM user Secret Key>` - required
if PROVIDER is set to `route53`
* `SLEEP_TIME` - optional (defaults to `1d`) sleep time between renewals.  The special value `0` means 'run once, then exit'.
* `CERTBOT_DOMAIN` - the domain to get the certificate for.
* `CERTBOT_STAGING` - if set to anything but `False`, requests a fake certificate,
not subject to rate limits.
* `CERTBOT_DELEGATED` - if specified, indicates the part of the domain delegated to another DNS authority. `False` is equivalent to not set.
* `CERTBOT_ALIAS` - if specified, sets the name of the directory under `/certs` to be used.

`CERTBOT_ALIAS` is required to request wildcard certificates.

## Volumes

* `<your Letsencrypt certificates directory>:/certs`
