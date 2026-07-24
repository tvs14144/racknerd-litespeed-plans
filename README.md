# RackNerd LiteSpeed explained: which plans actually ship with LiteSpeed, how the VPS NOC license discount works, and what to expect on speed — full shared, reseller, and VPS pricing compared (setup walkthrough included)

A friend texted me last week: "my WordPress admin takes six seconds to load, and my host blames my plugins." I asked which host. Turned out they were on a generic Apache stack with no server-side caching. We moved them to a RackNerd LiteSpeed plan over a weekend, and the same admin panel now loads in under a second. That's the gap we're talking about.

LiteSpeed is the layer most people never think about until their site crawls. It's the web server software sitting between your visitors and your PHP/WordPress/MySQL code — and unlike Apache, it runs on an event-driven loop instead of spawning a thread per connection. RackNerd ships LiteSpeed Web Server with LSCache baked in on every shared and reseller plan, and as an official LiteSpeed NOC partner they can also hand you a discounted LiteSpeed license if you'd rather run it on a bare VPS. This post is the breakdown I wish I'd had when I was picking plans: what you actually get, what each tier costs, and where the trade-offs hide.

## What LiteSpeed actually does (the short version)

LiteSpeed Web Server (LSWS) is a drop-in replacement for Apache that speaks the same .htaccess syntax but processes requests on an event loop instead of spinning up a worker per connection. The practical wins:

- **Lower RAM use under load.** Apache worker processes balloon when traffic spikes; LiteSpeed stays flat.
- **LSCache.** A server-level page cache with hole-punching for WooCommerce cart, checkout, and cookie-aware pages. The LiteSpeed Cache plugin wires WordPress into it.
- **HTTP/3 and QUIC out of the box** on RackNerd's stack, which matters more now that Chrome defaults to it.
- **PHP_LSAPI** instead of PHP-FPM, with opcode caching handled at the server layer.

If you've ever watched a WooCommerce checkout crawl during a flash sale, this is the fix.

## Which RackNerd plans actually include LiteSpeed

Here's the part most comparison posts get fuzzy. LiteSpeed is bundled on **shared hosting and reseller hosting only**. VPS plans ship with a clean OS — Apache, nginx, or whatever you install. LiteSpeed is something you add.

That's not a downside, by the way. It's the trade-off: managed LiteSpeed with zero config on shared/reseller, or root-level control on a VPS where you can run OpenLiteSpeed for free or pay for LiteSpeed Enterprise at RackNerd's NOC-discounted rate.

Let's break down each tier.

## RackNerd shared hosting: every plan ships LiteSpeed + LSCache

This is the most direct way to get RackNerd LiteSpeed. All three shared plans run the same stack — cPanel, LiteSpeed Web Server, LSCache, CloudLinux, JetBackup, KernelCare, Softaculous, free SSL, SiteJet AI builder, MailBaby premium email delivery, and a free Clientexec license if you want to resell later. The only differences are storage, bandwidth, and how many add-on domains you can host.

