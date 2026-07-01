# IP Locator Website
Website for my IP Locator API (https://github.com/Nils1024/IPLocatorAPI)

## Demo
Try it on: https://ip.nilsb.tech/

## How to deploy it using Nginx?
1. Build the website
```bash
npm run install
npm run build
```
2. Upload the files from /dist/ to your server into a folder like /var/www/iplocatorwebsite/
3. Open the nginx config
4. Add something like this:
```
server {
    server_name yourdomain.com

    root /var/www/iplocatorwebsite;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```
5. Add your server to certbot:
```bash
certbot --nginx -d yourdomain.com
```
6. Reload nginx:
```bash
systemctl reload nginx
```

## AI Declaration
I used the JetBrains autocomplete for the website.