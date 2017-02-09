step1-add-http-ghost:
trac.conf:
     location / {
        proxy_pass http://localhost:2368;
nginx.conf: emptyish

ports open: 80, 443
http://blog.redf4rth.net blog
https://blog.redf4rth.net can't be reached
http://blog.redf4rth.net/my_project 404
https://blog.redf4rth.net/my_project can't be reached

step2-add-https-ghost:
nginx.conf:
    location / {
        proxy_pass http://localhost:2368;

ports open: 80, 443
http://blog.redf4rth.net blog
https://blog.redf4rth.net blog
http://blog.redf4rth.net/my_project 404
https:///my_project 404

step3-add-http-trac:
ports open: 80, 443
trac.conf:
    location /my_project {
        proxy_pass http://localhost:8088;
nginx.conf:    <== THIS FILE DOESN'T SEEM TO BE RELEVANT.
    location / {
        proxy_pass http://localhost:2368;

http://blog.redf4rth.net blog
https://blog.red.net blog
http://blog.red.net/my_project wiki
https://blog/my_project 404

step4-add-https-trac:
ports open: 80, 443
nginx.conf:
    location /my_project {
        proxy_pass http://localhost:8088;

http://blog.redf4rth.net blog
https://blog.red.net blog
http://blog.red.net/my_project redirects to https/my_project wiki
https://blog/my_project wiki
login redirects to http not https

step5-add-https-trac-with-login-redirect:
ports open: 80, 443
trac.conf
    location /my_project {
        //some lines here omitted for brevity
        return 301 https://$server_name$request_uri;

http://blog.redf4rth.net blog
https://blog.red.net blog
http://blog.red.net/my_project redirects to https/my_project wiki
https://blog/my_project wiki
login redirects to https

PROBABLY SHOULD CLOSE PORT 80 NOW