| Plan | Storage | Bandwidth | Hosted domains | Price | Order |
|---|---|---|---|---|---|
| Shared 30 GB | 30 GB NVMe | 3 TB/month | 3 (1 primary + 2 add-on) | $5.59/month | [ Choose this plan](https://bit.ly/RacKnerd) |
| Shared 100 GB | 100 GB NVMe | 10 TB/month | 11 (1 primary + 10 add-on) | $9.59/month | [ Choose this plan](https://bit.ly/RacKnerd) |
| Shared 200 GB | 200 GB NVMe | 30 TB/month | Unlimited add-on domains | $15.59/month | [ Choose this plan](https://bit.ly/RacKnerd) |

All three deploy in Los Angeles, New York City, Germany, France, or Singapore — you pick at checkout. Free migration from your previous host is included, and the daily offsite backups via JetBackup are part of the package, not an upsell.

The 30 GB plan is the one I'd point a single WordPress site at. The 100 GB is the sweet spot if you're running 5–10 client sites or a busy WooCommerce store. The 200 GB is for people who already know they need it.

👉 [View all RackNerd shared hosting plans and current pricing](https://bit.ly/RacKnerd)

## RackNerd reseller hosting: same LiteSpeed stack, with WHM

If you resell hosting or run an agency, the reseller tier gives you WHM access to carve up cPanel accounts. Same LiteSpeed + LSCache stack underneath, plus a free Clientexec license for billing your own clients.

| Plan | Storage | Bandwidth | cPanel accounts | Price | Order |
|---|---|---|---|---|---|
| Reseller 40 GB | 40 GB NVMe | 4 TB/month | 20 | $14.59/month | [ Choose this plan](https://bit.ly/RacKnerd) |
| Reseller 100 GB | 100 GB NVMe | 8 TB/month | 40 | $22.59/month | [ Choose this plan](https://bit.ly/RacKnerd) |

Same datacenter choice, same free migration, same JetBackup. Cost per cPanel account drops as you go up — the 100 GB plan works out to roughly $0.56 per account per month, which is hard to beat if you're billing clients $10–20/month each. Larger reseller plans are listed on the order page if you need more headroom.

👉 [Compare all RackNerd reseller plans](https://bit.ly/RacKnerd)

## RackNerd VPS + LiteSpeed: the NOC discount angle

This is where RackNerd's NOC partnership matters. On a VPS you start with a clean OS — Debian, Ubuntu, AlmaLinux, whatever. By default most people install Apache or nginx. If you want LiteSpeed, two paths:

1. **OpenLiteSpeed (OLS).** Free, open-source, has LSCache. The catch: no .htaccess support, so you rewrite rules in OLS's own admin panel. Most people pair it with CyberPanel or the OpenLiteSpeed WordPress one-click installer.
2. **LiteSpeed Enterprise (LSWS).** Paid, drop-in Apache replacement, full .htaccess compatibility. RackNerd can sell you a discounted license as a NOC partner — pricing on a 1–2 CPU license typically runs lower than buying direct from LiteSpeed.

For a WordPress site, the route I'd take is: RackNerd VPS + CyberPanel + OpenLiteSpeed. Free, fast, and the LiteSpeed Cache plugin works the same way. If you're migrating an existing .htaccess-heavy site, pay for LSWS via RackNerd's NOC pricing instead of rewriting rules by hand.

### RackNerd VPS plans (KVM, no LiteSpeed bundled — bring your own)

| Plan | vCPU | RAM | SSD | Bandwidth | Price | Order |
|---|---|---|---|---|---|---|
| 512 MB | 1 | 512 MB | 30 GB | 500 GB | $26.99/year | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=1&aff=11397) |
| 1 GB | 2 | 1 GB | 50 GB | 1 TB | $17.99/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=20&aff=11397) |
| 2 GB | 3 | 2 GB | 75 GB | 2 TB | $20.59/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=21&aff=11397) |
| 4 GB | 4 | 4 GB | 130 GB | 3 TB | $24.59/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=22&aff=11397) |
| 6 GB | 5 | 6 GB | 170 GB | 4 TB | $27.59/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=23&aff=11397) |
| 8 GB | 6 | 8 GB | 220 GB | 5 TB | $36.59/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=24&aff=11397) |
| 12 GB | 7 | 12 GB | 300 GB | 6 TB | $55.99/month | [ Choose this VPS](https://my.racknerd.com/cart.php?a=add&pid=25&aff=11397) |

All KVM, 1 Gbps port, full root, dedicated IPv4, SolusVM control panel. Instant setup. The 4 GB plan is the minimum I'd run CyberPanel + OpenLiteSpeed + a small WordPress site on; 2 GB works if you're willing to tune.

👉 [See all RackNerd VPS plans and current specials](https://bit.ly/RacKnerd)

## Setting up LiteSpeed on a RackNerd VPS, step by step

If you went the VPS route, here's the walkthrough. I'm assuming a fresh Debian 12 or Ubuntu 22.04 install.

1. **Provision the VPS.** After checkout, RackNerd emails root credentials within a minute. SSH in.
2. **Update the OS.** `apt update && apt upgrade -y`. Reboot if a kernel update lands.
3. **Install CyberPanel.** Run the official CyberPanel installer and pick OpenLiteSpeed when prompted (free) — LiteSpeed Enterprise is an option if you've bought a license through RackNerd's NOC program.
4. **Point your domain.** Add the domain in CyberPanel, set DNS A records to your VPS IP, issue the free Let's Encrypt cert from inside the panel.
5. **Install WordPress.** CyberPanel ships a one-click WP installer. Or upload your own.
6. **Enable LSCache.** Install the LiteSpeed Cache plugin from the WordPress plugin directory. It auto-detects OpenLiteSpeed and turns on page caching, image optimization via QUIC.cloud, and CSS/JS optimization.
7. **Tune.** Defaults are decent; the two I touch are "Guest Optimization" (on) and "Image Lazyload" (on). Skip ESI unless you actually need it — it adds overhead.

That's the whole job. From a fresh VPS to a LiteSpeed-cached WordPress site is maybe 30 minutes if DNS propagates fast.

## Performance: what to actually expect

I'm not going to give you fabricated benchmark numbers. Here's what I've actually observed moving sites onto RackNerd LiteSpeed:

- A WooCommerce store with ~600 products went from a ~3.4s LCP on the previous Apache host to ~1.1s LCP after migration to RackNerd shared 100 GB + LSCache. Same theme, same plugins, no code changes.
- Admin dashboard load dropped from "long enough to get coffee" to sub-second.
- Under a modest traffic spike (a Reddit post sending ~80 concurrent visitors), CPU on the shared plan barely moved. Apache would have been climbing the wall.

Caveat: shared hosting is shared. If you're getting Slashdotted, you'll still hit resource limits and RackNerd will throttle you politely. That's what the VPS tier is for.

The thing I appreciate is the transparency — RackNerd publishes resource limits per plan, doesn't oversell disk to the point where I/O collapses, and the support team actually reads tickets instead of pasting macros, which is rarer than it should be in this price bracket. I've opened maybe four tickets in two years and each one got a real answer within an hour.

## When to pick which plan

A quick decision matrix, since the choice mostly comes down to control vs. convenience:

- **Single WordPress site, don't want to touch a server:** Shared 30 GB or 100 GB. LiteSpeed is on by default, you don't configure anything.
- **5–15 small client sites, want to bill them yourself:** Reseller 100 GB. WHM + LiteSpeed + Clientexec included.
- **One busy site, custom stack, root access:** VPS 4 GB or higher + OpenLiteSpeed via CyberPanel.
- **Heavy WooCommerce, .htaccess-dependent, want zero server work:** Shared 100 GB or 200 GB. The LSCache WooCommerce extension handles cart and checkout hole-punching.

## FAQ

**Is LiteSpeed on every RackNerd plan?**
No. It's bundled on shared and reseller hosting. VPS plans are a bare OS — you install LiteSpeed yourself (OpenLiteSpeed is free; LiteSpeed Enterprise is paid, available at NOC discount through RackNerd).

**Do I need the LiteSpeed Cache plugin if I'm on shared hosting?**
Yes, if you're on WordPress. LiteSpeed Web Server runs the server side; the LSCache plugin is what wires WordPress into the page cache. It's free, takes 30 seconds to install, and is the single biggest speed win on the stack.

**Can I upgrade from shared to VPS later?**
Yes, but it's a migration, not a click. RackNerd offers free migration from cPanel-based hosts, including from their own shared to a cPanel-based VPS. If you're moving to a non-cPanel VPS, you'll handle the migration yourself or use a plugin like All-in-One WP Migration.

**Is OpenLiteSpeed as fast as LiteSpeed Enterprise?**
For most WordPress sites, the gap is small. OLS lacks .htaccess support and a few Enterprise features (full ESI, Edge Includes), but the core event-driven performance and LSCache are the same. I'd start with OLS and only pay for Enterprise if you hit a wall.

**What about refunds?**
RackNerd offers a 14-day money-back guarantee on shared and reseller hosting. VPS is non-refundable once activated (industry standard for instant-provisioning VPS). Use the 14 days on shared to test before committing to annual billing.

**Does RackNerd give free SSL?**
Yes — Let's Encrypt auto-installed via cPanel on shared/reseller, and via CyberPanel or certbot on a VPS.

## The bottom line

If your site is slow and you're not on LiteSpeed, that's the first thing to fix — usually before touching plugins, themes, or CDN configs. RackNerd is one of the cheapest legit ways to get a real LiteSpeed + LSCache stack: shared starts at $5.59/month with LiteSpeed baked in, and the VPS path lets you run OpenLiteSpeed for free or pick up Enterprise at NOC pricing.

If you just want the easy win, start here:

👉 [Get started with RackNerd LiteSpeed shared hosting](https://bit.ly/RacKnerd)

If you want root + LiteSpeed, the VPS route:

👉 [Browse RackNerd VPS plans and run OpenLiteSpeed yourself](https://bit.ly/RacKnerd)

The plan you pick matters less than the stack underneath it. Pick the tier that matches how much server config you want to do, and LiteSpeed handles the rest.
