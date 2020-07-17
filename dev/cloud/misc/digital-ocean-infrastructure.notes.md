# Provision a DigitalOcean Architecture with Terraform

## Notes

* use [**Terraform**](https://www.terraform.io/docs/index.html) by HashiCorp to provision cloud architecture;
    * group the config files by the functionality it targets, not the technology -- e.g. web-servers.tf, not droplets.tf;
    * for each functionally grouped config, put everything related to that function in there -- dns records and firewalls etc.;
    * make use of **variables** -- use a separate config to store them;
    * you can [**provision droplet packages**][cloud-init] with **cloud init** -- like Nginx, Postgresql etc.;
    * create the new infrastructure before you teardown the old one ([see here][create-first]) -- this is safer, in case of problems;
* use an [**SSH bastion**][ssh-bastion] host;
    * if you're using a VPC, this is required (because of firewall);
    * you can [automagically manage keys][ssh-keys] with [data sources][data-sources];
    * use [SSH forwarding][ssh-forwarding-explained] but make sure that you [**secure it**][secure-ssh-forwarding];
        * this isn't enough to secure it, research this; 
    * use Ansible to configure hosts if it's needed; 
* use [**TLS termination**][tls-termination-config] at the load balancer;
    * must use VPC to isolate unencrypted traffic;
    * [create the cert][tls-cert];
* use a **load balancer**
  * [configure it][loadbalancer] with Terraform;
  * create a [dns record][dns-config] for it -- the LB is what's publicly visible;
* create a **VPC**
    * Terraform can [**reuse properties**][vpc-uuid] to make it easier to include droplets into VPCs
* use [**firewalls**][firewall-config], internally and externally
    * control access to the database 
    * DO supports [tags][tags], these can be set within terraform, and used to create rules;
    * consider a [NAT gateway][nat];
        * although a little more expensive, and risky because it's a single point of failure; 
        * not necessarily more secure;

## Glossary

* **Data sources**: A way to pull read-only data from your DO account with Terraform;
* **DO**: DigitalOcean;
* **LB**: Load balancer. For this tutorial it is Nginx;
* **VPC**: Virtual Private Cloud -- a private cloud network;

## Sources

* [Primary Source | DigitalOcean | 2020](https://www.youtube.com/watch?v=Q3Dxtkgsh9I)
* [SSH Forwarding Explained | Medium | 2018][ssh-forwarding-explained]
* [Secure SSH Forwarding | HackerNews | 2020][secure-ssh-forwarding]


[tags]: https://youtu.be/Q3Dxtkgsh9I?t=17m50s
[vpc-uuid]: https://youtu.be/Q3Dxtkgsh9I?t=17m14s
[cloud-init]: https://youtu.be/Q3Dxtkgsh9I?t=18m20s
[create-first]: https://youtu.be/Q3Dxtkgsh9I?t=19m01s
[ssh-keys]: https://youtu.be/Q3Dxtkgsh9I?t=23m55s
[loadbalancer]: https://youtu.be/Q3Dxtkgsh9I?t=31m42s
[tls-termination-config]: https://youtu.be/Q3Dxtkgsh9I?t=33m11s
[tls-cert]: https://youtu.be/Q3Dxtkgsh9I?t=33m48s
[data-sources]: https://youtu.be/Q3Dxtkgsh9I?t=35m35s
[firewall-config]: https://youtu.be/Q3Dxtkgsh9I?t=36m59s
[nat]: https://youtu.be/Q3Dxtkgsh9I?t=38m34s
[dns-config]: https://youtu.be/Q3Dxtkgsh9I?t=39m34s
[ssh-bastion]: https://youtu.be/Q3Dxtkgsh9I?t=45m09s
[secure-ssh-forwarding]: https://news.ycombinator.com/item?id=19643400
[ssh-forwarding-explained]: https://medium.com/@crishantha/handing-bastion-hosts-on-aws-via-ssh-agent-forwarding-f1d2d4e8622a
