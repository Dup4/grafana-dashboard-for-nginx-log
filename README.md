# grafana loki dashboard for nginx

## Usage

### Enable [Geoip2](https://github.com/leev/ngx_http_geoip2_module)

If you want to count the requested geographic location information, you may need to enable the `geoip` or `geoip2` module.

How to enable the `geoip` or `geoip2` module will not be repeated here.

![](./images/geographic_location_infographics.png)

Before using `geoip2`, you may need to download the corresponding geographic location information database.

Maybe you can use [MaxMind](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data).

You can refer to the [official documentation](https://github.com/leev/ngx_http_geoip2_module#example-usage) for related configuration.

### Configure Nginx log format

Required NGINX json log format configuration below.

```config
log_format          json_analytics_log_format escape=json '{'
                    # request unixtime in seconds with a milliseconds resolution
                    '"msec": "$msec", '
                    # connection serial number
                    '"connection": "$connection", '
                    # number of requests made in connection
                    '"connection_requests": "$connection_requests", '
                    # process pid
                    '"pid": "$pid", '
                    # the unique request id
                    '"request_id": "$request_id", '
                    # request length (including headers and body)
                    '"request_length": "$request_length", '
                    # client IP
                    '"remote_addr": "$remote_addr", '
                    # client HTTP username
                    '"remote_user": "$remote_user", '
                    # client port
                    '"remote_port": "$remote_port", '
                    '"time_local": "$time_local", '
                    # local time in the ISO 8601 standard format
                    '"time_iso8601": "$time_iso8601", '
                    # full path no arguments if the request
                    '"request": "$request", '
                    # full path and arguments if the request
                    '"request_uri": "$request_uri", '
                    # full path without arguments
                    '"uri": "$uri", '
                    # args
                    '"args": "$args", '
                    # response status code
                    '"status": "$status", '
                    # the number of body bytes exclude headers sent to a client
                    '"body_bytes_sent": "$body_bytes_sent", '
                    # the number of bytes sent to a client
                    '"bytes_sent": "$bytes_sent", '
                    # HTTP referer
                    '"http_referer": "$http_referer", '
                    # user agent
                    '"http_user_agent": "$http_user_agent", '
                    # http_x_forwarded_for
                    '"http_x_forwarded_for": "$http_x_forwarded_for", '
                    # the request Host: header
                    '"http_host": "$http_host", '
                    '"host": "$host", '
                    # the name of the vhost serving the request
                    '"server_name": "$server_name", '
                    # request processing time in seconds with msec resolution
                    '"request_time": "$request_time", '
                    # upstream backend server for proxied requests
                    '"upstream": "$upstream_addr", '
                    # upstream handshake time incl. TLS
                    '"upstream_connect_time": "$upstream_connect_time", '
                    # time spent receiving upstream headers
                    '"upstream_header_time": "$upstream_header_time", '
                    # time spend receiving upstream body
                    '"upstream_response_time": "$upstream_response_time", '
                    # upstream response length
                    '"upstream_response_length": "$upstream_response_length", '
                    # cache HIT/MISS where applicable
                    '"upstream_cache_status": "$upstream_cache_status", '
                    # TLS protocol
                    '"ssl_protocol": "$ssl_protocol", '
                    # TLS cipher
                    '"ssl_cipher": "$ssl_cipher", '
                    # http or https
                    '"scheme": "$scheme", '
                    # request method
                    '"request_method": "$request_method", '
                    # request protocol, like HTTP/1.1 or HTTP/2.0
                    '"server_protocol": "$server_protocol", '
                    # "p" if request was pipelined, "." otherwise
                    '"pipe": "$pipe", '
                    '"gzip_ratio": "$gzip_ratio", '

                    # Need to install geoip2 module
                    '"geoip2_country_code": "$geoip2_data_country_code", '
                    '"geoip2_country_name": "$geoip2_data_country_name", '
                    '"geoip2_city_name":    "$geoip2_data_city_name", '

                    '"http_cf_ray": "$http_cf_ray" '
                    '}';
```

If you want to add more parameters, you can refer to the [official documentation](http://nginx.org/en/docs/varindex.html).

## Reference

- [Grafana Loki Dashboard for NGINX Service Mesh](https://grafana.com/grafana/dashboards/12559)