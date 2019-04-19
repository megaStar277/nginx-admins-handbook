<div align="center">
  <h1>Nginx Quick Reference</h1>
</div>

<div align="center">
  <h6><code>My notes about Nginx...</code></h6>
</div>

<br>

<p align="center">
  <a href="https://github.com/trimstray/nginx-quick-reference/pulls">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?longCache=true" alt="Pull Requests">
  </a>
  <a href="http://www.gnu.org/licenses/">
    <img src="https://img.shields.io/badge/License-GNU-blue.svg?longCache=true" alt="License">
  </a>
</p>

<div align="center">
  <sub>Created by
  <a href="https://twitter.com/trimstray">trimstray</a> and
  <a href="https://github.com/trimstray/nginx-quick-reference/graphs/contributors">contributors</a>
</div>

<br>

****

# Table of Contents

- **[Introduction](#introduction)**
  * [General disclaimer](#general-disclaimer)
  * [Contributing & Support](#contributing--support)
  * [Reports: blkcipher.info](#reports-blkcipherinfo)
    * [SSL Labs](#ssl-labs)
    * [Mozilla Observatory](#mozilla-observatory)
  * [Printable high-res hardening checklist](#printable-high-res-hardening-checklist)
- **[Books](#books)**
  * [Nginx Essentials](#nginx-essentials)
  * [Nginx Cookbook](#nginx-cookbook)
  * [Nginx HTTP Server](#nginx-http-server)
  * [Nginx High Performance](#nginx-high-performance)
  * [Mastering Nginx](#mastering-nginx)
- **[External Resources](#external-resources)**
  * [About Nginx](#about-nginx)
  * [References](#references)
  * [Cheatsheets](#cheatsheets)
  * [Performance & Hardening](#performance--hardening)
  * [Playgrounds](#playgrounds)
  * [Config generators](#config-generators)
  * [Static analyzers](#static-analyzers)
  * [Log analyzers](#log-analyzers)
  * [Performance analyzers](#performance-analyzers)
  * [Benchmarking tools](#benchmarking-tools)
  * [Online tools](#online-tools)
  * [Other stuff](#other-stuff)
- **[Helpers](#helpers)**
  * [Installation from source](#installation-from-source)
  * [Installation from prebuilt packages](#installation-from-prebuilt-packages)
    * [RHEL7 or CentOS 7](#rhel7-or-centos-7)
    * [Debian or Ubuntu](#debian-or-ubuntu)
  * [Nginx directories and files](#nginx-directories-and-files)
  * [Nginx commands](#nginx-commands)
  * [Nginx processes](#nginx-processes)
  * [Nginx contexts](#nginx-contexts)
  * [Error log severity levels](#error-log-severity-levels)
  * [Debugging](#debugging)
    * [See the top 5 IP addresses in a web server log](#see-the-top-5-ip-addresses-in-a-web-server-log)
    * [Analyse web server log and show only 2xx http codes](#analyse-web-server-log-and-show-only-2xx-http-codes)
    * [Analyse web server log and show only 5xx http codes](#analyse-web-server-log-and-show-only-5xx-http-codes)
    * [Get range of dates in a web server log](#get-range-of-dates-in-a-web-server-log)
    * [Get line rates from web server log](#get-line-rates-from-web-server-log)
    * [Trace network traffic for all Nginx processes](#trace-network-traffic-for-all-nginx-processes)
    * [List all files accessed by a Nginx](#list-all-files-accessed-by-a-nginx)
  * [Rate Limiting](#rate-limiting)
    * [Limiting the rate of requests with burst mode](#limiting-the-rate-of-requests-with-burst-mode)
    * [Limiting the rate of requests with burst mode and nodelay](#limiting-the-rate-of-requests-with-burst-mode-and-nodelay)
    * [Limiting the number of connections](#limiting-the-number-of-connections)
  * [Shell aliases](#shell-aliases)
- **[Base Rules](#base-rules)**
  * [Organising Nginx configuration](#beginner-organising-nginx-configuration)
  * [Separate listen directives for 80 and 443](#beginner-separate-listen-directives-for-80-and-443)
  * [Prevent processing requests with undefined server names](#beginner-prevent-processing-requests-with-undefined-server-names)
  * [Use reload method to change configurations on the fly](#beginner-use-reload-method-to-change-configurations-on-the-fly)
  * [Use only one SSL config for specific listen directive](#beginner-use-only-one-ssl-config-for-specific-listen-directive)
  * [Force all connections over TLS](#beginner-force-all-connections-over-tls)
  * [Use geo/map modules instead allow/deny](#beginner-use-geomap-modules-instead-allowdeny)
  * [Map all the things...](#beginner-map-all-the-things)
  * [Drop the same root inside location block](#beginner-drop-the-same-root-inside-location-block)
  * [Use debug mode for debugging](#beginner-use-debug-mode-for-debugging)
  * [Use custom log formats for debugging](#beginner-use-custom-log-formats-for-debugging)
- **[Performance](#performance)**
  * [Adjust worker processes](#beginner-adjust-worker-processes)
  * [Use HTTP/2](#beginner-use-http2)
  * [Maintaining SSL sessions](#beginner-maintaining-ssl-sessions)
  * [Use exact names where possible](#beginner-use-exact-names-where-possible)
  * [Avoid checks server_name with if directive](#beginner-avoid-checks-server_name-with-if-directive)
  * [Use limit_conn to improve limiting the download speed](#beginner-use-limit_conn-to-improve-limiting-the-download-speed)
- **[Hardening](#hardening)**
  * [Run as an unprivileged user](#beginner-run-as-an-unprivileged-user)
  * [Disable unnecessary modules](#beginner-disable-unnecessary-modules)
  * [Protect sensitive resources](#beginner-protect-sensitive-resources)
  * [Hide Nginx version number](#beginner-hide-nginx-version-number)
  * [Hide Nginx server signature](#beginner-hide-nginx-server-signature)
  * [Hide upstream proxy headers](#beginner-hide-upstream-proxy-headers)
  * [Use min. 2048-bit private keys](#beginner-use-min-2048-bit-private-keys)
  * [Keep only TLS 1.2](#beginner-keep-only-tls-12)
  * [Use only strong ciphers](#beginner-use-only-strong-ciphers)
  * [Use more secure ECDH Curve](#beginner-use-more-secure-ecdh-curve)
  * [Use strong Key Exchange](#beginner-use-strong-key-exchange)
  * [Defend against the BEAST attack](#beginner-defend-against-the-beast-attack)
  * [Disable HTTP compression (mitigation of CRIME/BREACH attacks)](#beginner-disable-http-compression-mitigation-of-crimebreach-attacks)
  * [HTTP Strict Transport Security](#beginner-http-strict-transport-security)
  * [Reduce XSS risks (Content-Security-Policy)](#beginner-reduce-xss-risks-content-security-policy)
  * [Control the behavior of the Referer header (Referrer-Policy)](#beginner-control-the-behavior-of-the-referer-header-referrer-policy)
  * [Provide clickjacking protection (X-Frame-Options)](#beginner-provide-clickjacking-protection-x-frame-options)
  * [Prevent some categories of XSS attacks (X-XSS-Protection)](#beginner-prevent-some-categories-of-xss-attacks-x-xss-protection)
  * [Prevent Sniff Mimetype middleware (X-Content-Type-Options)](#beginner-prevent-sniff-mimetype-middleware-x-content-type-options)
  * [Deny the use of browser features (Feature-Policy)](#beginner-deny-the-use-of-browser-features-feature-policy)
  * [Reject unsafe HTTP methods](#beginner-reject-unsafe-http-methods)
  * [Control Buffer Overflow attacks](#beginner-control-buffer-overflow-attacks)
  * [Mitigating Slow HTTP DoS attack (Closing Slow Connections)](#beginner-mitigating-slow-http-dos-attack-closing-slow-connections)
- **[Load Balancing](#load-balancing)**
  * [Tweak passive health checks](#beginner-tweak-passive-health-checks)
  * [Don't disable backends by comments, use down parameter](#beginner-dont-disable-backends-by-comments-use-down-parameter)
- **[Configuration Examples](#configuration-examples)**
  * [Reverse Proxy](#reverse-proxy)
    * [Import configuration](#import-configuration)
    * [Set bind IP address](#set-bind-ip-address)
    * [Set your domain name](#set-your-domain-name)
    * [Regenerate private keys and certs](#regenerate-private-keys-and-certs)
    * [Add new domain](#add-new-domain)
    * [Test your configuration](#test-your-configuration)

# Introduction

<img src="https://github.com/trimstray/nginx-quick-reference/blob/master/static/img/nginx_logo.png" align="right">

  > Before using the **Nginx** please read **[Beginner’s Guide](http://nginx.org/en/docs/beginners_guide.html)**.

<p align="justify"><b>Nginx</b> (<i>/ˌɛndʒɪnˈɛks/ EN-jin-EKS</i>) is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server, originally written by Igor Sysoev. For a long time, it has been running on many heavily loaded Russian sites including Yandex, Mail.Ru, VK, and Rambler.</p>

To increase your knowledge, read **[Nginx Documentation](https://nginx.org/en/docs/)**.

## General disclaimer

This is not an official handbook. Many of these rules refer to external resources. It is rather a quick collection of some rules and papers used by me in production environments (not only).

Throughout this reference you will explore the many features of Nginx and how to use them. This guide is fairly comprehensive, and touches a lot of the functions (e.g. security, performance) of Nginx server.

Before you start remember about the two most important things:

  > **`Do not follow guides just to get 100% of something. Think about what you actually do at your server!`**

  > **`These guidelines provides recommendations for very restrictive setup.`**

## Contributing & Support

If you find something which doesn't make sense, or something doesn't seem right, please make a pull request and please add valid and well-reasoned explanations about your changes or comments.

Before adding a pull request, please see the **[contributing guidelines](CONTRIBUTING.md)**.

If this project is useful and important for you, you can bring **positive energy** by giving some **good words** or **supporting this project**. Thank you!

## Reports: blkcipher.info

Many of these recipes have been applied to the configuration of my private website.

  > An example configuration is in [this](#configuration-examples) chapter.

### SSL Labs

I finally got all 100%'s on my scores:

<p align="center">
  <a href="https://www.ssllabs.com/ssltest/analyze.html?d=blkcipher.info&hideResults=on">
    <img src="https://github.com/trimstray/nginx-quick-reference/blob/master/static/img/blkcipher_ssllabs_preview.png" alt="blkcipher_ssllabs_preview">
  </a>
</p>

### Mozilla Observatory

I also got the highest note from Mozilla:

<p align="center">
  <a href="https://observatory.mozilla.org/analyze/blkcipher.info?third-party=false">
    <img src="https://github.com/trimstray/nginx-quick-reference/blob/master/static/img/blkcipher_mozilla_observatory_preview.png" alt="blkcipher_mozilla_observatory_preview">
  </a>
</p>

## Printable high-res hardening checklist

Hardening checklist based on these recipes (for @ssllabs A+ 100%) - High-Res 5000x8200.

  > For `*.xcf` and `*.pdf` formats please see [this](https://github.com/trimstray/nginx-quick-reference/tree/master/static/img) directory.

<p align="center">
    <img src="https://github.com/trimstray/nginx-quick-reference/blob/master/static/img/nginx-hardening-checklist.png"
        alt="nginx-hardening-checklist" width="75%" height="75%">
</p>

# Books

#### [Nginx Essentials](https://www.amazon.com/Nginx-Essentials-Valery-Kholodkov/dp/1785289535)

Authors: **Valery Kholodkov**

_Excel in Nginx quickly by learning to use its most essential features in real-life applications._

- _Learn how to set up, configure, and operate an Nginx installation for day-to-day use_
- _Explore the vast features of Nginx to manage it like a pro, and use them successfully to run your website_
- _Example-based guide to get the best out of Nginx to reduce resource usage footprint_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx Cookbook](https://www.oreilly.com/library/view/nginx-cookbook/9781492049098/)

Authors: **Derek DeJonghe**

_You’ll find recipes for:_

- _Traffic management and A/B testing_
- _Managing programmability and automation with dynamic templating and the NGINX Plus API_
- _Securing access through encrypted traffic, secure links, HTTP authentication subrequests, and more_
- _Deploying NGINX to AWS, Azure, and Google cloud-computing services_
- _Using Docker to deploy containers and microservices_
- _Debugging and troubleshooting, performance tuning, and practical ops tips_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx HTTP Server](https://www.amazon.com/Nginx-HTTP-Server-Harness-infrastructure/dp/178862355X)

Authors: **Martin Fjordvald**, **Clement Nedelcu**

_Harness the power of Nginx to make the most of your infrastructure and serve pages faster than ever._

- _Discover possible interactions between Nginx and Apache to get the best of both worlds_
- _Learn to exploit the features offered by Nginx for your web applications_
- _Get your hands on the most updated version of Nginx (1.13.2) to support all your web administration requirements_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx High Performance](https://www.amazon.com/Nginx-High-Performance-Rahul-Sharma/dp/1785281836)

Authors: **Rahul Sharma**

_Optimize NGINX for high-performance, scalable web applications._

- _Configure Nginx for best performance, with configuration examples and explanations_
- _Step–by-step tutorials for performance testing using open source software_
- _Tune the TCP stack to make the most of the available infrastructure_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Mastering Nginx](https://www.amazon.com/Mastering-Nginx-Dimitri-Aivaliotis/dp/1849517444)

Authors: **Dimitri Aivaliotis**

_Written for experienced systems administrators and engineers, this book teaches you from scratch how to configure Nginx for any situation. Step-by-step instructions and real-world code snippets clarify even the most complex areas._

<sup><i>This short review comes from this book or the store.</i></sup>

# External Resources

##### About Nginx

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.nginx.com/"><b>Nginx Project</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://nginx.org/en/docs/"><b>Nginx Documentation</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginx/nginx"><b>Nginx official read-only mirror</b></a><br>
</p>

##### References

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/h5bp/server-configs-nginx"><b>Nginx boilerplate configs</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginx-boilerplate/nginx-boilerplate"><b>Awesome Nginx configuration template</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/SimulatedGREG/nginx-cheatsheet"><b>Nginx Quick Reference</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/fcambus/nginx-resources"><b>A collection of resources covering Nginx and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.evanmiller.org/nginx-modules-guide.html"><b>Emiller’s Guide To Nginx Module Development</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml"><b>Transport Layer Security (TLS) Parameters</b></a><br>
</p>

##### Cheatsheets

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://gist.github.com/carlessanagustin/9509d0d31414804da03b"><b>Nginx Cheatsheet</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.scalescale.com/tips/nginx/"><b>Nginx Tutorials, Linux Sysadmin Configuration & Optimizing Tips and Tricks</b></a><br>
</p>

##### Performance & Hardening

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/denji/nginx-tuning"><b>Nginx Tuning For Best Performance by Denji</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/projects/best-practices/"><b>SSL/TLS Deployment Best Practices</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/projects/rating-guide/index.html"><b>SSL Server Rating Guide</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.upguard.com/blog/how-to-build-a-tough-nginx-server-in-15-steps"><b>How to Build a Tough NGINX Server in 15 Steps</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.cyberciti.biz/tips/linux-unix-bsd-nginx-webserver-security.html"><b>Top 25 Nginx Web Server Best Security Practices</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://calomel.org/nginx.html"><b>Nginx Secure Web Server</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html"><b>Strong SSL Security on Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://enable-cors.org/index.html"><b>Enable cross-origin resource sharing (CORS)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://istlsfastyet.com/"><b>TLS has exactly one performance problem: it is not used widely enough</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nbs-system/naxsi"><b>WAF for Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://geekflare.com/install-modsecurity-on-nginx/"><b>ModSecurity for Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet"><b>Transport Layer Protection Cheat Sheet</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://wiki.mozilla.org/Security/Server_Side_TLS"><b>Security/Server Side TLS</b></a><br>
</p>

##### Playgrounds

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/sportebois/nginx-rate-limit-sandbox"><b>NGINX Rate Limit, Burst and nodelay sandbox</b></a><br>
</p>

##### Config generators

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://nginxconfig.io/"><b>Nginx config generator on steroids</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://mozilla.github.io/server-side-tls/ssl-config-generator/"><b>Mozilla SSL Configuration Generator</b></a><br>
</p>

##### Static analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/yandex/gixy"><b>Nginx static analyzer</b></a><br>
</p>

##### Log analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://goaccess.io/"><b>GoAccess</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.graylog.org/"><b>Graylog</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.elastic.co/products/logstash"><b>Logstash</b></a><br>
</p>

##### Performance analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/lebinh/ngxtop"><b>ngxtop</b></a><br>
</p>

##### Benchmarking tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.joedog.org/siege-home/"><b>siege</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/wg/wrk"><b>wrk</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/codesenberg/bombardier"><b>bombardier</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/cmpxchg16/gobench"><b>gobench</b></a><br>
</p>

##### Online tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/ssltest/"><b>SSL Server Test by SSL Labs</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/ssltest/viewMyClient.html"><b>SSL/TLS Capabilities of Your Browser</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.htbridge.com/ssl/"><b>Test SSL/TLS (PCI DSS, HIPAA and NIST)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://sslanalyzer.comodoca.com/"><b>SSL analyzer and certificate checker</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cryptcheck.fr/"><b>Test your TLS server configuration (e.g. ciphers)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.jitbit.com/sslcheck/"><b>Scan your website for non-secure content</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cipherli.st/"><b>Strong ciphers for Apache, Nginx, Lighttpd and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://securityheaders.com/"><b>Analyse the HTTP response headers by Security Headers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://observatory.mozilla.org/"><b>Analyze your website by Mozilla Observatory</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://webhint.io/"><b>Linting tool that will help you with your site's accessibility, speed, security and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://urlscan.io/"><b>Service to scan and analyse websites</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://regexr.com/"><b>Online tool to learn, build, & test Regular Expressions</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.regextester.com/"><b>Online Regex Tester & Debugger</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cryptcheck.fr/suite/"><b>User agent compatibility (Cipher suite)</b></a><br>
</p>

##### Other stuff

<p>
&nbsp;&nbsp;:black_small_square: <a href="http://www.bbc.co.uk/blogs/internet/entries/17d22fb8-cea2-49d5-be14-86e7a1dcde04"><b>BBC Digital Media Distribution: How we improved throughput by 4x</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/jiangwenyuan/nuster/wiki/Web-cache-server-performance-benchmark:-nuster-vs-nginx-vs-varnish-vs-squid"><b>Web cache server performance benchmark: nuster vs nginx vs varnish vs squid</b></a><br>
</p>

# Helpers

#### Installation from source

There are currently two versions of Nginx:

- **stable** - is recommended, doesn’t include all of the latest features, but has critical bug fixes from mainline release
- **mainline** - is typically quite stable as well, includes the latest features and bug fixes and is always up to date

Mandatory requirements:

  > Download, compile and install or install prebuilt packages from your distribution repository.

- [OpenSSL](https://www.openssl.org/source/) library
- [Zlib](https://zlib.net/) library
- [PCRE](https://ftp.pcre.org/pub/pcre/) library
- [GCC](https://gcc.gnu.org/) Compiler

###### Nginx package

- [Nginx](https://nginx.org/download/) source code

  > Before starting the installation, please see [Installation and Compile-Time Options](https://www.nginx.com/resources/wiki/start/topics/tutorials/installoptions/).

```bash
# Download latest package:
wget -c https://nginx.org/download/nginx-1.9.8.tar.gz

# Extract content and go to the Nginx source directory:
tar xzvfp nginx-1.9.8.tar.gz && cd nginx-1.9.8

# Configure with default values for build parameters:
./configure

# Configure with new values for build parameters:
./configure --user=nginx \
            --group=nginx \
            --prefix=/usr/local/nginx \
            --conf-path=/usr/local/nginx/nginx.conf \
            --sbin-path=/usr/local/nginx/nginx \
            --pid-path=/usr/local/nginx/nginx.pid \
            --error-log-path=/usr/local/nginx/error.log \
            --http-log-path=/usr/local/nginx/access.log \
            --with-http_ssl_module \
            --with-http_v2_module \
            --with-stream \
            --with-openssl=../openssl-1.1.0b \
            --with-openssl-opt=no-weak-ssl-ciphers \
            --with-openssl-opt=no-ssl3 \
            --with-pcre=../pcre-8.42 \
            --with-zlib=../zlib-1.2.11

# or other example:
./configure --user=nginx \
            --group=nginx \
            --prefix=/etc/nginx \
            --conf-path=/etc/nginx/nginx.conf \
            --sbin-path=/usr/sbin/nginx \
            --pid-path=/var/run/nginx.pid \
            --lock-path=/var/run/nginx.lock \
            --modules-path=/usr/lib64/nginx/modules \
            --error-log-path=/var/log/nginx/error.log \
            --http-log-path=/var/log/nginx/access.log \
            --http-client-body-temp-path=/var/cache/nginx/client_temp \
            --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
            --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
            --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
            --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
            --with-openssl=../openssl-1.1.0b \
            --with-openssl-opt=no-weak-ssl-ciphers \
            --with-openssl-opt=no-ssl3 \
            --with-pcre=../pcre-8.42 \
            --with-pcre-jit \
            --with-zlib=../zlib-1.2.11 \
            --with-compat \
            --with-file-aio \
            --with-threads \
            --with-http_addition_module \
            --with-http_auth_request_module \
            --with-http_gunzip_module \
            --with-http_gzip_static_module \
            --with-http_random_index_module \
            --with-http_realip_module \
            --with-http_secure_link_module \
            --with-http_slice_module \
            --with-http_ssl_module \
            --with-http_stub_status_module \
            --with-http_sub_module \
            --with-http_v2_module \
            --with-stream \
            --with-stream_realip_module \
            --with-stream_ssl_module \
            --with-stream_ssl_preread_module \
            --with-cc-opt='-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -m64 -mtune=generic -fPIC' \
            --with-ld-opt='-Wl,-z,relro -Wl,-z,now -pie'

# Compile and install:
make && make install
```

#### Installation from prebuilt packages

##### RHEL7 or CentOS 7

###### From EPEL

```bash
# Install epel repository:
yum install epel-release
# or alternative:
#   wget -c https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
#   yum install epel-release-latest-7.noarch.rpm

# Install Nginx:
yum install nginx
```

###### From Software Collections

```bash
# Install and enable scl:
yum install centos-release-scl
yum-config-manager --enable rhel-server-rhscl-7-rpms

# Install Nginx (rh-nginx14, rh-nginx16, rh-nginx18):
yum install rh-nginx16

# Enable Nginx from SCL:
scl enable rh-nginx16 bash
```

###### From Official Repository

```bash
# Where:
#   - <os_type> is: rhel or centos
cat > /etc/yum.repos.d/nginx.repo << __EOF__
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/<os_type>/$releasever/$basearch/
gpgcheck=0
enabled=1
__EOF__

# Install Nginx:
yum install nginx
```

##### Debian or Ubuntu

Check available flavors of Nginx before install. For more information please see [this](https://askubuntu.com/a/556382) great answer by [Thomas Ward](https://askubuntu.com/users/10616/thomas-ward).

###### From Debian/Ubuntu Repository

```bash
# Install Nginx:
apt-get install nginx
```

###### From Official Repository

```bash
# Where:
#   - <os_type> is: debian or ubuntu
#   - <os_release> is: xenial, bionic, jessie, stretch or other
cat > /etc/apt/sources.list.d/nginx.list << __EOF__
deb http://nginx.org/packages/<os_type>/ <os_release> nginx
deb-src http://nginx.org/packages/<os_type>/ <os_release> nginx
__EOF__

# Update packages list:
apt-get update

# Download the public key (or <pub_key> from your GPG error):
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <pub_key>

# Install Nginx:
apt-get update
apt-get install nginx
```

#### Nginx directories and files

  > If you compile Nginx server by default all files and directories are available from `/usr/local/nginx` location.

For prebuilt Nginx package paths can be as follows:

- `/etc/nginx` - is the default configuration root for the Nginx service
- `/etc/nginx/nginx.conf` - is the default configuration entry point used by the Nginx services. Includes the top-level http block and all other configuration files
- `/usr/share/nginx` - is the default root directory for requests, contains `html` directory and basic static files
- `/var/log/nginx` - is the default log (access and error log) location for Nginx
- `/var/lib/nginx` or `/var/cache/nginx` - is the default temporary files location for Nginx
- `/etc/nginx/conf`, `/etc/nginx/conf.d` or `/etc/nginx/sites-enabled` - contains custom/vhosts configuration files
- `/usr/local/nginx/logs` or `/var/run/nginx` - contains information about Nginx process(es)

#### Nginx commands

- `nginx -h` - shows the help
- `nginx -v` - shows the Nginx version
- `nginx -V` - shows the extended information about Nginx: version, build parameters and configuration arguments
- `nginx -t` - tests the Nginx configuration
- `nginx -c` - sets configuration file (default: `/etc/nginx/nginx.conf`)
- `nginx -p` - sets prefix path (default: `/etc/nginx/`)
- `nginx -T` - tests the Nginx configuration and prints the validated configuration on the screen
- `nginx -s` - sends a signal to the Nginx master process:
  - `stop` - discontinues the Nginx process immediately
  - `quit` - stops the Nginx process after it finishes processing
inflight requests
  - `reload` - reloads the configuration without stopping Nginx processes
  - `reopen` - instructs Nginx to reopen log files
- `nginx -g` - sets [global directives](https://nginx.org/en/docs/ngx_core_module.html) out of configuration file

#### Nginx processes

Nginx has **one master process** and **one or more worker processes**.

The main purpose of the master process is to read and evaluate configuration files, as well as maintain the worker processes.

Master process should be started as **root** user, because this will allow Nginx to open sockets below 1024 (it needs to be able to listen on port 80 for HTTP and 443 for HTTPS).

The worker processes do the actual processing of requests. These are spawned by the master process, and the user and group will as specified (unprivileged).

  > Nginx has also cache loader and cache manager processes but only if you enable caching.

The following signals can be sent to the Nginx master process:

| <b>SIGNAL</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `TERM`, `INT` | quick shutdown |
| `QUIT` | graceful shutdown |
| `KILL` | halts a stubborn process |
| `HUP` | configuration reload, start new workers, gracefully shutdown the old worker processes |
| `USR1` | reopen the log files |
| `USR2` | upgrade executable on the fly |
| `WINCH` | gracefully shutdown the worker processes |

There’s no need to control the worker processes yourself. However, they support some signals too:

| <b>SIGNAL</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `TERM`, `INT` | quick shutdown |
| `QUIT` | graceful shutdown |
| `USR1` | reopen the log files |

#### Nginx contexts

The Nginx contexts structure looks like this:

```
Global/Main Context
        |
        |
        +-----» Events Context
        |
        |
        +-----» HTTP Context
        |          |
        |          |
        |          +-----» Server Context
        |          |          |
        |          |          |
        |          |          +-----» Location Context
        |          |
        |          |
        |          +-----» Upstream Context
        |
        |
        +-----» Mail Context
```

#### Error log severity levels

The following is a list of all severity levels:

| <b>TYPE</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `debug` | information that can be useful to pinpoint where a problem is occurring |
| `info` | informational messages that aren’t necessary to read but may be good to know |
| `notice` | something normal happened that is worth noting |
| `warn` | something unexpected happened, however is not a cause for concern |
| `error` | something was unsuccessful, contains the action of limiting rules |
| `crit` | important problems that need to be addressed |
| `alert` | severe situation where action is needed promptly |
| `emerg` | the system is in an unusable state and requires immediate attention |

For example: if you set `crit` error log level, messages of `crit`, `alert`, and `emerg` levels are logged.

#### Debugging

###### See the top 5 IP addresses in a web server log

```bash
cut -d ' ' -f1 /path/to/logfile | sort | uniq -c | sort -nr | head -5 | nl
```

###### Analyse web server log and show only 2xx http codes

```bash
tail -n 100 -f /path/to/logfile | grep "HTTP/[1-2].[0-1]\" [2]"
```

###### Analyse web server log and show only 5xx http codes

```bash
tail -n 100 -f /path/to/logfile | grep "HTTP/[1-2].[0-1]\" [5]"
```

###### Get range of dates in a web server log

```bash
# 1)
awk '/05\/Feb\/2019:09:2.*/,/05\/Feb\/2019:09:5.*/' /path/to/logfile

# 2)
awk '/'$(date -d "1 hours ago" "+%d\\/%b\\/%Y:%H:%M")'/,/'$(date "+%d\\/%b\\/%Y:%H:%M")'/ { print $0 }' /path/to/logfile
```

###### Get line rates from web server log

```bash
tail -F /path/to/logfile | pv -N RAW -lc 1>/dev/null
```

###### Trace network traffic for all Nginx processes

```bash
strace -e trace=network -p `pidof nginx | sed -e 's/ /,/g'`
```

###### List all files accessed by a Nginx

```bash
strace -ff -e trace=file nginx 2>&1 | perl -ne 's/^[^"]+"(([^\\"]|\\[\\"nt])*)".*/$1/ && print'
```

#### Rate Limiting

  > All rate limiting rules (definitions) should be added to the Nginx `http` context.

Rate limiting rules are useful for:

- traffic shaping
- traffic optimizing
- slow down the rate of incoming requests
- protect http requests flood
- protect against slow http attacks
- prevent consume a lot of bandwidth
- mitigating ddos attacks
- protect brute-force attacks

Nginx has following variables (unique keys) that can be used in a rate limiting rules:

| <b>VARIABLE</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `$remote_addr` | client address |
| `$binary_remote_addr`| client address in a binary form, it is smaller and saves space then `remote_addr` |
| `$server_name` | name of the server which accepted a request |
| `$request_uri` | full original request URI (with arguments) |
| `$query_string` | arguments in the request line |

<sup><i>Please see [official doc](https://nginx.org/en/docs/http/ngx_http_core_module.html#variables) for more information about variables.</i></sup>

Nginx also provides following keys:

| <b>KEY</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `limit_req_zone` | stores the current number of excessive requests |
| `limit_conn_zone` | stores the maximum allowed number of connections |

and directives:

| <b>DIRECTIVE</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `limit_req` | sets the shared memory zone and the maximum burst size of requests |
| `limit_conn` | sets the shared memory zone and the maximum allowed number of connections to the server per a client IP |

Keys are used to store the state of each IP address and how often it has accessed a limited object. This information are stored in shared memory available from all Nginx worker processes.

Both keys also provides response status parameters indicating too many requests or connections with specific http code (default **503**).

- `limit_req_status <value>`
- `limit_conn_status <value>`

For example, if you want to set the desired logging level for cases when the server limits the number of connections:

```
# Add this to http context:
limit_req_status 429;

# Set your own error page for 429 http code:
error_page 429 /rate_limit.html;
location = /rate_limit.html {
  root /usr/share/www/http-error-pages/sites/other;
  internal;
}

# And create this file:
cat > /usr/share/www/http-error-pages/sites/other/rate_limit.html << __EOF__
HTTP 429 Too Many Requests
__EOF__
```

Rate limiting rules also have zones that lets you define a shared space in which to count the incoming requests or connections.

  > All requests or connections coming into the same space will be counted in the same rate limit. This is what allows you to limit per URL, per IP, or anything else.

The zone has two required parts:

- `<name>` - is the zone identifier
- `<size>` - is the zone size

Example:

```bash
<key> <variable> zone=<name>:<size>;
```

  > State information for about **16,000** IP addresses takes **1 megabyte**. So **1 kilobyte** zone has **16** IP addresses.

The range of zones is as follows:

- **http context**
```bash
http {

  ... zone=<name>;

```
- **server context**
```bash
server {

  ... zone=<name>;

```
- **location directive**
```bash
location /api {

  ... zone=<name>;

```

`limit_req_zone` key lets you set `rate` parameter (optional) - it defines the rate limited URL(s).

For enable queue you should use `limit_req` or `limit_conn` directives (see above). `limit_req` also provides optional parameters:

| <b>PARAMETER</b> | <b>DESCRIPTION</b> |
| :---         | :---         |
| `burst=<num>` | sets the maximum number of excessive requests that await to be processed in a timely manner; maximum requests as `rate` * `burst` in `burst` seconds |
| `nodelay`| it imposes a rate limit without constraining the allowed spacing between requests; default Nginx would return 503 response and not handle excessive requests |

  > `nodelay` parameters are only useful when you also set a `burst`.

Without `nodelay` option Nginx would wait (no 503 response) and handle excessive requests with some delay.

###### Limiting the rate of requests with burst mode

```bash
limit_req_zone $binary_remote_addr zone=req_for_remote_addr:64k rate=10r/m;
```

- key/zone type: `limit_req_zone`
- the unique key for limiter: `$binary_remote_addr`
  - limit requests per IP as following
- zone name: `req_for_remote_addr`
- zone size: `64k` (1024 IP addresses)
- rate is `0,16` request each second or `10` requests per minute (`1` request every `6` second)

Example of use:

```bash
location ~ /stats {

  limit_req zone=req_for_remote_addr burst=5;
```

- set maximum requests as `rate` * `burst` in `burst` seconds
  - with bursts not exceeding `5` requests:
    + `0,16r/s` * `5` = `0.80` requests per `5` seconds
    + `10r/m` * `5` = `50` requests per `5` minutes

Testing queue:

```bash
# siege -b -r 1 -c 12 -v https://x409.info/stats/
** SIEGE 4.0.4
** Preparing 12 concurrent users for battle.
The server is now under siege...
HTTP/1.1 200 *   0.20 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 503     0.20 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.20 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.21 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.22 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.22 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.23 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 200 *   6.22 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *  12.24 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *  18.27 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *  24.30 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *  30.32 secs:       2 bytes ==> GET  /stats/
             |
             - burst=5
             - 0,16r/s, 10r/m - 1r every 6 seconds

Transactions:              6 hits
Availability:          50.00 %
Elapsed time:          30.32 secs
Data transferred:       0.01 MB
Response time:         15.47 secs
Transaction rate:       0.20 trans/sec
Throughput:             0.00 MB/sec
Concurrency:            3.06
Successful transactions:   6
Failed transactions:       6
Longest transaction:   30.32
Shortest transaction:   0.20
```

###### Limiting the rate of requests with burst mode and nodelay

```bash
limit_req_zone $binary_remote_addr zone=req_for_remote_addr:50m rate=2r/s;
```

- key/zone type: `limit_req_zone`
- the unique key for limiter: `$binary_remote_addr`
  - limit requests per IP as following
- zone name: `req_for_remote_addr`
- zone size: `50m` (800,000 IP addresses)
- rate is `2` request each second or `120` requests per minute (`2` requests every `1` second)

Example of use:

```bash
location ~ /stats {

  limit_req zone=req_for_remote_addr burst=5 nodelay;
```

- set maximum requests as `rate` * `burst` in `burst` seconds
  - with bursts not exceeding `5` requests
    + `2r/s` * `5` = `10` requests per `5` seconds
    + `120r/m` * `5` = `600` requests per `5` minutes
- allocates slots in the queue according to the `burst` parameter with `nodelay`

Testing queue:

```bash
# siege -b -r 1 -c 12 -v https://x409.info/stats/
** SIEGE 4.0.4
** Preparing 12 concurrent users for battle.
The server is now under siege...
HTTP/1.1 200 *   0.18 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *   0.18 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *   0.19 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *   0.19 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *   0.19 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 200 *   0.19 secs:       2 bytes ==> GET  /stats/
HTTP/1.1 503     0.19 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.19 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.20 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.21 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.21 secs:    1501 bytes ==> GET  /stats/
HTTP/1.1 503     0.22 secs:    1501 bytes ==> GET  /stats/
             |
             - burst=5 with nodelay
             - 2r/s, 120r/m - 1r every 0.5 second

Transactions:              6 hits
Availability:          50.00 %
Elapsed time:           0.23 secs
Data transferred:       0.01 MB
Response time:          0.39 secs
Transaction rate:      26.09 trans/sec
Throughput:             0.04 MB/sec
Concurrency:           10.17
Successful transactions:   6
Failed transactions:       6
Longest transaction:    0.22
Shortest transaction:   0.18
```

###### Limiting the number of connections

```bash
limit_conn_zone $binary_remote_addr zone=conn_for_remote_addr:1m;
```

- key/zone type: `limit_conn_zone`
- the unique key for limiter: `$binary_remote_addr`
  - limit requests per IP as following
- zone name: `conn_for_remote_addr`
- zone size: `1m` (16,000 IP addresses)

Example of use:

```bash
location ~ /stats {

  limit_conn conn_for_remote_addr 1;
```

- limit a single IP address to make no more than `1` connection from IP at the same time

Testing queue:

```bash
# siege -b -r 1 -c 100 -t 10s --no-parser https://x409.info/stats/
defaulting to time-based testing: 10 seconds
** SIEGE 4.0.4
** Preparing 100 concurrent users for battle.
The server is now under siege...
Lifting the server siege...
Transactions:            364 hits
Availability:          32.13 %
Elapsed time:           9.00 secs
Data transferred:       1.10 MB
Response time:          2.37 secs
Transaction rate:      40.44 trans/sec
Throughput:             0.12 MB/sec
Concurrency:           95.67
Successful transactions: 364
Failed transactions:     769
Longest transaction:    1.10
Shortest transaction:   0.38
```

#### Shell aliases

```bash
alias ng.test='nginx -t -c /etc/nginx/nginx.conf'

alias ng.stop='ng.test && systemctl stop nginx'

alias ng.reload='ng.test && systemctl reload nginx'
alias ng.reload='ng.test && kill -HUP $(cat /var/run/nginx.pid)'
#                       ... kill -HUP $(ps auxw | grep [n]ginx | grep master | awk '{print $2}')

alias ng.restart='ng.test && systemctl restart nginx'
alias ng.restart='ng.test && kill -QUIT $(cat /var/run/nginx.pid) && /usr/sbin/nginx'
#                        ... kill -QUIT $(ps auxw | grep [n]ginx | grep master | awk '{print $2}') ...
```

# Base Rules

#### :beginner: Organising Nginx configuration

###### Rationale

  > When your Nginx configuration grow, the need for organising your configuration will also grow. Well organised code is:

  > - easier to understand
  > - easier to maintain
  > - easier to work with

  > Use `include` directive to move common server settings into a separate files and to attach your Nginx specific code to global config, contexts and other.

###### Example

```bash
# Store this configuration in e.g. https-ssl-common.conf
listen 10.240.20.2:443 ssl;

root /etc/nginx/error-pages/other;

ssl_certificate /etc/nginx/domain.com/certs/nginx_domain.com_bundle.crt;
ssl_certificate_key /etc/nginx/domain.com/certs/domain.com.key;

# And include this file in server section:
server {

  include /etc/nginx/domain.com/commons/https-ssl-common.conf;

  server_name domain.com www.domain.com;

  ...
```

###### External resources

- [Organize your data and code](https://kbroman.org/steps2rr/pages/organize.html)

#### :beginner: Separate listen directives for 80 and 443

###### Rationale

  > I don't like duplicating the rules, but it's certainly an easy and maintainable way.

###### Example

```bash
# For http:
server {

  listen 10.240.20.2:80;

  ...

}

# For https:
server {

  listen 10.240.20.2:443 ssl;

  ...

}
```

###### External resources

- [Understanding the Nginx Configuration File Structure and Configuration Contexts](https://www.digitalocean.com/community/tutorials/understanding-the-nginx-configuration-file-structure-and-configuration-contexts)

#### :beginner: Prevent processing requests with undefined server names

###### Rationale

  > Nginx should prevent processing requests with undefined server names (also on IP address). It also protects against configuration errors and don't pass traffic to incorrect backends. The problem is easily solved by creating a default catch all server config.

  > If none of the listen directives have the `default_server` parameter then the first server with the `address:port` pair will be the default server for this pair.

  > If someone makes a request using an IP address instead of a server name, the `Host` request header field will contain the IP address and the request can be handled using the IP address as the server name.

  > Also good point is `return 444;` for default server name because this will close the connection and log it internally, for any domain that isn't defined in Nginx.

###### Example

```bash
# Place it at the beginning of the configuration file to prevent mistakes.
server {

  # Add default_server to your listen directive in the server that you want to act as the default.
  listen 10.240.20.2:443 default_server ssl;

  # We catch:
  #   - invalid domain names
  #   - requests without the "Host" header
  #   - and all others (also due to the above setting)
  server_name _ "" default_server;

  ...

  return 444;

  # We can also serve:
  # location / {

    # static file (error page):
    # root /etc/nginx/error-pages/404;
    # or redirect:
    # return 301 https://badssl.com;

    # return 444;

  # }

}

server {

  listen 10.240.20.2:443 ssl;

  server_name domain.com;

  ...

}

server {

  listen 10.240.20.2:443 ssl;

  server_name domain.org;

  ...

}
```

###### External resources

- [Server names](https://nginx.org/en/docs/http/server_names.html)
- [How nginx processes a request](https://nginx.org/en/docs/http/request_processing.html)
- [nginx: how to specify a default server](https://blog.gahooa.com/2013/08/21/nginx-how-to-specify-a-default-server/)

#### :beginner: Use `reload` method to change configurations on the fly

###### Rationale

  > Use the `reload` method of Nginx to achieve a graceful reload of the configuration without stopping the server and dropping any packets.

  > This ability of Nginx is very critical in a high-uptime, dynamic environments for keeping the load balancer or standalone server online.

  > When you restart Nginx you might encounter situation in which Nginx will stop, and won't start back again, because of syntax error. Reload method is safer than restarting because before old process will be terminated, new configuration file is parsed and whole process is aborted if there are any problems with it.

###### Example

```bash
# 1)
systemctl reload nginx

# 2)
service nginx reload

# 3)
/etc/init.d/nginx reload

# 4)
/usr/sbin/nginx -s reload

# 5)
kill -HUP $(cat /var/run/nginx.pid)
# or
kill -HUP $(ps auxw | grep [n]ginx | grep master | awk '{print $2}')
```

###### External resources

- [Changing Configuration](https://nginx.org/en/docs/control.html#reconfiguration)

#### :beginner: Use only one SSL config for specific listen directive

###### Rationale

  > For sharing a single IP address between several HTTPS servers you should use one SSL config (e.g. protocols, ciphers, curves) because changes will affect only the default server.

  > Remember that regardless of SSL parameters, you are able to use multiple SSL certificates.

  > If you want to set up different SSL configurations for the same IP address then it will fail. It's important because SSL configuration is presented for default server - if none of the listen directives have the `default_server` parameter then the first server in your configuration. So you should use only one SSL setup with several names on the same IP address.

  > It's also to prevent mistakes and configuration mismatch.

###### Example

```bash
# Store this configuration in e.g. https.conf
listen 192.168.252.10:443 default_server ssl http2;

ssl_protocols TLSv1.2;
ssl_ciphers "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384";

ssl_prefer_server_ciphers on;

ssl_ecdh_curve secp521r1:secp384r1;

...

# Include this file to the server context (attach domain-a.com for specific listen directive)
server {

  include /etc/nginx/https.conf;

  server_name domain-a.com;

  ...

}

# Include this file to the server context (attach domain-b.com for specific listen directive)
server {

  include /etc/nginx/https.conf;

  server_name domain-b.com;

  ...

}
```

###### External resources

- [Nginx one ip and multiple ssl certificates](https://serverfault.com/questions/766831/nginx-one-ip-and-multiple-ssl-certificates)

#### :beginner: Force all connections over TLS

###### Rationale

  > You should always use HTTPS instead of HTTP to protect your website, even if it doesn’t handle sensitive communications.

###### Example

```bash
server {

  listen 10.240.20.2:80;

  server_name domain.com;

  return 301 https://$host$request_uri;

}

server {

  listen 10.240.20.2:443 ssl;

  server_name domain.com;

  ...

}
```

###### External resources

- [Should we force user to HTTPS on website?](https://security.stackexchange.com/questions/23646/should-we-force-user-to-https-on-website)

#### :beginner: Use geo/map modules instead allow/deny

###### Rationale

  > Creates variables with values depending on the client IP address. Use map or geo modules (one of them) to prevent users abusing your servers.

###### Example

```bash
# Map module:
map $remote_addr $globals_internal_map_acl {

  # Status code:
  #  - 0 = false
  #  - 1 = true
  default 0;

  ### INTERNAL ###
  10.255.10.0/24 1;
  10.255.20.0/24 1;
  10.255.30.0/24 1;
  192.168.0.0/16 1;

}

# Geo module:
geo $globals_internal_geo_acl {

  # Status code:
  #  - 0 = false
  #  - 1 = true
  default 0;

  ### INTERNAL ###
  10.255.10.0/24 1;
  10.255.20.0/24 1;
  10.255.30.0/24 1;
  192.168.0.0/16 1;

}
```

###### External resources

- [Nginx Basic Configuration (Geo Ban)](https://www.axivo.com/resources/nginx-basic-configuration.3/update?update=27)

#### :beginner: Map all the things...

###### Rationale

  > Manage a large number of redirects with Nginx maps.

  > Map module provides a more elegant solution for clearly parsing a big list of regexes, e.g. User-Agents.

###### Example

```bash
map $http_user_agent $device_redirect {

  default "desktop";

  ~(?i)ip(hone|od) "mobile";
  ~(?i)android.*(mobile|mini) "mobile";
  ~Mobile.+Firefox "mobile";
  ~^HTC "mobile";
  ~Fennec "mobile";
  ~IEMobile "mobile";
  ~BB10 "mobile";
  ~SymbianOS.*AppleWebKit "mobile";
  ~Opera\sMobi "mobile";

}

if ($device_redirect = "mobile") {

  return 301 https://m.domain.com$request_uri;

}
```

###### External resources

- [Cool Nginx feature of the week](https://www.ignoredbydinosaurs.com/posts/236-cool-nginx-feature-of-the-week)

#### :beginner: Drop the same root inside location block

###### Rationale

  > If you add a root to every location block then a location block that isn’t matched will have no root. Set global `root` inside server directive.

###### Example

```bash
server {

  server_name domain.com;

  root /var/www/domain.com/public;

  location / {

    ...

  }

  location /api {

    ...

  }

  location /static {

    root /var/www/domain.com/static;

    ...

  }

}
```

###### External resources

- [Nginx Pitfalls: Root inside location block](http://wiki.nginx.org/Pitfalls#Root_inside_Location_Block)

#### :beginner: Use debug mode for debugging

###### Rationale

  > There's probably more detail than you want, but that can sometimes be a lifesaver (but log file growing rapidly on a very high-traffic sites).

###### Example

```bash
rewrite_log on;
error_log /var/log/nginx/error-debug.log debug;
```

###### External resources

- [A debugging log](https://nginx.org/en/docs/debugging_log.html)

#### :beginner: Use custom log formats for debugging

###### Rationale

  > Anything you can access as a variable in Nginx config, you can log, including non-standard http headers, etc. so it's a simple way to create your own log format for specific situations.

  > This is extremely helpful for debugging specific `location` directives.

###### Example

```bash
# Default main log format from nginx repository:
log_format main
                '$remote_addr - $remote_user [$time_local] "$request" '
                '$status $body_bytes_sent "$http_referer" '
                '"$http_user_agent" "$http_x_forwarded_for"';

# Extended main log format:
log_format main-level-0
                '$remote_addr - $remote_user [$time_local] '
                '"$request_method $scheme://$host$request_uri '
                '$server_protocol" $status $body_bytes_sent '
                '"$http_referer" "$http_user_agent" '
                '$request_time';

# Debug log formats:
log_format debug-level-0
                '$remote_addr - $remote_user [$time_local] '
                '"$request_method $scheme://$host$request_uri '
                '$server_protocol" $status $body_bytes_sent '
                '$request_id $pid $msec $request_time '
                '$upstream_connect_time $upstream_header_time '
                '$upstream_response_time "$request_filename" '
                '$request_completion';

log_format debug-level-1
                '$remote_addr - $remote_user [$time_local] '
                '"$request_method $scheme://$host$request_uri '
                '$server_protocol" $status $body_bytes_sent '
                '$request_id $pid $msec $request_time '
                '$upstream_connect_time $upstream_header_time '
                '$upstream_response_time "$request_filename" $request_length '
                '$request_completion $connection $connection_requests';

log_format debug-level-2
                '$remote_addr - $remote_user [$time_local] '
                '"$request_method $scheme://$host$request_uri '
                '$server_protocol" $status $body_bytes_sent '
                '$request_id $pid $msec $request_time '
                '$upstream_connect_time $upstream_header_time '
                '$upstream_response_time "$request_filename" $request_length '
                '$request_completion $connection $connection_requests '
                '$server_addr $server_port $remote_addr $remote_port';
```

###### External resources

- [Module ngx_http_log_module](https://nginx.org/en/docs/http/ngx_http_log_module.html)
- [Nginx: Custom access log format and error levels](https://fabianlee.org/2017/02/14/nginx-custom-access-log-format-and-error-levels/)
- [nginx: Log complete request/response with all headers?](https://serverfault.com/questions/636790/nginx-log-complete-request-response-with-all-headers)

# Performance

#### :beginner: Adjust worker processes

###### Rationale

  > The `worker_processes` directive is the sturdy spine of life for Nginx. This directive is responsible for letting our virtual server know many workers to spawn once it has become bound to the proper IP and port(s).

  Official Nginx documentation say:

  > _When one is in doubt, setting it to the number of available CPU cores would be a good start (the value "auto" will try to autodetect it)._

  > I think for high load proxy servers (also standalone servers) good value is `ALL_CORES - 1` (please test it before used).

###### Example

```bash
# VCPU = 4 , expr $(nproc --all) - 1
worker_processes 3;
```

###### External resources

- [Nginx Core Module - worker_processes](https://nginx.org/en/docs/ngx_core_module.html#worker_processes)

#### :beginner: Use HTTP/2

###### Rationale

  > HTTP/2 will make our applications faster, simpler, and more robust.

  > The primary goals for HTTP/2 are to reduce latency by enabling full request and response multiplexing, minimize protocol overhead via efficient compression of HTTP header fields, and add support for request prioritization and server push.

  > HTTP/2 is backwards-compatible with HTTP/1.1, so it would be possible to ignore it completely and everything will continue to work as before.

###### Example

```bash
# For https:
server {

  listen 10.240.20.2:443 ssl http2;

  ...
```

###### External resources

- [Introduction to HTTP/2](https://developers.google.com/web/fundamentals/performance/http2/)
- [What is HTTP/2 - The Ultimate Guide](https://kinsta.com/learn/what-is-http2/)
- [The HTTP/2 Protocol: Its Pros & Cons and How to Start Using It](https://www.upwork.com/hiring/development/the-http2-protocol-its-pros-cons-and-how-to-start-using-it/)

#### :beginner: Maintaining SSL sessions

###### Rationale

  > This improves performance from the clients’ perspective, because it eliminates the need for a new (and time-consuming) SSL handshake to be conducted each time a request is made.

  > Most servers do not purge sessions or ticket keys, thus increasing the risk that a server compromise would leak data from previous (and future) connections.

###### Example

```bash
ssl_session_cache shared:SSL:10m;
ssl_session_timeout 24h;
ssl_session_tickets off;
ssl_buffer_size 1400;
```

###### External resources

- [SSL Session (cache)](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_session_cache)
- [Speeding up TLS: enabling session reuse](https://vincent.bernat.ch/en/blog/2011-ssl-session-reuse-rfc5077)

#### :beginner: Use exact names where possible

###### Rationale

  > Exact names, wildcard names starting with an asterisk, and wildcard names ending with an asterisk are stored in three hash tables bound to the listen ports.

  > The exact names hash table is searched first. If a name is not found, the hash table with wildcard names starting with an asterisk is searched. If the name is not found there, the hash table with wildcard names ending with an asterisk is searched. Searching wildcard names hash table is slower than searching exact names hash table because names are searched by domain parts.

  > Regular expressions are tested sequentially and therefore are the slowest method and are non-scalable. For these reasons, it is better to use exact names where possible.

###### Example

```bash
# It is more efficient to define them explicitly:
server {

    listen       80;

    server_name  example.org  www.example.org  *.example.org;

    ...

}

# than to use the simplified form:
server {

    listen       80;

    server_name  .example.org;

    ...

}
```

###### External resources

- [Server names](https://nginx.org/en/docs/http/server_names.html)

#### :beginner: Avoid checks `server_name` with if directive

###### Rationale

  > When Nginx receives a request no matter what is the subdomain being requested, be it `www.example.com` or just the plain `example.com` this if directive is always evaluated. Since you’re requesting Nginx to check for the `Host` header for every request. It’s extremely inefficient.

  > Instead use two server directives like the example below. This approach decreases Nginx processing requirements.

###### Example

```bash
# Bad configuration:
server {

  ...

  server_name                 domain.com www.domain.com;

  if ($host = www.domain.com) {

    return                    301 https://domain.com$request_uri;

  }

  server_name                 domain.com;

  ...

}

# Good configuration:
server {

    server_name               www.domain.com;
    return                    301 $scheme://domain.com$request_uri;
    # If you force your web traffic to use HTTPS:
    #                         301 https://domain.com$request_uri;

}

server {

    listen                    80;

    server_name               domain.com;

    ...

}
```

###### External resources

- [If Is Evil](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/)

#### :beginner: Use `limit_conn` to improve limiting the download speed

###### Rationale

  > Nginx provides two directives to limiting download speed:
  >   - `limit_rate_after` - sets the amount of data transferred before the `limit_rate` directive takes effect
  >   - `limit_rate` - allows you to limit the transfer rate of individual client connections (past exceeding `limit_rate_after`)

  > This solution limits nginx download speed per connection, so, if one user opens multiple e.g. video files, it will be able to download `X * the number of times` he connected to the video files.

  > To prevent this situation use `limit_conn_zone` and `limit_conn` directives.

###### Example

```bash
# Create limit connection zone:
limit_conn_zone $binary_remote_addr zone=conn_for_remote_addr:1m;

# Add rules to limiting the download speed:
limit_rate_after 1m;  # run at maximum speed for the first 1 megabyte
limit_rate 250k;      # and set rate limit after 1 megabyte

# Enable queue:
location /videos {

  # Max amount of data by one client: 10 megabytes (limit_rate_after * 10)
  limit_conn conn_for_remote_addr 10;

  ...
```

###### External resources

- [How to Limit Nginx download Speed](https://www.scalescale.com/tips/nginx/how-to-limit-nginx-download-speed/)

# Hardening

#### :beginner: Run as an unprivileged user

###### Rationale

  > There is no real difference in security just by changing the process owner name. On the other hand in security, the principle of least privilege states that an entity should be given no more permission than necessary to accomplish its goals within a given system. This way only master process runs as root.

###### Example

```bash
# Edit nginx.conf:
user www-data;

# Set owner and group for root (app, default) directory:
chown -R www-data:www-data /var/www/domain.com
```

###### External resources

- [Why does nginx starts process as root?](https://unix.stackexchange.com/questions/134301/why-does-nginx-starts-process-as-root)

#### :beginner: Disable unnecessary modules

###### Rationale

  > It is recommended to disable any modules which are not required as this will minimize the risk of any potential attacks by limiting the operations allowed by the web server.

  > The best way to disable unused modules you should use the `configure` option during installation.

###### Example

```bash
# During installation:
./configure --without-http_autoindex_module

# Comment modules in the configuration file e.g. modules.conf:
# load_module                 /usr/share/nginx/modules/ndk_http_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_auth_pam_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_cache_purge_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_dav_ext_module.so;
load_module                   /usr/share/nginx/modules/ngx_http_echo_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_fancyindex_module.so;
load_module                   /usr/share/nginx/modules/ngx_http_geoip_module.so;
load_module                   /usr/share/nginx/modules/ngx_http_headers_more_filter_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_image_filter_module.so;
# load_module                 /usr/share/nginx/modules/ngx_http_lua_module.so;
load_module                   /usr/share/nginx/modules/ngx_http_perl_module.so;
# load_module                 /usr/share/nginx/modules/ngx_mail_module.so;
# load_module                 /usr/share/nginx/modules/ngx_nchan_module.so;
# load_module                 /usr/share/nginx/modules/ngx_stream_module.so;
```

###### External resources

- [nginx-modules](https://github.com/nginx-modules)

#### :beginner: Protect sensitive resources

###### Rationale

  > Hidden directories and files should never be web accessible.

###### Example

```bash
if ($request_uri ~ "/\.git") {

  return 403;

}

# or
location ~ /\.git {

  deny all;

}

# or
location ~* ^.*(\.(?:git|svn|htaccess))$ {

  return 403;

}

# or all . directories/files excepted .well-known
location ~ /\.(?!well-known\/) {

  deny all;

}
```

###### External resources

- [Hidden directories and files as a source of sensitive information about web application](https://medium.com/@_bl4de/hidden-directories-and-files-as-a-source-of-sensitive-information-about-web-application-84e5c534e5ad)

#### :beginner: Hide Nginx version number

###### Rationale

  > Disclosing the version of Nginx running can be undesirable, particularly in environments sensitive to information disclosure.

  The "Official Apache Documentation (Apache Core Features)" say:

  > _Setting ServerTokens to less than minimal is not recommended because it makes it more difficult to debug interoperational problems. Also note that disabling the Server: header does nothing at all to make your server more secure. The idea of "security through obscurity" is a myth and leads to a false sense of safety._

###### Example

```bash
server_tokens off;
```

###### External resources

- [Remove Version from Server Header Banner in nginx](https://geekflare.com/remove-server-header-banner-nginx/)
- [Reduce or remove server headers](https://www.tunetheweb.com/security/http-security-headers/server-header/)

#### :beginner: Hide Nginx server signature

###### Rationale

  > In my opinion there is no real reason or need to show this much information about your server. It is easy to look up particular vulnerabilities once you know the version number.

  > You should compile Nginx from sources with `ngx_headers_more` to used `more_set_headers` directive.

###### Example

```bash
more_set_headers "Server: Unknown";
```

###### External resources

- [Shhh... don’t let your response headers talk too loudly](https://www.troyhunt.com/shhh-dont-let-your-response-headers/)
- [How to change (hide) the Nginx Server Signature?](https://stackoverflow.com/questions/24594971/how-to-changehide-the-nginx-server-signature)

#### :beginner: Hide upstream proxy headers

###### Rationale

  > When Nginx is used to proxy requests to an upstream server (such as a PHP-FPM instance), it can be beneficial to hide certain headers sent in the upstream response (e.g. the version of PHP running).

###### Example

```bash
proxy_hide_header X-Powered-By;
proxy_hide_header X-AspNetMvc-Version;
proxy_hide_header X-AspNet-Version;
proxy_hide_header X-Drupal-Cache;
```

###### External resources

- [Remove insecure http headers](https://veggiespam.com/headers/)

#### :beginner: Use min. 2048-bit private keys

###### Rationale

  > Advisories recommend 2048 for now. Security experts are projecting that 2048 bits will be sufficient for commercial use until around the year 2030 (as per NIST).

  > Generally there is no compelling reason to choose 4096 bit keys over 2048 provided you use sane expiration intervals.

  > If you want to get **A+ with 100%s on SSL Lab** (for Key Exchange) you should definitely use 4096 bit private keys. That's the main reason why you should use them.

  > Longer keys take more time to generate and require more CPU (please use `openssl speed rsa` on your server) and power when used for encrypting and decrypting, also the SSL handshake at the start of each connection will be slower. It also has a small impact on the client side (e.g. browsers).

  > Use of alternative solution: ECC Certificate Signing Request (CSR).

  The "SSL/TLS Deployment Best Practices" book say:

  > _The cryptographic handshake, which is used to establish secure connections, is an operation whose cost is highly influenced by private key size. Using a key that is too short is insecure, but using a key that is too long will result in “too much” security and slow operation. For most web sites, using RSA keys stronger than 2048 bits and ECDSA keys stronger than 256 bits is a waste of CPU power and might impair user experience. Similarly, there is little benefit to increasing the strength of the ephemeral key exchange beyond 2048 bits for DHE and 256 bits for ECDHE._

  Konstantin Ryabitsev (Reddit):

  > _Generally speaking, if we ever find ourselves in a world where 2048-bit keys are no longer good enough, it won't be because of improvements in brute-force capabilities of current computers, but because RSA will be made obsolete as a technology due to revolutionary computing advances. If that ever happens, 3072 or 4096 bits won't make much of a difference anyway. This is why anything above 2048 bits is generally regarded as a sort of feel-good hedging theatre._

###### Example

```bash
### Example (RSA):
( _fd="domain.com.key" ; _len="4096" ; openssl genrsa -out ${_fd} ${_len} )

# Let's Encrypt:
certbot certonly -d domain.com -d www.domain.com --rsa-key-size 4096

### Example (ECC):
# _curve: prime256v1, secp521r1, secp384r1
( _fd="domain.com.key" ; _fd_csr="domain.com.csr" ; _curve="prime256v1" ; \
openssl ecparam -out ${_fd} -name ${_curve} -genkey ; openssl req -new -key ${_fd} -out ${_fd_csr} -sha256 )

# Let's Encrypt (from above):
certbot --csr ${_fd_csr} -[other-args]
```

For `x25519`:

```bash
( _fd="private.key" ; _curve="x25519" ; \
openssl genpkey -algorithm ${_curve} -out ${_fd} )
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **100**</sub>

```bash
( _fd="domain.com.key" ; _len="2048" ; openssl genrsa -out ${_fd} ${_len} )

# Let's Encrypt:
certbot certonly -d domain.com -d www.domain.com
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **90**</sub>

###### External resources

- [So you're making an RSA key for an HTTPS certificate. What key size do you use?](https://certsimple.com/blog/measuring-ssl-rsa-keys)

#### :beginner: Keep only TLS 1.2

###### Rationale

  > It is recommended to run TLS 1.1/1.2 and fully disable SSLv2, SSLv3 and TLS 1.0 that have protocol weaknesses.

  > TLS 1.1 and 1.2 are both without security issues - but only v1.2 provides modern cryptographic algorithms. TLS 1.0 and TLS 1.1 protocols will be removed from browsers at the beginning of 2020.

  > Before enabling specific protocol version, you should check which ciphers are supported by the protocol. So if you turn on TLS 1.2 and TLS 1.1 both remember about [the correct (and strong)](#beginner-use-only-strong-ciphers) ciphers to handle them. Otherwise, they will not be anyway works without supported ciphers.

  > If you told Nginx to use TLS 1.3, it will use TLS 1.3 only where available. Nginx supports TLS 1.3 since version 1.13.0 (released in April 2017), when built against OpenSSL 1.1.1 or more.

  > TLS 1.2 does require careful configuration to ensure obsolete cipher suites with identified vulnerabilities are not used in conjunction with it. TLS 1.3 removes the need to make these decisions.

###### Example

```bash
ssl_protocols TLSv1.2;

# To enable TLS 1.3:
ssl_protocols TLSv1.3 TLSv1.2;
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **100**</sub>

```bash
ssl_protocols TLSv1.2 TLSv1.1;
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **95**</sub>

###### External resources

- [TLS/SSL Explained – Examples of a TLS Vulnerability and Attack, Final Part](https://www.acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/)
- [Deprecating TLS 1.0 and 1.1 - Enhancing Security for Everyone](https://www.keycdn.com/blog/deprecating-tls-1-0-and-1-1)
- [TLS v1.2 handshake overview](https://medium.com/@ethicalevil/tls-handshake-protocol-overview-a39e8eee2cf5)
- [TLS1.3 - OpenSSLWiki](https://wiki.openssl.org/index.php/TLS1.3)
- [TLS1.2 - Every byte explained and reproduced](https://tls12.ulfheim.net/)
- [TLS1.3 - Every byte explained and reproduced](https://tls13.ulfheim.net/)
- [How to enable TLS 1.3 on Nginx](https://ma.ttias.be/enable-tls-1-3-nginx/)
- [An Overview of TLS 1.3 - Faster and More Secure](https://kinsta.com/blog/tls-1-3/)
- [Differences between TLS 1.2 and TLS 1.3](https://www.wolfssl.com/differences-between-tls-1-2-and-tls-1-3/)

#### :beginner: Use only strong ciphers

###### Rationale

  > This parameter changes quite often, the recommended configuration for today may be out of date tomorrow.

  > For more security use only strong and not vulnerable ciphersuite (but if you use HTTP/2 you can get `Server sent fatal alert: handshake_failure` error).

  > Place `ECDHE` and `DHE` suites at the top of your list. The order is important; because `ECDHE` suites are faster, you want to use them whenever clients supports them.

  > For backward compatibility software components you should use less restrictive ciphers.

  > You should definitely disable weak ciphers like those with `DSS`, `DSA`, `DES/3DES`, `RC4`, `MD5`, `SHA1`, `null`, anon in the name.

###### Example

Ciphersuite for TLS 1.2:

```bash
ssl_ciphers "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384";
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **100**</sub>

Ciphersuite for TLS 1.2/1.1:

```bash
# 1)
ssl_ciphers "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA256";

# 2)
ssl_ciphers "ECDHE-ECDSA-CHACHA20-POLY1305:ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:!AES256-GCM-SHA256:!AES256-GCM-SHA128:!aNULL:!MD5";
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **90**</sub>

Ciphersuite for TLS 1.3:

```bash
ssl_ciphers "TLS13-CHACHA20-POLY1305-SHA256:TLS13-AES-256-GCM-SHA384:TLS13-AES-128-GCM-SHA256";
```

###### External resources

- [TLS Cipher Suites](https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4)
- [SSL/TLS: How to choose your cipher suite](https://technology.amis.nl/2017/07/04/ssltls-choose-cipher-suite/)
- [HTTP/2 and ECDSA Cipher Suites](https://sparanoid.com/note/http2-and-ecdsa-cipher-suites/)
- [Which SSL/TLS Protocol Versions and Cipher Suites Should I Use?](https://www.securityevaluators.com/ssl-tls-protocol-versions-cipher-suites-use/)
- [Recommendations for a cipher string](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/TLS_Cipher_String_Cheat_Sheet.md)
- [Why use Ephemeral Diffie-Hellman](https://tls.mbed.org/kb/cryptography/ephemeral-diffie-hellman)
- [Cipher Suite Breakdown](https://blogs.technet.microsoft.com/askpfeplat/2017/12/26/cipher-suite-breakdown/)
- [OpenSSL IANA Mapping](https://testssl.sh/openssl-iana.mapping.html)

#### :beginner: Use more secure ECDH Curve

###### Rationale

  > For a SSL server certificate, an "elliptic curve" certificate will be used only with digital signatures (`ECDSA` algorithm).

  > `x25519` is a more secure but slightly less compatible option. To maximise interoperability with existing browsers and servers, stick to `P-256 prime256v1` and `P-384 secp384r1` curves.

  > NSA Suite B says that NSA uses curves `P-256` and `P-384` (in OpenSSL, they are designated as, respectively, `prime256v1` and `secp384r1`). There is nothing wrong with `P-521`, except that it is, in practice, useless. Arguably, `P-384` is also useless, because the more efficient `P-256` curve already provides security that cannot be broken through accumulation of computing power.

  > Use `P-256` to minimize trouble. If you feel that your manhood is threatened by using a 256-bit curve where a 384-bit curve is available, then use `P-384`: it will increases your computational and network costs.

  > If you do not set `ssh_ecdh_curve`, then the Nginx will use its default settings, e.g. Chrome will prefer `x25519`, but this is **not recommended** because you can not control the Nginx's default settings (seems to be `P-256`).

  > Explicitly set `ssh_ecdh_curve X25519:prime256v1:secp521r1:secp384r1;` **decreases the Key Exchange SSL Labs rating**.

  > Definitely do not use the `secp112r1`, `secp112r2`, `secp128r1`, `secp128r2`, `secp160k1`, `secp160r1`, `secp160r2`, `secp192k1` curves. They have a too small size for security application according to NIST recommendation.

###### Example

```bash
ssl_ecdh_curve secp521r1:secp384r1;
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **100**</sub>

```bash
# Alternative (this one doesn’t affect compatibility, by the way; it’s just a question of the preferred order).
# This setup downgrade Key Exchange score:
ssl_ecdh_curve X25519:prime256v1:secp521r1:secp384r1;
```

###### External resources

- [Standards for Efficient Cryptography Group](http://www.secg.org/)
- [SafeCurves: choosing safe curves for elliptic-curve cryptography](https://safecurves.cr.yp.to/)
- [P-521 is pretty nice prime](https://blog.cr.yp.to/20140323-ecdsa.html)
- [Safe ECC curves for HTTPS are coming sooner than you think](https://certsimple.com/blog/safe-curves-and-openssl)
- [Cryptographic Key Length Recommendations](https://www.keylength.com/)
- [Testing for Weak SSL/TLS Ciphers, Insufficient Transport Layer Protection (OTG-CRYPST-001)](https://www.owasp.org/index.php/Testing_for_Weak_SSL/TLS_Ciphers,_Insufficient_Transport_Layer_Protection_(OTG-CRYPST-001))
- [Elliptic Curve performance: NIST vs Brainpool](https://tls.mbed.org/kb/cryptography/elliptic-curve-performance-nist-vs-brainpool)
- [Which elliptic curve should I use?](https://security.stackexchange.com/questions/78621/which-elliptic-curve-should-i-use/91562)

#### :beginner: Use strong Key Exchange

###### Rationale

  > The DH key is only used if DH ciphers are used. Modern clients prefer `ECDHE` instead and if your Nginx accepts this preference then the handshake will not use the DH param at all since it will not do a `DHE` key exchange but an `ECDHE` key exchange.

  > Most of the "modern" profiles from places like Mozilla's ssl config generator no longer recommend using this.

  > Default key size in OpenSSL is `1024 bits` - it's vulnerable and breakable. For the best security configuration use your own `4096 bit` DH Group or use known safe ones pre-defined DH groups (it's recommended) from [mozilla](https://wiki.mozilla.org/Security/Server_Side_TLS#ffdhe4096).

###### Example

```bash
# To generate a DH key:
openssl dhparam -out /etc/nginx/ssl/dhparam_4096.pem 4096

# To produce "DSA-like" DH parameters:
openssl dhparam -dsaparam -out /etc/nginx/ssl/dhparam_4096.pem 4096

# To generate a ECDH key:
openssl ecparam -out /etc/nginx/ssl/ecparam.pem -name prime256v1

# Nginx configuration:
ssl_dhparam /etc/nginx/ssl/dhparams_4096.pem;
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **100**</sub>

###### External resources

- [Weak Diffie-Hellman and the Logjam Attack](https://weakdh.org/)
- [Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)
- [Pre-defined DHE groups](https://wiki.mozilla.org/Security/Server_Side_TLS#ffdhe4096)
- [Instructs OpenSSL to produce "DSA-like" DH parameters](https://security.stackexchange.com/questions/95178/diffie-hellman-parameters-still-calculating-after-24-hours/95184#95184)
- [OpenSSL generate different types of self signed certificate](https://security.stackexchange.com/questions/44251/openssl-generate-different-types-of-self-signed-certificate)

#### :beginner: Defend against the BEAST attack

###### Rationale

  > Enables server-side protection from BEAST attacks.

###### Example

```bash
ssl_prefer_server_ciphers on;
```

###### External resources

- [Is BEAST still a threat?](https://blog.ivanristic.com/2013/09/is-beast-still-a-threat.html)

#### :beginner: Disable HTTP compression (mitigation of CRIME/BREACH attacks)

###### Rationale

  > You should probably never use TLS compression. Some user agents (at least Chrome) will disable it anyways. Disabling SSL/TLS compression stops the attack very effectively.

  > Some attacks are possible (e.g. the real BREACH attack is a complicated) because of gzip (HTTP compression not TLS compression) being enabled on SSL requests. In most cases, the best action is to simply disable gzip for SSL.

  > Compression is not the only requirement for the attack to be done so using it does not mean that the attack will succeed. Generally you should consider whether having an accidental performance drop on HTTPS sites is better than HTTPS sites being accidentally vulnerable.

  > You shouldn't use HTTP compression on private responses when using TLS.

  > Compression can be (I think) okay to HTTP compress publicly available static content like css or js and HTML content with zero sensitive info (like an "About Us" page).

###### Example

```bash
gzip off;
```

###### External resources

- [Is HTTP compression safe?](https://security.stackexchange.com/questions/20406/is-http-compression-safe)
- [HTTP compression continues to put encrypted communications at risk](https://www.pcworld.com/article/3051675/http-compression-continues-to-put-encrypted-communications-at-risk.html)
- [SSL/TLS attacks: Part 2 – CRIME Attack](http://niiconsulting.com/checkmate/2013/12/ssltls-attacks-part-2-crime-attack/)
- [To avoid BREACH, can we use gzip on non-token responses?](https://security.stackexchange.com/questions/172581/to-avoid-breach-can-we-use-gzip-on-non-token-responses)
- [Don't Worry About BREACH](https://blog.ircmaxell.com/2013/08/dont-worry-about-breach.html)

#### :beginner: HTTP Strict Transport Security

###### Rationale

  > The header indicates for how long a browser should unconditionally refuse to take part in unsecured HTTP connection for a specific domain.

###### Example

```bash
add_header Strict-Transport-Security "max-age=63072000; includeSubdomains" always;
```

&nbsp;&nbsp;<sub>:arrow_up: ssllabs score: **A+**</sub>

###### External resources

- [HTTP Strict Transport Security Cheat Sheet](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)

#### :beginner: Reduce XSS risks (Content-Security-Policy)

###### Rationale

  > CSP reduce the risk and impact of XSS attacks in modern browsers.

###### Example

```bash
# This policy allows images, scripts, AJAX, and CSS from the same origin, and does not allow any other resources to load.
add_header Content-Security-Policy "default-src 'none'; script-src 'self'; connect-src 'self'; img-src 'self'; style-src 'self';" always;
```

###### External resources

- [Content Security Policy (CSP) Quick Reference Guide](https://content-security-policy.com/)
- [Content Security Policy – OWASP](https://www.owasp.org/index.php/Content_Security_Policy)

#### :beginner: Control the behavior of the Referer header (Referrer-Policy)

###### Rationale

  > Determine what information is sent along with the requests.

###### Example

```bash
add_header Referrer-Policy "no-referrer";
```

###### External resources

- [A new security header: Referrer Policy](https://scotthelme.co.uk/a-new-security-header-referrer-policy/)

#### :beginner: Provide clickjacking protection (X-Frame-Options)

###### Rationale

  > Helps to protect your visitors against clickjacking attacks. It is recommended that you use the `x-frame-options` header on pages which should not be allowed to render a page in a frame.

###### Example

```bash
add_header X-Frame-Options "SAMEORIGIN" always;
```

###### External resources

- [Clickjacking Defense Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)

#### :beginner: Prevent some categories of XSS attacks (X-XSS-Protection)

###### Rationale

  > Enable the cross-site scripting (XSS) filter built into modern web browsers.

###### Example

```bash
add_header X-XSS-Protection "1; mode=block" always;
```

###### External resources

- [X-XSS-Protection HTTP Header](https://www.tunetheweb.com/security/http-security-headers/x-xss-protection/)

#### :beginner: Prevent Sniff Mimetype middleware (X-Content-Type-Options)

###### Rationale

  > It prevents the browser from doing MIME-type sniffing (prevents "mime" based attacks).

###### Example

```bash
add_header X-Content-Type-Options "nosniff" always;
```

###### External resources

- [X-Content-Type-Options HTTP Header](https://www.keycdn.com/support/x-content-type-options)

#### :beginner: Deny the use of browser features (Feature-Policy)

###### Rationale

  > This header protects your site from third parties using APIs that have security and privacy implications, and also from your own team adding outdated APIs or poorly optimized images.

###### Example

```bash
add_header Feature-Policy "geolocation 'none'; midi 'none'; notifications 'none'; push 'none'; sync-xhr 'none'; microphone 'none'; camera 'none'; magnetometer 'none'; gyroscope 'none'; speaker 'none'; vibrate 'none'; fullscreen 'none'; payment 'none'; usb 'none';";
```

###### External resources

- [Feature Policy Explainer](https://docs.google.com/document/d/1k0Ua-ZWlM_PsFCFdLMa8kaVTo32PeNZ4G7FFHqpFx4E/edit)
- [Policy Controlled Features](https://github.com/w3c/webappsec-feature-policy/blob/master/features.md)

#### :beginner: Reject unsafe HTTP methods

###### Rationale

  > Set of methods support by a resource. An ordinary web server supports the `HEAD`, `GET` and `POST` methods to retrieve static and dynamic content. Other (e.g. `OPTIONS`, `TRACE`) methods should not be supported on public web servers, as they increase the attack surface.

###### Example

```bash
add_header Allow "GET, POST, HEAD" always;

if ($request_method !~ ^(GET|POST|HEAD)$) {

  return 405;

}
```

###### External resources

- [Vulnerability name: Unsafe HTTP methods](https://www.onwebsecurity.com/security/unsafe-http-methods.html)

#### :beginner: Control Buffer Overflow attacks

###### Rationale

  > Buffer overflow attacks are made possible by writing data to a buffer and exceeding that buffers’ boundary and overwriting memory fragments of a process. To prevent this in Nginx we can set buffer size limitations for all clients.

###### Example

```bash
client_body_buffer_size 100k;
client_header_buffer_size 1k;
client_max_body_size 100k;
large_client_header_buffers 2 1k;
```

###### External resources

- [SCG WS nginx](https://www.owasp.org/index.php/SCG_WS_nginx)

#### :beginner: Mitigating Slow HTTP DoS attack (Closing Slow Connections)

###### Rationale

  > Close connections that are writing data too infrequently, which can represent an attempt to keep connections open as long as possible.

###### Example

```bash
client_body_timeout 10s;
client_header_timeout 10s;
keepalive_timeout 5s 5s;
send_timeout 10s;
```

###### External resources

- [Mitigating DDoS Attacks with NGINX and NGINX Plus](https://www.nginx.com/blog/mitigating-ddos-attacks-with-nginx-and-nginx-plus/)
- [SCG WS nginx](https://www.owasp.org/index.php/SCG_WS_nginx)

# Load Balancing

#### :beginner: Tweak passive health checks

###### Rationale

  > Monitoring for health is important on all types of load balancing mainly for business continuity. Passive checks watches for failed or timed-out connections as they pass through Nginx as requested by a client.

  > This functionality is enabled by default but the parameters mentioned here allow you to tweak their behavior. Default values are: `max_fails=1` and `fail_timeout=10s`.

###### Example

```bash
upstream backend {

  server bk01_node:80 max_fails=3 fail_timeout=5s;
  server bk02_node:80 max_fails=3 fail_timeout=5s;

}
```

###### External resources

- [Module ngx_http_upstream_module](https://nginx.org/en/docs/http/ngx_http_upstream_module.html)

#### :beginner: Don't disable backends by comments, use `down` parameter

###### Rationale

  > Sometimes we need to turn off backends e.g. at maintenance-time. I think good solution is marks the server as permanently unavailable with `down` parameter even if the downtime takes a short time.

  > Comments are good for really permanently disable servers or if you want to leave information for historical purposes.

  > Nginx also provides a `backup` parameter which marks the server as a backup server. It will be passed requests when the primary servers are unavailable. I use this option rarely for the above purposes and only if I am sure that the backends will work at the maintenance time.

###### Example

```bash
upstream backend {

  server bk01_node:80 max_fails=3 fail_timeout=5s down;
  server bk02_node:80 max_fails=3 fail_timeout=5s;

}
```

###### External resources

- [Module ngx_http_upstream_module](https://nginx.org/en/docs/http/ngx_http_upstream_module.html)

# Configuration Examples

  > Remember to make a copy of the current configuration and all files/directories.

## Reverse Proxy

This chapter describes the basic configuration of my proxy server (for [blkcipher.info](https://blkcipher.info) domain).

#### Import configuration

It's very simple - clone the repo and perform full directory sync:

```bash
git clone https://github.com/trimstray/nginx-quick-reference.git
rsync -avur --delete lib/nginx/ /etc/nginx/
```

  > For leaving your configuration (not recommended) remove `--delete` rsync param.

#### Set bind IP address

###### Find and replace 192.168.252.2 string in directory and file names

```bash
cd /etc/nginx
find . -depth -name '*192.168.252.2*' -execdir bash -c 'mv -v "$1" "${1//192.168.252.2/xxx.xxx.xxx.xxx}"' _ {} \;
```

###### Find and replace 192.168.252.2 string in configuration files

```bash
cd /etc/nginx
find . -type f -print0 | xargs -0 sed -i 's/192.168.252.2/xxx.xxx.xxx.xxx/g'
```

#### Set your domain name

###### Find and replace blkcipher.info string in directory and file names

```bash
cd /etc/nginx
find . -depth -name '*blkcipher.info*' -execdir bash -c 'mv -v "$1" "${1//blkcipher.info/example.com}"' _ {} \;
```

###### Find and replace blkcipher.info string in configuration files

```bash
cd /etc/nginx
find . -type f -print0 | xargs -0 sed -i 's/blkcipher_info/example_com/g'
find . -type f -print0 | xargs -0 sed -i 's/blkcipher.info/example.com/g'
```

#### Regenerate private keys and certs

###### For localhost

```bash
cd /etc/nginx/master/_server/localhost/certs
# Private key + Self-signed certificate
( _fd="localhost.key" ; _fd_crt="nginx_localhost_bundle.crt" ; \
openssl req -x509 -newkey rsa:4096 -keyout ${_fd} -out ${_fd_crt} -days 365 -nodes \
-subj "/C=X0/ST=localhost/L=localhost/O=localhost/OU=X00/CN=localhost" )
```

###### For `default_server`

```bash
cd /etc/nginx/master/_server/defaults/certs
# Private key + Self-signed certificate
( _fd="defaults.key" ; _fd_crt="nginx_defaults_bundle.crt" ; \
openssl req -x509 -newkey rsa:4096 -keyout ${_fd} -out ${_fd_crt} -days 365 -nodes \
-subj "/C=X1/ST=default/L=default/O=default/OU=X11/CN=default_server" )
```

###### For your domain (e.g. Let's Encrypt)

```bash
cd /etc/nginx/master/_server/example.com/certs

# For multidomain:
certbot certonly -d example.com -d www.example.com --rsa-key-size 4096

# For wildcard:
certbot certonly --manual --preferred-challenges=dns -d example.com -d *.example.com --rsa-key-size 4096

# Copy private key and chain:
cp /etc/letsencrypt/live/example.com/fullchain.pem nginx_example.com_bundle.crt
cp /etc/letsencrypt/live/example.com/privkey.pem example.com.key
```

#### Add new domain

###### Updated `nginx.conf`

```bash
# At the end of the file (in 'IPS/DOMAINS' section)
include /etc/nginx/master/_server/domain.com/servers.conf;
include /etc/nginx/master/_server/domain.com/backends.conf;
```
###### Init domain directory

```bash
cd /etc/nginx/cd master/_server
cp -R example.com domain.com
cd domain.com
find . -depth -name '*example.com*' -execdir bash -c 'mv -v "$1" "${1//example.com/domain.com}"' _ {} \;
find . -type f -print0 | xargs -0 sed -i 's/example_com/domain_com/g'
find . -type f -print0 | xargs -0 sed -i 's/example.com/domain.com/g'
```

#### Test your configuration

```bash
nginx -t -c /etc/nginx/nginx.conf
```
