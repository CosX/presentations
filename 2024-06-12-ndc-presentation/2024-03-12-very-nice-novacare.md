---
transition: "none"
enableMenu: false
---

### Building a Home Server Using Kubernetes on Old Laptops: A Sustainable Approach to Minimizing E-Waste 🚀

Karl Solgård, NOVACARE AS

12.06.2024 @ NDC

note: Hello! My name is Karl Solgård. I'm a senior consultant at NOVACARE during the day and I like to make stuff during the night. And one of the things that I have made is a kubernetes cluster at home using old e-waste around the house. 

---

## E-Waste is a big environmental challenge

<img src="81176701.jpg"/>

note: E-waste is a significant environmental challenge. A total of 154,000 tons of e-waste was collected in Norway during 2022, which is about 28 kg per person. Still, a lot of e-waste lies around Norwegian households, dusting away. How can we turn some of this waste into something useful?

---

## Harvest E-waste guts and make stuff!

A "Frakenstein's Lab" Home Server 🧟‍♂️

note: Like Dr. Frankenstein, who brought new life to assembled parts, we're reviving old laptops by using their logic boards to create a home lab. These laptops, relics from my student years and early career, still pack a punch equivalent to many modern single-board computers. It's a shame to let such potential go to waste. Today, we're not just recycling — we're creating a monster of efficiency and sustainability that breathes new life into what was once considered electronic waste.

---

## How do we tie these computers together?

![Alt text](20240213_082927.jpg)

---

## k3s!

How many lines of code does it take to set up a k3s instance?

note: k3s is a good match for this kind of build. It is a lightweight, easy-to-install Kubernetes distribution designed for edge computing, IoT, and small to medium-sized clusters, emphasizing simplicity and resource efficiency. Husk spm!!!

---

## Install k3s with one line!

Add the control plane:
```bash
$ curl -sfL https://get.k3s.io | sh - 
```

... and to add worker nodes:

```bash
$ curl -sfL https://get.k3s.io | 
  \ K3S_URL=https://ip-address-of-control-plane:6443 
  \ K3S_TOKEN=mynodetoken sh -
```

note: This takes about 30 seconds to run and will set up your machine as a k3s control plane! This command is also configurable to suit your needs. You can disable things that you want to replace, such as traefik and servicelb. 

---

![Alt text](image.png)

note: this is an overview of the relationship between the machines. We're going to install one control plane and two worker nodes. This setup prioritizes resourcefulness over high availability. The control plane manages the cluster, handling all administrative tasks like scheduling applications and maintaining their desired state.Worker nodes execute the actual application workloads, running the containers that comprise your applications.


---

![Alt text](image-1.png)

---

![Alt text](20240310_203712.jpg)

---

## What I run on my home lab
- AdGuard Home
- Prometheus with exporters for:
  - Blackbox (Uptime)
  - Kepler (Power consumption per service)
- Grafana
- Personal blog (blog.solgard.solutions)
- Home Assistant
- Flux for GitOps

---

## Power consumption ⚡
- The cluster draws about 30 Wh
- Monthly cost of 16,5 NOK (1,52 USD) given a kWh rate of 0,767 NOK (0,07 USD)

note: Just for fun and in the spirit of comparing apples to oranges, the minimal "free" tier to an azure kubernetes instance would be a monthly cost of 35,34 USD (1 VM, 4 GB RAM).

---

## Services on the internet with cloudflare tunnels
- No port openings needed
- Install cloudflared in the cluster
- blog.solgard.solutions survives after 10.3K requests made in 2 minutes and hasn't been "hugged to death" by reddit

---

## Thank you, NDC!

- https://blog.solgard.solutions
- https://github.com/CosX/very-nice-cluster-public