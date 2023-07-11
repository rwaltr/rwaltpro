---
title: Centos Stream and Kubernetes 1.20.0v
date: 2020-12-17
author: Ryan Walter
---

{{< alert >}}
This is a legacy post
{{< /alert >}}

---

{{< alert "bomb" >}}
This did not age well. CentOS Steam at the time was not easy to use. Nowadays solutions like _Talos Linux_ provide better solutions
{{< /alert >}}

I recently decided to deploy CentOS Stream due to the Recent announcement from both Redhat on their new focus and Kubernetes on their deprication of the Dockershim.

I decided to use ContainerD with Kubernetes 1.20.0V. CentOS Stream was installed with minimal install.

Currently testing a deployment using Calico as the network manager and the nfs-client-provisioner (Now known as the nfs-subdir-client-provisoner)

Eventually I will be using the following components

- Calico Network
- BGP peering
- Traefik ingress controller
- External-DNS
- Cert-Manager
- Vault Secret Manager
- Node-Discovery
- HA Control node
- Kubevirt
