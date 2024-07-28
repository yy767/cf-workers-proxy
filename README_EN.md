<div align="center">

<h1 align="center">Cloudflare Workers Proxy</h1>

English / [简体中文](README.md)

Cloudflare Workers HTTP reverse proxy

<p>
<a href="https://www.gnu.org/licenses/gpl-3.0.html"><img src="https://img.shields.io/github/license/jonssonyan/cf-workers-proxy" alt="License: GPL-3.0"></a>
<a href="https://github.com/jonssonyan/cf-workers-proxy/stargazers"><img src="https://img.shields.io/github/stars/jonssonyan/cf-workers-proxy" alt="GitHub stars"></a>
<a href="https://github.com/jonssonyan/cf-workers-proxy/forks"><img src="https://img.shields.io/github/forks/jonssonyan/cf-workers-proxy" alt="GitHub forks"></a>
</p>

</div>

**It is recommended to set PATHNAME_REGEX or UA_REGEX for personal use, and set a custom domain name. It is forbidden to
use the proxy for the entire site, such as GitHub. Otherwise, the official risk control will not be responsible for the
account.**

Theoretically, it supports proxying any blocked domain name. You only need to set the environment variable
PROXY_HOSTNAME to the blocked domain name, and then access it through your worker custom domain name.

## Environment variables

| Name           | Required | Default | Example                | Remark                                      |
|----------------|----------|---------|------------------------|---------------------------------------------|
| PROXY_HOSTNAME | √        |         | github.com             | Proxy address hostname                      |
| PROXY_PROTOCOL | ×        | https   | https                  | Proxy address protocol                      |
| PATHNAME_REGEX | ×        |         | ^./jonssonyan/         | Regular expression for proxy address path   |
| UA_REGEX       | ×        |         | (curl)                 | Regular expression for User-Agent whitelist |
| URL302         | ×        |         | https://jonssonyan.com | 302 Redirect address                        |
| DEBUG          | ×        | false   | false                  | Enable DEBUG                                |

## Deploy

Copy [http_proxy.js](http_proxy.js), save and deploy

## Mirror repository proxy

1. Set the environment variable PROXY_HOSTNAME to the mirror repository address.

| Mirror repository | Address              |     
|-------------------|----------------------|
| docker            | registry-1.docker.io |   
| k8s-gcr           | k8s.gcr.io           |   
| k8s               | registry.k8s.io      |    
| quay              | quay.io              |   
| gcr               | gcr.io               |  
| ghcr              | ghcr.io              |   
| cloudsmith        | docker.cloudsmith.io |   
| ecr               | public.ecr.aws       |  

2. Set up a Docker registry proxy

   Replace https://dockerhub.xxx.com with your worker custom domain name

   ```bash
   mkdir -p /etc/docker
   cat >/etc/docker/daemon.json <<EOF
   {
     "registry-mirrors":["https://dockerhub.xxx.com"]
   }
   EOF
   systemctl daemon-reload
   systemctl restart docker
   ```

## Other

you can contact me at YouTube: https://www.youtube.com/@jonssonyan

If this project is helpful to you, you can buy me a cup of coffee.

<img src="https://github.com/jonssonyan/install-script/assets/46235235/cce90c48-27d3-492c-af3e-468b656bdd06" width="150" alt="Wechat sponsor code" title="Wechat sponsor code"/>

## License

[GPL-3.0](LICENSE)