docker run -it --rm -v /mycode/:/home/conf  httpd cp conf/httpd.conf /home/conf/httpd.conf

LoadModule proxy_module modules/mod_proxy.so                # support proxy
LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so      # Call PHP via Proxy
LoadModule deflate_module modules/mod_deflate.so            # let apache compress the returned data
LoadModule rewrite_module modules/mod_rewrite.so            # to use .htaccess, rewrite url
LoadModule ssl_module modules/mod_ssl.so                    # support SSL (https, port 443)

Include conf/extra/httpd-vhosts.conf                        # to load Virtual Hosts from httpd-vhosts.conf

#Thêm vào
AddHandler "proxy:fcgi://php-product:9000" .php             # to run PHP Script via Proxy

docker build -t httpd:version2 --force-rm -f Dockerfile .    # create image from Dockerfile
docker save --output httpd.tar httpd:version2                # save image to file (to merge layers)
docker image rm httpd:version2                               # delete image
docker load -i httpd.tar                                     # reload image from file

So far, there is an image containing APACHE HTTPD with the above config, which can be quickly tested with the command:

docker run -it --rm -p 3456:80 httpd:version2 # containers self-delete when finished