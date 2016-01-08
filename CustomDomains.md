# Pressly - Hub domain settings

Pressly hubs are served via the platform URL:

`https://pressly.com/<account>/<hub>`

Optionaly, hub creators can host their hub on a custom domain in 3 different setups:

## Option 1: Serving a Hub on a root domain (ie. `<www.yourhub.com>`)

Pressly supports hosting a hub like any traditional website on the base of a domain such as: `http://yourhub.com` and `http://www.yourhub.com`.

### Setup

1. Ensure `yourhub.com` domain is registered
2. Update the `DNS` (Domain Name Server) settings of `yourhub.com` to:
	- `yourhub.com A record` to `23.235.33.163`
	- `www.yourhub.com CNAME record` to ‘hub.pressly.com’
3. Login to your Pressly account, open your hub from the navigation menu. Once you’re on the hub, select the “gear” icon and click “Settings”.
4. Put `www.yourhub.com` in the “Custom Domain” field and click “Save Changes”.

At this point your domain is setup with the DNS servers and hooked up to Pressly’s platform.

Note: as your DNS updates propagate, you may have to wait a few minutes until your Hub is accessible through the new host.

## Option 2: Serving a Hub on a sub-domain (ie. `<hub>.yourdomain.com`)

Pressly makes it easy to setup a hub on a subdomain, such as: `http://hub.yourdomain.com`

### Setup

1. Update the `DNS` (Domain Name Server) settings of `yourdomain.com` to:
	- `hub.yourdomain.com CNAME record` to ‘hub.pressly.com’
2. Login to your Pressly account, open your hub from the navigation menu. Once you’re on the hub, select the “gear” icon and click “Settings”.
3. Put `hub.yourdomain.com` in the “Custom Domain” field and click “Save Changes”.

At this point your domain is setup with the DNS servers and hooked up to Pressly’s platform.

Note: as your DNS updates propagate, you may have to wait a few minutes until your Hub is accessible through the new host.

## Option 3: Serving a Hub on an existing Website (ie. `www.yoursite.com/<hub>`)

NOTE: These instructions are a bit more advanced require the help of your Website administrator of `yoursite.com`.

Pressly allows your to host a Hub as a path on an existing Website such as: `http://www.yoursite.com/hub`

### Setup

1. Login to your Pressly account, open your hub from the navigation menu. Once you’re on the hub, select the “gear” icon and click “Settings”.
2. Put `www.yoursite.com` in the “Custom Domain” field, and `/hub` in the “Host Path” field,  and click “Save Changes”.
3. Configure a new *backend* on the Webserver of `www.yoursite.com`. The configuration must *reverse proxy* all requests to `/hub*` of your Webserver to `”https://hub.pressly.com”`. Tip: make sure to forward the HTTP `HOST` request header to the Pressly backend.

#### Example Nginx backend setup

```
location /hub {
    rewrite ^([^.]*[^/])$ $1/ permanent;
}
location ^~ /hubs/north-york/ {
    proxy_set_header Host www.yoursite.com;
    proxy_pass https://hub.pressly.com;
}
```
