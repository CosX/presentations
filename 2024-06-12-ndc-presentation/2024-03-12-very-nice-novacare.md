---
marp: true
transition: "none"
enableMenu: false
---

### Building a Home Server Using Kubernetes on Old Laptops: A Sustainable Approach to Minimizing E-Waste 

🏠 + 💻 = ♻️

Karl Solgård (@KarlSolgard) NOVACARE AS

12.06.2024 @ NDC

note: Hello everybody! So nice to be here at NDC! My name is Karl Solgård. I work as a senior consultant at a company called NOVACARE. I'm currently on paternity leave so I have a lot of time to do side projects. And the side project I'm going to show today is my at-home Kubernetes cluster using recycled E-waste. (As one does when in paternity leave...)

---

## Agenda

- Motivations behind making a Kubernetes cluster at home
- How to set up k3s
- Quick overview of applications and experiences

---

## E-Waste is a big environmental challenge

![Alt text](81176701.jpg)

note: E-waste is a significant environmental challenge. A total of 154,000 tons of e-waste was collected in Norway during 2022, which is about 28 kg per person. Still, a lot of e-waste lies around Norwegian households, dusting away. How can we turn some of this waste into something useful?

---

## Harvest E-waste guts and make something useful

A "Frakenstein's Lab" Home Server 🧟‍♂️

note: I like to draw similarities to Dr. Frankenstein. We're reviving old laptops by using their logic boards to create a home lab. These laptops still pack a punch similar to many modern single-board computers. It's a shame to let such potential go to waste. Today, we're not just recycling — we're creating a monster of efficiency and sustainability that breathes new life into what was once considered electronic waste.

---

## How do we tie these computers together?🪢

![Alt text](20240213_082927.jpg)

note: Speaking of monsters! This was a picture of my home lab in the prototyping stage. My wife is embarrased that i'm showing you this image, but I'm actually proud of this! Husk spm! Coherent unit.

---

## kubernetes and k3s

How many lines of code does it take to set up a k3s instance?

note: We use k3s! I'm going to try to explain kubernetes in one sentence (wish me luck). Kubernetes is a highly configurable platform for managing and orchestrating containerized applications across a cluster of machines. k3s is a lightweight, easy-to-install variant of Kubernetes designed for simplicity and resource efficiency. Which makes this a good fit for this kind of build. Husk spm!!!

---

## Install k3s with one line

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

note: this is an overview of the relationship between my machines. We're going to install one control plane and two worker nodes which is a setup that prioritizes resourcefulness. Worker nodes execute the actual application workloads, running the containers that contain your applications. The control plane has an added role of managing the cluster, handling all administrative tasks like scheduling applications and maintaining their desired state. Gå igjennom maskinene.

---

![Alt text](image-1.png)

---

![Alt text](20240310_203712.jpg)

---

## Work in progress 🏗️

- Add smartphones as worker nodes (PostmarketOS)
- Build NAS and connect as a volume provider

note: A collegue of mine encouraged me to try adding phones to the mix. I found an awesome project called PostmarketOS. The project installs a fully fledged Alpine Linux distribution on the phone. My Galaxy S8 is not officially supported, but I've gotten some signs from the maintainers that it might be supported in recent builds...  

---

## What I run on my home lab 🥼

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

- The cluster draws about 30 W
- Monthly cost of 16,5 NOK (1,52 USD) given a kWh rate of 0,767 NOK (0,07 USD)

note: Just for fun and in the spirit of comparing apples to oranges, the minimal "free" tier to an azure kubernetes instance would be a monthly cost of 35,34 USD (1 VM, 4 GB RAM).

---

## Public services with cloudflare tunnels ☁️🔥

- No port openings needed
- Install cloudflared in the cluster
- blog.solgard.solutions handles 10.3K requests made in 2 minutes and didn't get "hugged to death" by reddit

note: Some of my services is exposed to the internet and is publicly available. I achieve this using cloudflare tunnels. This require no port openings and is just a simple configuration, mapping the services to the given DNS. Se siste punkt! k6 load testing tool.

---

## Conclusion

- Old hardware is still usable 👴
- Decrease your E-Waste 🌿
- Good way to learn Kubernetes and bragging rights of having a cluster at home 📚

---

## Thank you, NDC!

- https://blog.solgard.solutions
- https://github.com/CosX/very-nice-cluster-public
