# prerendercloud-apache

<img align="right" src="https://cloud.githubusercontent.com/assets/22159102/21554484/9d542f5a-cdc4-11e6-8c4c-7730a9e9e2d1.png">

Apache middleware for pre-rendering JavaScript single page apps with [Headless-Render-API.com](https://headless-render-api.com) (formerly named prerender.cloud from 2016 - 2022)

## Usage
* The [www/.htaccess](www/.htaccess) file is intended as a drop in config for a single standard, single Apache static host serving a single page application (redirects 404s to index.html)
  * You can also copy and paste parts or all of the config into your own Apache configuration

### Docker usage

If you're using the standard apache docker image from https://hub.docker.com/_/httpd/

1. uncomment `LoadModule proxy_module modules/mod_proxy.so`
2. uncomment `LoadModule proxy_http_module modules/mod_proxy_http.so`
3. uncomment `LoadModule rewrite_module modules/mod_rewrite.so`
4. uncomment `AllowOverride None` from your `<Directory "/usr/local/apache2/htdocs">` section
5. add       `AllowOverride All` from your `<Directory "/usr/local/apache2/htdocs">` section

...and assuming your index.html, css, and js are in `./www`

```
docker pull httpd
docker run -p8080:80 -v $(pwd)/www:/usr/local/apache2/htdocs:ro -v $(pwd)/httpd.conf:/usr/local/apache2/conf/httpd.conf:ro httpd
```
