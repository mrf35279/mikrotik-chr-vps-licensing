# MikroTik VPS hosting: what the monthly price leaves out, which CHR licence you actually need, and which JustHost plan is enough (full plan table, port ceilings, 1- and 3-year cost)

JustHost.asia sells KVM virtual servers from $1.99 a month, lists MikroTik RouterOS among the systems you can install, and hands you a custom-ISO uploader when the image you want isn't on the menu. The monthly fee does not include a CHR licence. A production RouterOS instance needs a one-time key ($45 for P1, $95 for P10, $250 for P-Unlimited), and the free tier runs at 1 Mbit/s per interface, which is a lab speed rather than a production one.

What follows is every JustHost preset with its published price, the licence arithmetic, which of the three ceilings (port, licence, CPU) you hit first, and what one year versus three years actually costs.

> **Quick pick.** A VPN hub or a lab CHR fits the **Sirius** preset: 1 vCPU, 1 GB RAM, 20 GB NVMe, 300 Mbit port, **$3.51/mo** on monthly billing or **$2.81/mo** paid annually. Add a one-time **$45 P1 licence** and you're finished. A P10 key would cost $50 more and change nothing at 300 Mbit.
>
> 👉 [See JustHost's current VPS presets and prices](https://justhost.asia/?ref=196392)

## Every JustHost VPS preset, with prices

| Plan | vCPU / RAM | Storage | Port | Price | Order |
| --- | --- | --- | --- | --- | --- |
| Promo | 1 core / 512 MB | 5 GB NVMe | 10 Mbit | $0.99/mo | [Order](https://justhost.asia/?ref=196392) |
| Sirius | 1 core / 1 GB | 20 GB NVMe | 300 Mbit | $3.51/mo · $2.81/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Sirius IPv6 | 1 core / 1 GB | 20 GB NVMe | 300 Mbit | $2.61/mo · $2.09/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Arcturus | 1 core / 2 GB | 30 GB NVMe | 300 Mbit | $5.01/mo · $4.01/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Arcturus IPv6 | 1 core / 2 GB | 30 GB NVMe | 300 Mbit | $3.51/mo · $2.81/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Ainalrami | 1 core / 4 GB | 25 GB NVMe | 200 Mbit | $7.31/mo · $5.85/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Acamar | 1 core / 4 GB | 50 GB NVMe | 200 Mbit | $7.98/mo · $6.39/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Acrab | 1 core / 4 GB | 100 GB NVMe | 200 Mbit | $9.03/mo · $7.23/mo annual | [Order](https://justhost.asia/?ref=196392) |
| Acrux | 1 core / 4 GB | 500 GB NVMe | 200 Mbit | $27.28/mo · $21.83/mo annual | [Order](https://justhost.asia/?ref=196392) |

JustHost sells through a configurator, so these presets are starting points. RAM, disk and data-centre location can all be changed, and the figure at checkout is the one that applies. Traffic is unmetered on a fair-share basis, which means you share the port with other tenants rather than getting a guaranteed pipe.

## What the preset table doesn't tell you

**The IPv6 variants have no public IPv4.** They cost roughly 20% less and route fine inside RouterOS, but anything that needs to reach you over IPv4 — upstream BGP peers, most RADIUS servers, WinBox from a hotel network — needs a v4 address or a tunnel. If you're unsure which you need, pay the extra dollar.

**Backups are your problem.** JustHost's own FAQ says it doesn't run automatic backups and suggests keeping a copy on a separate server. On a router that means scheduling `/export` and shipping the file off-box on a timer.

**DDoS filtering is included** on every VPS, and migration from another provider is free. CPU, RAM and disk can be increased later without moving the server to a new machine.

**The console is your rescue hatch.** Each VPS ships with a Proxmox console in the client area, plus reinstall and reboot buttons. That's how you get back in after a firewall rule or an address-list entry locks you out of RouterOS.

**Refund terms come from JustHost's own policy page**, so read it before paying. Across this segment the window ranges from 7 days (PerLod) to 30 days (Unmeterd's pricing page, dated 2023-09-12, so treat that figure as old).

## The CHR licence is the line item that decides your plan

CHR is RouterOS compiled to run as a virtual machine. You get the same feature set as a RouterBOARD minus the hardware drivers: stateful firewall, NAT, queues, BGP, OSPF, MPLS, VLANs, IPsec, WireGuard, hotspot, managed over WinBox, WebFig, SSH or the API.

Licences are per instance, bought once, not subscribed:

| Licence | Throughput cap | One-time price |
| --- | --- | --- |
| Free | 1 Mbit/s per interface | $0 |
| P1 | 1 Gbit/s | $45 |
| P10 | 10 Gbit/s | $95 |
| P-Unlimited | none at the licence layer | $250 |

Every new instance gets a 60-day trial at any tier, so you can benchmark before committing.

There are two purchasing models and they are not interchangeable. Some hosts bundle a licence into the plan; others are bring-your-own-key, where you buy from MikroTik with your own account and apply the key yourself. JustHost lists RouterOS as an installable system but nothing in its published material says a paid CHR key is included, so budget for one. It's worth confirming at checkout if that changes your maths.

One caveat that gets lost in marketing copy: P-Unlimited lifts the licence cap only. It doesn't promise the VPS can carry the traffic.

👉 [Start with a JustHost preset and add your own CHR key](https://justhost.asia/?ref=196392)

## Port, licence, CPU: which ceiling do you hit first?

The entry presets run 200–300 Mbit ports. That sits below P1's 1 Gbit/s cap, which makes P1 the correct licence for those plans and P10 an extra $50 for headroom you cannot reach. Put the money into RAM or a second location instead.

If you configure a 1 Gbit/s port, P10 starts earning its price. Above that, the licence stops being the constraint and the CPU becomes one, because queues, firewall rules and IPsec encryption all run in software on the same cores. A sane floor for a P10 box is 2 vCPU / 4 GB, moving to 8 GB once you're running heavy queue trees with BFIFO or PCQ across a few hundred subscribers.

For a home VPN or an MTCNA lab none of this matters. A 300 Mbit port and a P1 key will carry a handful of WireGuard tunnels without strain.

## Which MikroTik VPS hosting plan fits your job

**WireGuard or IPsec hub for a dozen remote users.** Sirius with P1. Encryption at that scale won't saturate a core, and 1 GB holds the config comfortably.

**Site-to-site between two or three offices.** Arcturus if you're running OSPF plus a few hundred firewall rules; Sirius if the configuration is flat.

**BGP edge announcing your own prefixes.** Assume you'll build GRE or IPsec tunnels to your own carriers and announce from there, because most VPS providers route your IPv4 through their own edge and won't accept customer BGP sessions on their fabric. Arcturus or Ainalrami, P1.

**Cloud firewall and NAT in front of a server rack.** Arcturus. Connection tracking and rule sets consume RAM before they consume CPU.

**Hotspot or PPPoE concentrator.** Ainalrami's 4 GB is the sensible floor once you're holding a few hundred sessions with per-user queues.

**Certification lab.** Promo at $0.99 with a Free licence. The 1 Mbit cap is exactly what a lab needs, and the 10 Mbit port stops you from accidentally treating it as production.

## Putting CHR on a JustHost server

If RouterOS appears in the OS list at checkout, install it there and skip the rest. If it doesn't, JustHost's documented path works:

1. Open the client area, find the active service, click **Control**.
2. Click **Connect ISO** on the right and paste a direct link to the CHR image. It must be an ISO file, and the link must begin downloading immediately. A page with a download button won't work.
3. Wait for the confirmation email that the image is attached.
4. Open the Proxmox console using the credentials in the VPS creation email, shut the VPS down, start it again, then press Esc straight away to catch the boot menu and select the ISO entry.
5. Install, then apply your licence key from WinBox or the console.

Two details that catch people out. RouterOS on KVM expects virtio disk and network drivers, which the official CHR image carries and a generic x86 RouterOS image may not. And IP addressing is configured manually after install, with the parameters in the provisioning email rather than handed out by DHCP.

## How JustHost compares on the published numbers

|  | Entry price | CHR licence | Refund window | Port on entry plan |
| --- | --- | --- | --- | --- |
| JustHost | $1.99/mo; presets from $2.81/mo annual | Buy your own key | Set by its own policy page | 200–300 Mbit |
| Cloudzy | $3.48/mo (page shows 50% off, no end date) | Bring your own key | 14 days | 40 Gbit/s shared uplink |
| PerLod | $8.99/mo; $7.92/mo annual ($94.99/yr) | Not stated | 7 days | 1 Gbit/s |
| Cloudblast | €3.6/mo or €0.0058/hr | Not stated | Not stated | 10 Gbit/s |

"Not stated" means the provider's own page doesn't say; it isn't a no. Cloudzy also publishes 13 regions and a 99.95% uptime SLA, and its page claims 4.5/5 from 719+ Trustpilot reviews. PerLod's annual billing saves 12% across all four plans and its storage is listed as SSD rather than NVMe. Cloudblast bills hourly in euros, which suits boxes that only need to exist for a fortnight.

JustHost's entry price is the lowest of the four and its ports are the narrowest. Cloudzy and Cloudblast sell much fatter pipes at two to three times the monthly cost. That trade is the whole decision.

## One year and three years, in numbers

Basis: Sirius preset, annual billing at $2.81/mo ($33.72/yr), plus one $45 P1 key, no promo codes, prices as published at the time of writing.

- **Year 1:** $78.72
- **Year 2:** $33.72
- **Year 3:** $33.72
- **Three-year total:** $146.16

The licence is 57% of year one and 31% of the three-year total. That ratio is why the "cheap VPS" comparison is misleading if it stops at the monthly figure.

On monthly billing at $3.51 the same setup runs $87.12 for year one and $171.36 over three years, so annual billing saves about $25 across the term. Swapping in a P10 key adds $50 once, bringing year one to $96.16 on annual billing. That only pays off if you've configured a port faster than 1 Gbit/s.

## FAQ

**Can I run production on the free CHR licence?**
No. It caps at 1 Mbit/s per interface. Fine for a lab, unusable for a VPN hub or an office gateway.

**Will JustHost give me a BGP session?**
RouterOS speaks BGP, but a session needs a peer willing to accept it. Most VPS providers route your IPv4 through their own edge and won't take customer sessions. Build GRE or IPsec tunnels to your own upstreams and announce your prefixes from there.

**How long does migrating from a RouterBOARD take?**
Run `/export` on the physical box, paste the output into CHR, then fix the interface names. CHR uses ether1, ether2 rather than your hardware port names, so bindings need re-pointing. Typical configurations take well under an hour.

**What if a firewall rule locks me out?**
Proxmox console in the JustHost client area, or a reinstall. Keep an `/export` copy off the box so a reinstall costs you minutes rather than an evening.

**Monthly or annual billing?**
Annual saves about 20% on the presets ($3.51 down to $2.81). Since the CHR licence is bought once and the server is disposable, annual only makes sense if you're confident about the location and the plan size.

**Is the $0.99 Promo box enough for a CHR lab?**
For a Free-licence lab with one or two tunnels, yes. The 10 Mbit port rules out anything else.

## Before you order

- Lab, single tunnel, certification practice → Promo or Sirius, Free or P1 licence.
- VPN hub, small office edge → Sirius with P1.
- BGP edge, hotspot with hundreds of sessions → Arcturus or Ainalrami with P1.
- Anything past 1 Gbit/s → find a host with a faster port before you spend $95 on a P10 key.

Two things to confirm at checkout: whether a CHR key is bundled (assume it isn't), and when the refund window starts counting. Some providers count from the transaction rather than from server delivery, and that difference can cost you the whole first month.

👉 [Pick a JustHost preset and check today's price](https://justhost.asia/?ref=196392)
