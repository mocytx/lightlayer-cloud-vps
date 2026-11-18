# LightLayer Cloud VPS: What the $4 Plan Actually Includes, Why the Taiwan Premium Cart Shows 10–20 Mbps, and When CN2 Is Worth Paying For (Specs, Test IPs, Refund Rules)

LightLayer's own pricing page sells a **$4/month** cloud VPS, and its Taiwan Premium order page sells two 1 vCPU / 1GB / 50GB machines at **10 Mbps and 20 Mbps** with a **$9.00 monthly total** printed at the bottom. Both numbers exist. They describe different products, and the space between them is where most buying mistakes happen: the $4 tier never says which city or route you get, and the $9 page never says which of the two Taiwan plans that total belongs to.

Below are the plans LightLayer actually publishes, the prices that only exist in review articles, the per-route test IPs the company posted itself, and the refund rule that should decide whether the cheap box is worth your card details.

> **Quick pick.** A small Asia node for a site, a cron box, or a dev environment: TW-VP02 at 10 Mbps unmetered, if a non-native IP is fine for your use. Traffic from mainland China where latency matters: a Premium route plan, pinged from your own machine before you pay. Native IP, sustained throughput above 20 Mbps, or money back if you change your mind: none of these plans.
>
> 👉 [See the current plan list and prices in LightLayer's account center](https://account.lightlayer.net/?affid=74)

## Every LightLayer cloud VPS plan I could confirm

The first table is what appears on LightLayer's own pages. The second is what review articles and a 2024 promotional post claim, with no current page backing it up. Mixing the two is how the "$4 with 100 Mbps unlimited in Asia" story got started.

| Plan | Specs | Bandwidth & IP | Price | Where the numbers come from | Order |
| --- | --- | --- | --- | --- | --- |
| Startup | 1 core, 1GB RAM, 1 IPv4 (storage not listed) | 100M port, unlimited data, **not upgradeable** | $4.00/mo | LightLayer pricing page | [Check price](https://account.lightlayer.net/?affid=74) |
| Pay As You Go | from 2 cores, 2GB RAM, 1 IPv4 | 200M port, unlimited data, upgradeable | from $5.60/mo | LightLayer pricing page | [Check price](https://account.lightlayer.net/?affid=74) |
| Business | 32 cores, 32GB RAM, 1 IPv4 | 200M port, unlimited data, upgradeable | $53.60/mo | LightLayer pricing page | [Check price](https://account.lightlayer.net/?affid=74) |
| TW-VP02 | 1 vCPU, 1GB RAM, 50GB SSD | **10 Mbps, unmetered**, 1 IPv4 (**non-native**) | $9.00/mo page total, plan not specified | LightLayer Taiwan Premium cart | [Check price](https://account.lightlayer.net/?affid=74) |
| TW-VP04 | 1 vCPU, 1GB RAM, 50GB SSD | **20 Mbps, 1TB**, 1 IPv4 (**non-native**) | same $9.00/mo page total | LightLayer Taiwan Premium cart | [Check price](https://account.lightlayer.net/?affid=74) |

Reported but not confirmed on any page I could open:

| Plan | Specs | Bandwidth & route | Price | Status |
| --- | --- | --- | --- | --- |
| Mid-Tier | 4 cores, 4GB, 80GB SSD | 200 Mbps unlimited, Standard or Premium | ~$11–18/mo | Review articles only |
| Manila annual | 1 core, 1GB, 50GB SSD | Premium / Standard / Global options | $24.99/yr | Review articles, plus LightLayer's 2024 promo post |
| Taiwan annual | 1 core, 1GB, 50GB SSD | Premium 20M unmetered or 30M/1TB | $24.99/yr | Same |
| Los Angeles annual | 1 core, 1GB, 50GB SSD | Global / Standard / Premium | $29.99 / $39.99 / $49.99 per year | Review articles only, and they conflict with the 2024 post |

Two things about that second table. The 2024 promotional post on LightLayer's own site lists Los Angeles annual 1C/1G at $24.99 as well, with the port speed and data cap changing by route, while review articles quote $29.99 to $49.99 for the same city. Nobody has published a current official annual price list, so treat every yearly figure here as something to verify in the cart, not a fact.

## What the $4 plan includes, and what it leaves out

The pricing page is short: 1 core, 1GB RAM, 1 IPv4, 100M speed port, unlimited data, **not upgradeable**. That last word matters more than the price. You cannot add RAM or cores to a Startup box later; the growth path is Pay As You Go, which starts at 2 cores and 2GB for $5.60 and is upgradeable.

The page also doesn't list storage, and it doesn't attach a city or a network route to any of the three tiers. Review articles fill that gap by putting 1 core / 1GB at $4 on the Global route in Los Angeles, $5.60 on Standard, and $7+ on Premium. If those numbers are right, the $4 plan is the cheapest, least optimized path in the fleet, not a cheap ticket into the Asia network.

The per-core math on the top tier is worth a look: $53.60 for 32 cores works out to about $1.68 per core, against $2.80 per core at the Pay As You Go entry point. It's the best value per core on the page and the least flexible thing on it. Batch jobs, build runners, and CI farms fit. A single site does not.

## Taiwan Premium: the plans behind the $9.00 total

The Taiwan Premium order page is the most concrete Asia pricing LightLayer shows. Both plans are 1 vCPU, 1GB RAM, 50GB SSD, one IPv4 marked **Non-Native IP**, and both are upgradeable. TW-VP02 gives you 10 Mbps with unmetered data; TW-VP04 gives 20 Mbps with a 1TB monthly cap.

Put that next to the $4 Startup plan and the trade is obvious. You pay roughly double for a fifth of the port speed, and what you buy with the difference is the route, not the hardware. If the route isn't worth anything to you, this page has nothing for you.

The non-native IP is the harder limit. It means the address isn't registered in the country the server sits in, which shows up in geo-databases, some streaming and banking checks, and anything that cares whether an IP is residential, native, or datacenter. If your project needs a native Taiwan address, stop here; no amount of configuration fixes it.

One structural detail from LightLayer's own promotional writing: the Taiwan location is described as offering **Premium and Global** lines only, while Los Angeles is described as offering Premium, Standard, and Global. Review articles say most locations carry all three tiers. For Taiwan, the official page is the one to trust, and it says two.

## Premium, Standard, Global, and how to test before you pay

Premium runs over CN2 GIA (China Telecom's premium backbone) plus CMIN2 (China Mobile's transit). Standard is ordinary BGP transit. Global is international BGP with no regional optimization, and it's the cheapest of the three wherever all three exist.

The price ladder from the Los Angeles comparison in review articles, same 1 core / 1GB specs: $4 Global, $5.60 Standard, $7+ Premium. You are buying a path, and the path is the expensive part.

Here's the part most write-ups skip. LightLayer published test IPs for each route in its own promotional post:

- Los Angeles: Premium **38.61.2.254**, Standard **38.61.5.254**, Global **38.61.7.254**
- Taiwan: Premium **46.8.124.242**, Global **46.8.126.64**
- Manila: Premium **154.39.138.254**, Global **154.39.140.254**

Ping and traceroute those from where your users actually sit, during their busy hours, before you order anything. The post carrying those addresses dates from 2024, so if one doesn't answer, ask support for the current set rather than assuming the route is down. Five minutes of this tells you more than any review, including this one.

If your audience isn't in mainland China or nearby Asia, Premium is money spent on transit you'll never feel. Standard or Global handles a Europe or US-facing site fine.

👉 [Compare the current plan list before you pick a route](https://account.lightlayer.net/?affid=74)

## The annual question, and the 4x gap nobody quotes together

$24.99 a year works out to about **$2.08 a month**. The Taiwan cart page shows a $9.00 monthly total. Run both: $9 a month is $108 a year. That's a fourfold difference for hardware that looks identical on paper.

Whether the comparison is fair is the open question. The annual figure comes from a 2024 promotion covering Los Angeles, Taiwan, and Manila, and the current cart total doesn't specify which plan it belongs to. Before paying a year up front, confirm four things match: same datacenter, same route, same port speed and data cap, same IP type. A $24.99 annual plan on the Global line and a $9 monthly plan on Premium are not the same product at different prices.

The 2024 post also does something useful at a single price point. It lets you choose **20 Mbps unmetered** or **30 Mbps with a 1TB cap** on the Premium line for the same $24.99. Pick by traffic shape: unmetered for a steady low-volume service that must never stop, the 1TB cap if you need faster bursts and can live with a ceiling.

On renewals, the 2024 post says orders renew at the same price, and review articles claim LightLayer hasn't done the intro-rate-then-double trick. There is no current official renewal page to check that against. Budget for the possibility that a promotional rate doesn't survive, and you won't be surprised either way.

## Refunds: the policy that should shape how you buy

The refund policy is **provider fault only**. Regular-priced products and promotional products are both non-refundable; only issues attributable to LightLayer get considered, and a directory that last verified the policy on 2026-11-11 records it that way. Payment goes through PayPal, credit cards, and Alipay. No free trial is mentioned anywhere in the material I reviewed.

Read that as a purchasing instruction rather than a complaint. Your risk controls are the test IPs and a monthly billing cycle. Buying an annual plan as a first order inverts both.

👉 [Check the current plans and start with a monthly cycle](https://account.lightlayer.net/?affid=74)

## Who should not buy this

Skip LightLayer if any of these describe you:

- You need a native IP in the country the server sits in. The Taiwan plans are explicitly non-native.
- You need more than 20 Mbps sustained on an Asia Premium plan at entry pricing. The published Taiwan port speeds are 10 and 20 Mbps.
- You want a refund window as a safety net. The policy doesn't offer one.
- You need managed support, an SLA, or redundancy. Budget VPS hosting doesn't include those, and review articles say so directly.
- You need to know the company will still be around in five years. The brand is a MegaLayer subsidiary and relatively new; a directory entry flags long-term stability as unproven and even lists two different founding years in the same profile. Review articles that name "25+ locations" only list eleven cities, so treat the footprint claims loosely.

It suits development environments, staging boxes, personal projects, small sites with Asian visitors, and anything where a few dollars a month buys experimentation room.

## FAQ

**Is the $4/month plan real?**
Yes, it's on LightLayer's pricing page: 1 core, 1GB RAM, 1 IPv4, 100M port, unlimited data, not upgradeable. It isn't the Taiwan Premium plan, it doesn't state a location or route, and it can't be upgraded in place.

**Taiwan or Los Angeles?**
Taiwan if your users are in mainland China or nearby Asia and you want the Premium route in the same country as the server. Los Angeles if you want the $4 entry price, three route options, or a US presence. Taiwan's official material lists only Premium and Global.

**Is CN2 worth the extra money?**
Only if a meaningful share of your traffic reaches mainland China. The review-reported step from $4 Global to $7+ Premium in Los Angeles buys transit quality, not CPU. Test with the Premium IP first; if the latency difference from your users' location is small, save the money.

**Can I get a refund if it doesn't work out?**
Only for faults attributable to LightLayer. Regular and promotional plans are excluded.

**Is annual billing cheaper?**
The reported $24.99/year is about $2.08/month against a $9.00 monthly cart total on the Taiwan page, but the two figures may not cover the same configuration. Verify datacenter, route, port speed, data cap, and IP type in the cart before committing.

## How to decide in one pass

A light Asia node and a non-native IP is acceptable: start with TW-VP02 at 10 Mbps unmetered, monthly billing, and ping 46.8.124.242 first.

Mainland China latency is the whole point: only look at Premium, test every route IP from your users' location, and accept the 10–20 Mbps port as the price of the route.

You need the cheapest box that runs Linux: the $4 Startup plan does that, with the understanding that you can't grow it and the route is whatever the cart assigns.

You need a native IP, more than 20 Mbps, an SLA, or a refund window: buy something else.

Order in a monthly cycle, confirm the route and IP type on the checkout page, and keep the annual plans for a second purchase once you've seen the network behave. 👉 [Check current LightLayer VPS pricing and availability](https://account.lightlayer.net/?affid=74)
