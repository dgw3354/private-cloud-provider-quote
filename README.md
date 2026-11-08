# Private Cloud Service Providers: VPC, Single-Tenant or Managed — Which One Are You Actually Buying? (Real Price Anchors and a Quote Checklist)

Quotes for what sounds like the same product run from about $17 a month to €3,190 a month, and the gap isn't a discount or a markup. It's three different products sharing one keyword: a logically isolated network inside a public cloud, a single-tenant hardware cluster, and an end-to-end managed private cloud contract. Work out which of the three you need and half the vendor list removes itself.

Two verified anchors to keep in view. UpCloud's Dedicated Private Cloud starts at **€3,190 per month**, with hardware-level isolation and zero egress fees. Atlantic.net's cloud VMs started at **$17/month for Linux and $29/month for Windows as of April 2024**, aimed at small businesses that need HIPAA and PCI paperwork more than physical separation. Everything between those two numbers is a difference in what you own, who operates it, and what happens to the bill when traffic grows.

> **Quick read:** if you want dedicated hardware, a private Layer 2 network and control over the OS layer, you're shopping for a bare-metal private cloud, not a managed service. That's the shape of what SpinServers sells, quoted per configuration rather than per published tier. 👉 [See how SpinServers scopes a bare-metal private cloud](https://bit.ly/Spinservers)

## The three products sold under "private cloud service providers"

**Virtual private cloud (VPC).** AWS, Google Cloud and Azure sell this as private cloud. It's a logically isolated network inside a multi-tenant public cloud: your data and traffic are separated, the physical hardware is not. You get elasticity, and you also get noisy-neighbour risk and a bill that moves with usage.

**Single-tenant private cloud.** Compute, storage and networking hardware are reserved for one customer, either in your building or in a provider's. Performance is consistent because nobody else is on the box, and for steady, high-growth workloads the fixed monthly cost often lands below equivalent public cloud spend.

**Managed private cloud services.** Here the provider takes end-to-end responsibility for provisioning, configuration and ongoing operations, under an SLA. Everest Group draws the line explicitly in its Private Cloud Services PEAK Matrix: providers offering infrastructure or colocation only, without ownership or SLA-backed delivery of hosting and managed services, are excluded from the evaluation. To be included, a provider must own all three buckets, directly or through partners.

| Category | Whose hardware | Isolation | How it's priced | Fits |
| --- | --- | --- | --- | --- |
| Virtual private cloud | Shared with other tenants | Logical network separation | Per resource, usage-based | Spiky or short-lived workloads |
| Single-tenant private cloud | Yours exclusively | Physical | Fixed monthly per host or cluster | Steady, performance-sensitive workloads |
| Managed private cloud service | Provider or jointly owned | Physical, plus contractual SLA | Contract, often multi-year | Regulated workloads needing an accountable operator |

The exclusion rule matters more than any ranking. It explains why a company selling you a rack, a cross-connect and a support ticket doesn't appear next to DXC and TCS in the same assessment: those are different businesses with different obligations when something breaks at 3am.

## What "starting at €3,190" actually buys

UpCloud publishes enough detail to see where the number comes from, which most providers don't. The €3,190 entry point corresponds to the smallest of three node types, and the difference between them is the difference between one workload and ten.

| Node type | CPU | Memory | VMs supported |
| --- | --- | --- | --- |
| Standard | AMD EPYC 9355, 32 cores / 64 threads | 640 GB | Up to 200 |
| Premium | AMD EPYC 9575F, 64 cores / 128 threads | 1,280 GB | Up to 300 |
| High-Performance | AMD EPYC 9575F, 64 cores / 128 threads | 1,920 GB | Up to 500 |

Storage is billed on top of the monthly figure, not bundled: €0.22/GB/month for MaxIOPS block storage, €0.085/GB/month for standard block storage, €0.056/GB/month for archive. A 10 TB working set on standard storage adds roughly €870 a month before you've run anything.

That's the first of three line items that turn a headline price into an invoice. The second is the node tier: if your workload needs 1,920 GB of RAM instead of 640 GB, you're not on the entry price. The third is egress. UpCloud charges nothing for outbound transfer, and its own blog argues data transfer fees are the biggest hidden risk in server bills. Providers that do meter egress can add more to a media or API-heavy bill than the compute line itself. Ask for a per-TB outbound figure in writing, then multiply by your actual monthly transfer.

Test the arithmetic against a real deployment: Hack The Box moved onto UpCloud's private cloud and reported that during the proof of concept, service ready times improved significantly while the proposed plan cut costs by around 30%. That's a vendor-published case study, so treat the 30% as their number, not an independent benchmark. The useful part is the structure: they replaced slow infrastructure with fewer, larger dedicated hosts.

## Contracts, proof of concept, and what to negotiate

Billing model changes the real cost as much as the price list does. OpenMetal prices from hourly through to five-year commitments and offers a 30-day free proof of concept. Atlantic.net offers hourly and monthly billing plus discounts on one-, two- and three-year terms, and a free tier of one year with no credit card required. Those are 2024 figures for Atlantic.net; check current pricing before you budget on them.

Four things worth asking for, in this order:

1. **A paid or free POC on your own workload.** Thirty days on your data beats any spec sheet, and it's the only way to see whether a 640 GB node is enough.
2. **The storage and egress rates as separate lines.** A quote that shows one monthly number hides which dimension will grow.
3. **The commitment ladder, with the exit price.** A three-year discount is only a discount if you're still running the workload in year three.
4. **What management is included, in hours or in scope.** "Managed" can mean patching the hypervisor or running your database; the gap in cost between those two is bigger than most hardware choices.

## Compliance and data residency: ask for certificates, not assurances

If HIPAA, PCI-DSS or a sector regulator applies to you, the provider's certification list is a hard filter, not a nice-to-have. The specifics to collect: HIPAA hosting with a Business Associate Agreement available to covered entities, PCI-compliant hosting, SOC 2 and SOC 3 certified data centres, ISO 27001, and ISAE 3400/3402 for the outsourced control environment. Data residency belongs on the same list, because some jurisdictions require sensitive data to be stored and processed locally.

Copaco is a clean example of how to read this. It's a partner-only VMware cloud provider that never sells direct to end customers, runs on six data centres (four in the Netherlands, two in Belgium), holds ISO 27001 and ISAE 3400/3402, and keeps its technical teams in the Netherlands and Belgium. If your requirement says "EU staff, EU facilities, audited controls", that's the level of specificity you're looking for in an answer. For context on why this keeps coming up: 39% of businesses reported a cloud environment data breach in 2022, per Security Magazine.

## The VMware variable nobody puts in the comparison table

If your private cloud is built on VMware and delivered by an MSP, Broadcom's partner programme changes have already reached your contract. Under the current framework, future hardware can only be owned by Pinnacle partners, which directly affects service providers running white-label VCSP setups on hardware they bought themselves.

Existing hardware can keep running, but it has to be suitable for VMware Cloud Foundation 9. Broadcom assesses that per component, compute and storage separately, against the Broadcom Compatibility Guide. VCF 9 also brings new architectural principles, stricter compatibility requirements and a different management model, so the migration is a re-architecture, not a patch.

Three questions for any VMware-based provider you're evaluating:

- Do you hold Pinnacle status, and whose hardware will my environment sit on after the next refresh?
- Can you show the VCF 9 readiness assessment for the specific components in my stack?
- If my current hardware fails the component check, what's the migration path and who pays for it?

Copaco's published answer is that it holds VCSP Pinnacle status, offers dedicated resource domains inside shared hardware or fully isolated dedicated private cloud, and runs a VCF 9 Readiness Assessment before quoting. That's the format a credible answer takes. A provider that answers "we'll handle it" hasn't answered.

## Using analyst tiers as a shortlist, with the caveat attached

Everest Group's Private Cloud Services PEAK Matrix Assessment 2025 evaluated 16 providers across two axes: vision and capability, and market impact.

| Tier | Providers |
| --- | --- |
| Leaders | DXC Technology, HCLTech, Kyndryl, NTT DATA, TCS |
| Major Contenders | Accenture, Atos, Capgemini, Cognizant, Fujitsu, Infosys, Lenovo, Rackspace Technology, UnitedLayer |
| Aspirants | GRASS-MERKUR, Lumen Technologies |

One disclosure you should carry into the meeting: the copy of this document in circulation was licensed to Kyndryl, one of the five Leaders. The evaluation methodology is Everest's, the distribution isn't neutral. Use the tiers to build a shortlist of companies that can genuinely take end-to-end responsibility, then run your own POC.

The same caution applies to "top 10 private cloud providers" articles. One widely syndicated list opens by naming VMware, AWS, Azure, Google Cloud, Oracle and IBM, then leads its actual list with a Nexcess private cloud powered by VMware, states in the same article that VMware itself is not a cloud host, and recommends a sibling brand that absorbs VMware licensing costs. It also files AWS, Azure and Google Cloud VPCs under private cloud providers, which contradicts the definition the analyst community uses. Read those lists for vocabulary, not for ranking.

## Where SpinServers fits, and what to ask before you request a quote

SpinServers sells a bare-metal private cloud: dedicated server clusters with private networking, built around your workload rather than sold as fixed tiers. The public page describes dual 10Gbps links as the baseline, with 40Gbps, 100Gbps and custom network options for larger deployments, optional network management and managed hardware firewalls, and dedicated connectivity into AWS, Google Cloud or Azure for hybrid setups. Its own FAQ draws the line against a VPS: a VPS is a virtual machine on shared physical infrastructure, while this is dedicated servers reserved for one organisation.

Here is the honest state of the pricing information: **SpinServers publishes no tiers and no prices for the private cloud.** The site says pricing depends on server configuration, storage, networking and management requirements, and asks you to contact sales for a custom quote. So there is no package table to reproduce, and any article that shows you one with numbers is guessing. What is published looks like this:

| Item | What the public page states |
| --- | --- |
| Hardware | Dedicated server clusters reserved for one organisation; private networking |
| Network | Dual 10Gbps standard; 40Gbps, 100Gbps and custom on request |
| Management | Optional network management and managed hardware firewalls, scope agreed in the quote |
| Connectivity | Dedicated links to AWS, Google Cloud, Azure |
| Price | Not published; quoted per configuration, storage, networking, management |

Where that sits in the three-category model: it's the single-tenant hardware model with a network layer built around it. Under Everest Group's inclusion rule, a provider that supplies infrastructure plus optional network management, with the split of responsibilities agreed per quote, is on the infrastructure side of the line rather than the managed-service side. If you need someone contractually accountable for patching, monitoring and incident response end to end, ask for that scope explicitly and get it priced as a line item.

The quote request is where the decisions get made, so take these seven questions in with you:

1. Is each server exclusive to us, and is the private network Layer 2 between our own machines?
2. What's included in the base quote: storage, outbound bandwidth, IP transit, firewall management?
3. What term are we committing to, and what does renewal look like after the first period?
4. Can we run a proof of concept before signing, and what does it cost?
5. Which compliance certifications do the facilities hold, and will you sign a BAA if we're a covered entity?
6. Where will the hardware sit, and does that satisfy our data residency requirement?
7. Can the footprint grow later, and what's the lead time on added servers and network capacity?

The published answers to expansion are straightforward: additional servers and network capacity can be planned as requirements grow, with timelines depending on hardware and connectivity availability. That last clause is the one to pin down numerically for your configuration. 👉 [See the published bare-metal private cloud details](https://bit.ly/Spinservers)

## Which one to buy

Four rules, matched to the situation rather than the product name.

**Small team, compliance paperwork needed, predictable bill.** A standard cloud VM tier with HIPAA BAA availability and SOC-certified facilities covers it. Atlantic.net's $17/$29 entry points (April 2024) are the reference; a dedicated cluster is overkill at this scale.

**Steady load, physical isolation, no tolerance for noisy neighbours.** Single-tenant dedicated hardware. Compare the fixed monthly host cost against your current public cloud bill line by line, storage and egress included.

**Regulated, and you want an operator on the hook end to end.** A managed private cloud provider from the Leaders and Major Contenders tiers, with SLA tracking and governance in the contract.

**You already know what hardware you want and need it hosted, networked and reachable from your public cloud.** A bare-metal private cloud quoted to your configuration.

Two things to confirm before anything is signed. First, that the monthly number includes storage, egress and management, or that you've priced each of them separately against your own usage. Second, who owns the hardware at the end of the term and what the exit costs, which matters most in the VMware segment where ownership rules have already changed once.

👉 [Start a SpinServers private cloud quote with your configuration](https://bit.ly/Spinservers)
