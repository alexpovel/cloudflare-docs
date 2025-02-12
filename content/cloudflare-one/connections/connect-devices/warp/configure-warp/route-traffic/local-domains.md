---
pcx_content_type: how-to
title: Local Domain Fallback
weight: 2
---

# Configure Local Domain Fallback

By default, Cloudflare Zero Trust excludes common top level domains used for local resolution from being sent to Gateway for processing. These domains are resolved by the local DNS resolver configured for the device on its primary interface. Since these DNS requests bypass the Gateway resolver, they are not subject to Gateway DNS policies or DNS logging.

You can add additional domains to the Local Domain Fallback list and specify a DNS server to use in place of the Gateway resolver. The WARP client proxies these requests directly to the configured fallback servers.

## View local domains

To view the domains subject to Local Domain Fallback:

{{<render file="warp/_view-local-domains.md" productFolder="cloudflare-one">}}

On this page, you will see a list of domains excluded from Gateway. You can [add](#add-a-domain) or [remove](#delete-a-domain) domains from the list at any time.

{{<Aside type="warning">}}

Local Domain Fallback configuration only impacts where DNS requests get resolved, not the flow of traffic destined to those domains. If you want to prevent traffic from being sent to a specific domain or IP address, you must add those domains or IPs to your [Split Tunnel](/cloudflare-one/connections/connect-devices/warp/configure-warp/route-traffic/split-tunnels/) configuration.

{{</Aside>}}

## Add a domain

{{<render file="warp/_view-local-domains.md" productFolder="cloudflare-one">}}
4. In **Domain**, enter the domain that you want to exclude from Gateway. All prefixes under the domain are subject to the local domain fallback rule (in other words, `example.com` is interpreted as `*.example.com`).

5. {{<render file="warp/_add-local-domain-ip.md" productFolder="cloudflare-one">}}

6. Enter an optional description and select **Save domain**.

7. DNS traffic to the local domain fallback server is routed according to your [Split Tunnel](/cloudflare-one/connections/connect-devices/warp/configure-warp/route-traffic/split-tunnels/) configuration. To ensure that queries can reach your private DNS server:
   - If your DNS server is only reachable outside of the WARP tunnel (for example, via a third-party VPN), [exclude](/cloudflare-one/connections/connect-devices/warp/configure-warp/route-traffic/split-tunnels/#add-a-route) the server's IP.
   - If your DNS server is only reachable through the WARP tunnel (for example, if it is connected to Cloudflare via `cloudflared` or Magic WAN), [include](/cloudflare-one/connections/connect-devices/warp/configure-warp/route-traffic/split-tunnels/#add-a-route) the server's IP.

[Learn more](/cloudflare-one/connections/connect-devices/warp/configure-warp/route-traffic/#how-the-warp-client-handles-dns-requests) about how WARP handles DNS requests.

## Delete a domain

{{<render file="warp/_view-local-domains.md" productFolder="cloudflare-one">}}

4. Find the domain in the list and select **Delete**.

The domain will no longer be excluded from Gateway DNS policies, effective immediately.
