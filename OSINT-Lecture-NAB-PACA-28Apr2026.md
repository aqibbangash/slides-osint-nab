# Open-Source Intelligence in Money Laundering & NAO Cases

**A practitioner's guide for investigators, prosecutors, and financial-crime analysts.**

---

> Public lecture delivered at the **Pakistan Anti-Corruption Academy (PACA), NAB Headquarters Islamabad**, on **Tuesday, 28 April 2026**.
> Speaker: **M. Aqib Bangash** — Certified OSINT Master Trainer · CEO, Intelligence X One · CTO, Tech Net Group.

This document is the **public-read companion** to the slide deck and the speaker manual. Where slides are forced to be terse, this version expands every concept with the context, references, and small worked examples that didn't fit elsewhere. It is intended for anyone — investigators, prosecutors, journalists, academics, civil-society researchers — who wants to understand how Open-Source Intelligence is used in modern financial-crime work, with a Pakistan focus.

**Companion files**
- `OSINT-Lecture-NAB-PACA-28Apr2026.pptx` — the 67-slide deck
- `OSINT-Lecture-NAB-PACA-28Apr2026.pdf` — PDF export of the deck
- `OSINT-Lecture-NAB-PACA-28Apr2026-Speaker-Notes.pdf` — full hands-on speaker manual with every command and demo runbook
- `OSINT-Lecture-NAB-PACA-28Apr2026.html` — interactive HTML presentation

---

## Table of Contents

1. [Foreword and how to read this](#foreword)
2. [Module 1 — Introduction to OSINT](#module-1)
   - [1.1 What OSINT actually is](#osint-definition)
   - [1.2 A working definition and a short history](#working-definition)
   - [1.3 OSINT among the intelligence disciplines](#ints)
   - [1.4 Surface, deep, and dark — open ≠ accessible](#layers)
   - [1.5 The OSINT cycle](#cycle)
   - [1.6 Source reliability — the Admiralty Code](#admiralty)
   - [1.7 Legal and ethical boundaries in Pakistan](#legal)
   - [1.8 OPSEC for investigators](#opsec)
3. [Module 2 — OSINT in ML / NAO Cases](#module-2)
   - [2.1 Why OSINT is the financial-crime force-multiplier](#why-osint)
   - [2.2 Where OSINT plugs into the ML investigation lifecycle](#lifecycle)
   - [2.3 FATF typologies and their OSINT signatures](#fatf)
   - [2.4 Beneficial ownership and shell companies](#bo)
   - [2.5 Lifestyle analysis and unexplained wealth](#lifestyle)
   - [2.6 International money trails](#international)
   - [2.7 Crypto-enabled money laundering](#crypto)
   - [2.8 Making OSINT court-ready](#court-ready)
   - [2.9 An anonymized case vignette](#vignette)
   - [2.10 Limits and pitfalls of OSINT](#limits)
4. [Module 3 — OSINT Frameworks and Methodology](#module-3)
   - [3.1 Why frameworks beat tools](#why-frame)
   - [3.2 The OSINT Framework and Bellingcat Toolkit](#framework)
   - [3.3 The intelligence cycle, applied to a case](#applied)
   - [3.4 The Maltego methodology — entities, transforms, pivots](#maltego-method)
5. [Module 4 — Kali Linux Toolkit](#module-4)
   - [4.1 What is Kali Linux](#kali)
   - [4.2 theHarvester](#harvester)
   - [4.3 Recon-ng](#recon-ng)
   - [4.4 Sherlock and WhatsMyName](#sherlock)
   - [4.5 SpiderFoot](#spiderfoot)
   - [4.6 Maltego Community Edition](#maltego)
   - [4.7 ExifTool](#exiftool)
   - [4.8 Domain reconnaissance — Amass, subfinder, crt.sh](#amass)
   - [4.9 The full Kali OSINT toolkit reference](#toolkit-ref)
6. [Module 5 — OSINT Sources and Platforms](#module-5)
   - [5.1 Google dorking](#dorking)
   - [5.2 Social media intelligence (SOCMINT)](#socmint)
   - [5.3 Image intelligence](#image)
   - [5.4 Domains, WHOIS, DNS, certificate transparency](#domains)
   - [5.5 Corporate records and beneficial ownership](#corporate)
   - [5.6 Breach and leak data](#breaches)
   - [5.7 Dark web monitoring](#darkweb)
   - [5.8 Geospatial / GEOINT workflow](#geospatial)
   - [5.9 Crypto OSINT in detail](#crypto-detail)
   - [5.10 Enterprise OSINT platforms](#enterprise)
7. [Module 6 — CDR and IPDR Analysis](#module-6)
   - [6.1 What is a CDR](#cdr-what)
   - [6.2 Anatomy of a CDR record](#cdr-anatomy)
   - [6.3 CDR analysis workflow](#cdr-workflow)
   - [6.4 What IPDR adds](#ipdr)
   - [6.5 A worked example](#cdr-worked)
   - [6.6 Common pitfalls](#cdr-pitfalls)
8. [Module 7 — Tradecraft and Closing](#module-7)
   - [7.1 Sockpuppets and investigative personas](#sockpuppets)
   - [7.2 Attribution chains](#attribution)
   - [7.3 Metadata exploitation patterns](#metadata)
   - [7.4 Operational discipline checklist](#discipline)
   - [7.5 A 90-day learning path](#path)
   - [7.6 Resources and further reading](#resources)
9. [Annex A — Glossary](#glossary)
10. [Annex B — Pakistan legal references](#legal-refs)
11. [Annex C — Useful URLs](#urls)

---

<a id="foreword"></a>

## Foreword and how to read this

Open-Source Intelligence — OSINT — is the discipline of producing intelligence from publicly available information. It is not new. Intelligence services have been clipping foreign newspapers for over a century: the **Foreign Broadcast Information Service** (FBIS) was established in the United States in 1941, and similar bodies were standing in Britain, India, the USSR, and elsewhere by the late 1940s. What is new is *scale*. The internet has made everyone a publisher; commercial satellites image the planet weekly; corporate registries are increasingly online; entire datasets leak and are indexed within hours. The signal and the noise have both exploded.

This shift is consequential for **financial-crime work**. The United Nations Office on Drugs and Crime estimates that 2 to 5 percent of global GDP is laundered annually — somewhere between USD 800 billion and 2 trillion. Less than 1 percent of laundered funds are recovered globally (Europol, 2023). The Financial Action Task Force's mutual evaluations consistently flag **beneficial ownership opacity** as one of the hardest gaps to close — and that is exactly the gap where modern OSINT pays off. Layered shell companies, nominee directors, family trusts, real-estate holding vehicles, and crypto on-chain transfers all leave public traces. The investigator's job is to follow them.

This document mirrors the structure of the lecture. Each module begins with a concept, walks through the legal and ethical framing, then introduces the tools and platforms an investigator can practically use. Pakistan-specific references — NAO 1999, AMLA 2010, PECA 2016, Qanun-e-Shahadat 1984, SECP, FBR-NTN, ECP asset declarations — are woven through, because the audience and use-cases are Pakistani. But the techniques are universal.

A note on **scope**. We deliberately do *not* cover offensive cyber operations, lawful intercept, or covert surveillance. OSINT is defined here strictly as the use of *publicly accessible* information. Any technique that requires bypassing a technical or legal control is, by definition, outside this discipline. That boundary is not just legal — it is the foundation of admissibility under Pakistani evidence law.

A second note on **honesty about limits**. OSINT is a force-multiplier, not a panacea. It produces leads quickly and cheaply; it does *not* produce conclusions on its own. Every finding in this document — every technique, every tool — should be paired with a corroboration step. In court, a single OSINT artefact is usually graded under the Admiralty Code (introduced in §1.6) and supported by at least one independent second source before it carries weight. Treat OSINT as the cheapest pre-targeting intelligence layer available to your team. Use it to decide where to expend the slow, expensive, formal investigative steps that follow.

---

<a id="module-1"></a>

# Module 1 — Introduction to OSINT

<a id="osint-definition"></a>

## 1.1 What OSINT actually is

OSINT is the *craft* of answering an investigative question using information that anyone can legally access — the open web, social media, public records, news, leaked databases lawfully republished — and converting that raw information into evidence a decision-maker can act on.

Three statements about what OSINT is **not** are clarifying:

- **It is not hacking.** No unauthorised access to systems, data, or accounts is permissible. The moment you bypass a login, a paywall, a CAPTCHA, or a technical access control to obtain something, you have crossed the line out of OSINT into computer-misuse territory. In Pakistan that line is encoded in **PECA 2016 §3** (unauthorised access to information system). It can also vitiate the admissibility of every piece of evidence that flows downstream of the bad collection.
- **It is not guessing.** OSINT is built on *sourced, dated, reproducible* claims. "I read it somewhere" is not OSINT. "On 14 March 2026 at 09:43 PKT, the SECP eServices portal returned the following directorship record for *Acme Trading (Pvt) Ltd*, with SHA-256 hash `…`, retrieved by the analyst from a non-attributable network" is OSINT.
- **It is not free intelligence.** It is *cheap* relative to formal investigative steps, but it costs disciplined time. The discipline — collection method, hashing, chain-of-custody, second-sourcing — is what makes it useful in court. Without that discipline, OSINT is just internet research, and a defence motion will exclude it.

The investigator's edge in OSINT is **method**, not access. Public information becomes intelligence only when it is collected, structured, and reasoned about systematically. Two analysts looking at the same target should be able to produce the same finding from the same artefacts; that is the test of disciplined OSINT.

<a id="working-definition"></a>

## 1.2 A working definition and a short history

The formal working definition adopted by NATO and most Anglosphere intelligence services comes from the United States [National Defense Authorization Act of 2006](https://en.wikipedia.org/wiki/National_Defense_Authorization_Act_for_Fiscal_Year_2006):

> "Information that is publicly available, collected, exploited, and disseminated in a timely manner to an appropriate audience for the purpose of addressing a specific intelligence requirement."

Each of those four words matters. *Publicly available* draws the legal line. *Collected* implies discipline — not happenstance. *Exploited* is the analytical step. And *specific intelligence requirement* — usually written as a Priority Intelligence Requirement, or PIR — is what separates OSINT from generic Googling. A vague question produces unfocused collection; a precise question produces actionable intelligence.

OSINT is **not new**. The U.S. **FBIS** was founded in 1941 to monitor foreign radio broadcasts. The British **BBC Monitoring Service** ran in parallel. India's **DPSA** and Pakistan's later monitoring units performed the same role. Throughout the Cold War, OSINT — newspapers, journals, public statements, photo-essays — was estimated to constitute the majority of inputs to finished intelligence products on closed societies.

What has changed since the late 1990s is the *scale and speed* of public information. Commercial satellite imagery now offers sub-metre resolution to anyone with a credit card; certificate transparency logs reveal every TLS certificate ever issued; public corporate registries cover most major jurisdictions; financial-crime leaks (Panama Papers, 2016; Pandora Papers, 2021; FinCEN Files, 2020; Suisse Secrets, 2022) have pushed once-secret data into the open record. Public estimates today put OSINT at **70 to 90 percent** of inputs to many finished intelligence products. The work is increasingly less about *finding* information and more about *filtering* it and *grading* it.

<a id="ints"></a>

## 1.3 OSINT among the intelligence disciplines

The intelligence community organises collection by source type, often called the **"INTs"**:

| INT     | Source                 | Examples                                                  |
|---------|------------------------|-----------------------------------------------------------|
| HUMINT  | Human sources          | Informants, interviews, undercover operations             |
| SIGINT  | Signals                | Communications and electronic intercepts                  |
| IMINT   | Imagery                | Satellite, aerial, drone imagery                          |
| GEOINT  | Geospatial             | Location-based reasoning, mapping                          |
| MASINT  | Measurement            | Radar, acoustic, nuclear, chemical signatures             |
| **OSINT** | **Open source**       | **Public data — the subject of this lecture**             |

The discipline boundaries blur in practice — a satellite photo on a public news site is both IMINT and OSINT — but the distinction matters legally and procedurally. SIGINT and HUMINT in Pakistan require formal authorisation (lawful intercept warrants, source-handling protocols). OSINT does not. That is why, in a NAB investigation, you will usually **lead with OSINT**: it is lawful, quick, and reveals leads that the other disciplines then confirm formally.

A common mistake is to treat OSINT as inferior because it is public. The opposite is closer to true: a PIR answered using only OSINT, with documented sources, is often the *strongest* form of finding, because it can be reproduced by another analyst, by a defence team, by the court, by a journalist, by anyone. Reproducibility is the gold standard of evidence.

<a id="layers"></a>

## 1.4 Surface, deep, and dark — open ≠ accessible

A common confusion: "open source" is mistaken for "Google-indexed". In reality, the public web has three rough layers:

- **Surface web** — what search engines index. About 4 percent of the real web. News sites, blogs, most public social posts. The visible tip.
- **Deep web** — public but not indexed by general search engines. About 90 percent of the real web. Academic databases, court filings, corporate registries, gated records, paywalled archives. Most of the **useful OSINT for a corruption case lives here**, not on the surface.
- **Dark web** — accessible only via Tor or I2P. About 6 percent. Illicit markets, leak forums, ransomware victim portals, sanctioned-actor chatter, hawala broker channels.

The investigator's instinct should *not* be "Google first". It should be "what is the right registry / archive / dataset for this question?" Often the surface web does not have it. SECP filings are deep-web data — public but require navigating SECP eServices, not search. A target's school's parent-WhatsApp group may be deep — public to anyone with the school's domain. A leaked document on a paste site may be surface — but requires the right query. Understanding which layer your answer lives on is half the battle.

<a id="cycle"></a>

## 1.5 The OSINT cycle

Disciplined OSINT follows a five-stage cycle, derived from the standard intelligence cycle and adapted for open-source work:

1. **PLAN** — write the Priority Intelligence Requirement (PIR). Define *who* (subject), *what* (the precise question), *what decision* the answer enables, *what indicators* would confirm or refute, *what is out of scope* (legal, ethical, time), and *when* the answer is needed.
2. **COLLECT** — gather from sources mapped to the PIR. Always preserve originals — full-page captures, hashes, timestamps. Never paraphrase a document in your case file.
3. **PROCESS** — de-duplicate, translate, extract, structure into entities and events. This is where raw screenshots become structured rows in a database that can be queried later.
4. **ANALYZE** — pivot, corroborate, interpret. Apply the Admiralty Code (§1.6). Write conclusions explicitly tied to evidence — never beyond it.
5. **DISSEMINATE** — deliver to the decision-maker in usable form: a brief, a memo, an exhibit. Close the feedback loop: the decision-maker's question almost always raises new ones, which feed the next plan.

The cycle is **iterative**, not linear. Each analysis produces new questions. New questions produce new collection. The discipline is not in following the cycle once — it is in following it *every time*, even when shortcuts are tempting.

The PIR template is worth committing to memory:

```
Subject:    Who or what is the target?
Question:   The single sentence we are trying to answer.
Decision:   What action will the answer trigger?
Indicators: What facts would confirm or refute?
Boundary:   What is out of scope?
Deadline:   When is the answer needed?
```

Filling those six fields up-front prevents the most common failure mode in OSINT work — drifting from the question, accumulating tangentially-relevant findings, missing the deadline. A good PIR fits on a single index card.

<a id="admiralty"></a>

## 1.6 Source reliability — the Admiralty Code

Not all sources are equal, and not all information is equally credible. NATO and most Western intelligence services grade evidence on a **6×6 grid** known as the **Admiralty Code** (after its origin in the British Admiralty's intelligence work in the early 20th century):

**Source reliability** (letters):

- **A** — completely reliable
- **B** — usually reliable
- **C** — fairly reliable
- **D** — not usually reliable
- **E** — unreliable
- **F** — reliability cannot be judged

**Information credibility** (numbers):

- **1** — confirmed by other sources
- **2** — probably true
- **3** — possibly true
- **4** — doubtful
- **5** — improbable
- **6** — truth cannot be judged

Every artefact gets a two-character grade. A tweet from a verified journalist citing a court document → **B-2** (usually reliable source, probably true). An anonymous forum claim with no corroboration → **F-6** (reliability and truth both unknown). A SECP filing with the registry's official metadata → **A-1** (completely reliable, confirmed). 

**Investigator rule of thumb:** a single B-2 finding is suggestive. A court-defensible identity claim usually requires at least two independent **A-2 or B-2** findings. F-6 findings are leads only; never conclusions.

This grading is not bureaucratic ceremony — it is the discipline that lets a defence attorney's expert reproduce your reasoning. If your case file shows the grade for every artefact, you have a defensible reasoning chain. If it does not, you have a feeling.

<a id="legal"></a>

## 1.7 Legal and ethical boundaries in Pakistan

OSINT operates within a layered legal framework. The five most directly relevant laws for NAB / FMU / FIA investigators:

**[National Accountability Ordinance 1999 (NAO)](https://www.nab.gov.pk).** Empowers NAB to investigate wilful default and corruption. **Section 9** lists predicate offences including assets disproportionate to known means. **Section 27** authorises information collection from any source — squarely covers OSINT. The "any source" language is broad and has been interpreted to include open-source materials, foreign public records, leaked databases lawfully published by third parties, and online platforms.

**Anti-Money Laundering Act 2010 (AMLA).** Anti-money-laundering framework. **Section 7** grants the Financial Monitoring Unit (FMU) access to public and reporting-entity data. **Section 8** covers suspicious-transaction reporting. The Act has been amended several times to align with FATF recommendations.

**Prevention of Electronic Crimes Act 2016 (PECA).** Defines what is *not* permitted: **Section 3** — unauthorised access to information systems; **Section 13** — use of stolen identity; **Sections 29 and 32** — data privacy and cyber-stalking. OSINT must stay strictly on the **public-and-lawfully-accessed** side of these provisions. PECA is the line investigators cross at their peril.

**Investigation Act 2022.** Standard operating framework for federal investigations: chain-of-custody, digital evidence handling, search-and-seizure procedures.

**[Qanun-e-Shahadat Order 1984](https://pakistanlawsite.com).** Pakistan's evidence law. **Article 73** governs documentary evidence. **Article 164** specifically permits electronic evidence produced by modern devices, subject to integrity safeguards — primarily hashing and chain-of-custody documentation. This is the article every OSINT artefact in a NAO court submission rests on.

Beyond statute, two international frameworks shape the field:

- **FATF Recommendations 24, 25, and 40** — beneficial ownership transparency and international cooperation.
- **Egmont Group operational standards** for FIU information exchange.

The **golden rule**: if you would have to bypass a technical or legal control to obtain something, it is not OSINT. The corollary: when in doubt, ask the prosecutor before the artefact goes into the brief. A well-grounded OSINT finding strengthens a case. A questionably-sourced one can taint everything around it.

<a id="opsec"></a>

## 1.8 OPSEC for investigators

Operational Security (OPSEC) is the discipline of conducting OSINT without tipping the target or contaminating the case. The threats fall into six categories:

1. **Attribution** — the target sees your IP, browser fingerprint, or logged-in account. Modern social platforms log every profile view; your "anonymous" research session may be silently signalling investigative interest.
2. **Contamination** — browser cookies merge case evidence with your personal accounts. The exhibit you screenshot now contains your authenticated session — making it inadmissible and personally embarrassing.
3. **Malware** — target sites and leaked dumps are often booby-trapped. A single click from your government workstation onto a hostile PDF can compromise the entire department.
4. **Pivoting giveaway** — using the same persona / IP / cookies across platforms links the accounts. Sophisticated targets watch for this; skilled defence attorneys subpoena it later.
5. **Legal exposure** — impersonation or entrapment can taint admissibility. Even unintentional impersonation (creating a sockpuppet that resembles a real person) raises issues under PECA §13.
6. **Leaks** — bookmarks, screenshots, and notes leave traces on shared corporate hosts. A bookmark to "Money Trail Re: Subject X" on your office laptop is itself a discoverable artefact.

The mitigations are simple to state and require continuous discipline:

- **Isolated VM** — research happens in a virtual machine snapshotted before the session and reverted afterwards. Kali Linux is the typical workstation.
- **Dedicated research browser** — Firefox or Chromium profile separated from your daily browser. WebRTC disabled, autofill disabled, password manager disabled.
- **Non-attributable network** — VPN with a kill-switch, or Tor for sensitive lookups. *Never* research from the office IP.
- **Sockpuppet hygiene** — investigative personas built slowly over weeks, not hours; one persona per case; never linked to office IPs or government devices.
- **Per-case evidence storage** — separate folder, separate hash log, separate access controls for every case.

Two phrases worth memorising: *the discipline IS the case* (a perfect finding from a contaminated environment is worthless), and *observation only* (we look, we copy, we hash; we never solicit, propose, or transact, lest we step into entrapment territory).

---

<a id="module-2"></a>

# Module 2 — OSINT in ML / NAO Cases

<a id="why-osint"></a>

## 2.1 Why OSINT is the financial-crime force-multiplier

In a corruption or money-laundering investigation, OSINT delivers six specific advantages — each of which addresses a weakness of the formal-only investigative path:

- **Speed.** Leads in hours, not months. A preliminary subject assessment that informs which bank-record requests to file can be produced in a single afternoon. Compare with the months an MLAT request takes to return data from a foreign bank.
- **Cost.** No court order is required to read what is public. Your unit's budget stretches further when 80 percent of the pre-targeting work uses free tools and free data.
- **Coverage.** OSINT reaches jurisdictions where formal cooperation is slow or politically fraught. A subject's UAE property registry record is public; the equivalent bank record requires multilateral cooperation that may never come.
- **Deconfliction.** OSINT cross-checks assertions from suspects, witnesses, and corporate filings. Inconsistencies between what a subject declares and what is publicly visible are, by themselves, leads.
- **Targeting.** OSINT prioritises *which* assets, accounts, and entities to formally request records on. A scattershot bank-records request rarely produces; a precisely targeted one usually does.
- **Pattern discovery.** OSINT exposes networks of nominees, relatives, and shell entities that no single bank record would ever reveal.

The macro-economics are sobering. UNODC's working estimate is that **2 to 5 percent of global GDP** — roughly USD 800 billion to 2 trillion — is laundered annually. **Less than 1 percent** of that is recovered, according to Europol's 2023 estimate. The marginal value of better intelligence — even a 1 percent improvement in detection or recovery — is denominated in tens of billions of dollars globally and hundreds of millions in any major emerging-market economy.

For Pakistan specifically, FATF mutual evaluations have rated the country strong on detection of predicate offences but weaker on **beneficial-ownership transparency** — exactly the area where modern OSINT (corporate-registry crosswalks, leaked-data indices, real-estate cross-jurisdictional traces) most clearly helps.

<a id="lifecycle"></a>

## 2.2 Where OSINT plugs into the ML investigation lifecycle

A typical NAB / AMLA investigation has six phases. Each has its own OSINT use-case:

| Phase            | Trigger                                            | OSINT role                                                      |
|------------------|----------------------------------------------------|------------------------------------------------------------------|
| **DETECTION**    | Typology match, tip-off, STR review                | Profile the subject and their public footprint fast              |
| **INQUIRY**      | Preliminary fact-finding under NAB rules           | Map entities, associates, addresses, assets                      |
| **INVESTIGATION**| Formal case; banking, corporate, MLAT requests     | Target requests; corroborate; identify nominees                  |
| **ASSET TRACING**| Where did the money go?                            | Companies, real estate, vessels, crypto, travel                  |
| **PROSECUTION**  | Reference before NAB court                         | Timeline exhibits, verified public records                       |
| **ASSET RECOVERY**| Enforcement and repatriation                      | Post-judgment monitoring of respondents                          |

OSINT is not a single phase — it threads through all six. The skill is recognising *which OSINT question is most useful at which phase*. In **Detection**, the question is broad: who is this person, what are they publicly associated with? In **Asset Tracing**, the question is narrow: does this UAE property registry entry connect to our subject's nominee?

A common mistake is to treat OSINT as a one-shot pre-investigation tool. The opposite is true: OSINT is a *recurring* tool that gets re-run as the case develops. A subject identified in Phase 1 may have their UAE property listed in Phase 4 only because Phase 3 surfaced the spouse's name — which then enables a Phase 4 search nobody could have done in Phase 1.

<a id="fatf"></a>

## 2.3 FATF typologies and their OSINT signatures

The Financial Action Task Force publishes detailed typology reports that catalogue how money is laundered in practice. Each typology has its own **OSINT signature** — the public traces it tends to leave. Knowing the signature tells you which sources to query.

**Trade-based money laundering (TBML).** Over- or under-invoicing, multiple-invoicing, phantom shipments. OSINT signature: shipping registers, bills of lading, Automatic Identification System (AIS) vessel tracking via [MarineTraffic](https://marinetraffic.com) and [VesselFinder](https://vesselfinder.com), customs price benchmarks, transit-country company registries showing the same parties on multiple legs.

**Shell and front companies.** OSINT signature: beneficial-ownership registries, [OpenCorporates](https://opencorporates.com) (240 million companies, 140 jurisdictions), [OCCRP Aleph](https://aleph.occrp.org), [ICIJ Offshore Leaks Database](https://offshoreleaks.icij.org), [Sayari Search](https://sayari.com), sanctions lists. Common red flags: same registered address across "unrelated" companies; shared directors; nominee-service firms; incorporation bursts around suspicious dates; identical share structures; director resignations just before transactions.

**Cash-intensive businesses.** OSINT signature: business social-media presence (or telling absence), Google reviews density, public regulatory filings cross-checked against visible lifestyle indicators. A "thriving" cash business with zero customer reviews and no social presence is a tell.

**Real estate and high-value goods.** OSINT signature: land records (UK Land Registry, Dubai DLD, provincial Pakistani BoR portals), property listings, drone-shot satellite imagery (Google Earth Pro's historical slider is invaluable), yacht and aircraft registries, luxury marketplaces, builder testimonials.

**Professional launderers.** OSINT signature: press coverage in foreign jurisdictions, enforcement actions in those jurisdictions, PEP and adverse-media databases.

**Crypto laundering.** OSINT signature: blockchain explorers (purely public on-chain data), exchange sanctions lists (OFAC SDN), address clustering via [Breadcrumbs.app](https://breadcrumbs.app) or [Arkham Intelligence](https://arkhamintelligence.com), darknet market references on monitored forums. Detailed in §5.9 below.

For each typology, the workflow is the same: form a hypothesis (e.g. "subject is using TBML through a textile-export shell"), identify the OSINT signature, query the relevant sources, grade findings under the Admiralty Code, second-source any A2 / B2 finding, brief the case officer.

<a id="bo"></a>

## 2.4 Beneficial ownership and shell companies

Between a bank account and the actual person who controls it, a launderer typically inserts layers — legal entities, nominee directors, family trusts, holding companies in opaque jurisdictions. The job of beneficial-ownership OSINT is to **collapse those layers**.

**Common red-flag signals.**

- **Same registered address across companies.** Twenty companies registered at the same Karachi office address that turns out to be a small accountancy is a strong indicator of nominee provision.
- **Shared directors or nominee service firms.** OpenCorporates' director-search makes this trivial to surface.
- **Incorporation bursts.** Five companies incorporated within the same week, months before a major contract award, is a tell.
- **Director resignations just before transactions.** A director who resigns the day before a suspicious payment is a beneficiary trying to break the public record.
- **Identical share structures.** Two ostensibly unrelated companies with the same 70/15/10/5 share split between four parties are not unrelated.

**Key sources.**

- **[SECP eServices](https://eservices.secp.gov.pk)** — Pakistan corporate filings, directors, charges.
- **[OpenCorporates](https://opencorporates.com)** — global cross-jurisdictional company search, free tier with rate limits.
- **[OCCRP Aleph](https://aleph.occrp.org)** — investigative archive of corporate filings, leaks, sanctions, PEP data.
- **[ICIJ Offshore Leaks Database](https://offshoreleaks.icij.org)** — Panama Papers, Pandora Papers, Paradise Papers, Bahamas Leaks, FinCEN Files.
- **[Sayari Search](https://sayari.com)** — beneficial-ownership focus, free tier limited.
- **[Companies House (UK)](https://find-and-update.company-information.service.gov.uk)** — UK companies, free, full historical filings.
- **EU Business Register** — multi-state company search.
- **UAE Free Zones registries** — DMCC, DIFC, ADGM (variable transparency).

A typical investigative pivot looks like this:

1. SECP director search returns Subject as director of Acme Trading (Pvt) Ltd.
2. OpenCorporates pivot on Subject's name returns directorships in three foreign jurisdictions.
3. ICIJ Offshore Leaks search on Subject's name returns one hit in Panama Papers.
4. Cross-checking the foreign company's address with OpenCorporates returns 8 other companies sharing the address — likely a nominee provider.
5. Each of the 8 companies is then itself searched in ICIJ, OCCRP, and the local registry.

This kind of graph expansion is exactly what tools like Maltego (§4.6) automate.

<a id="lifestyle"></a>

## 2.5 Lifestyle analysis and unexplained wealth

NAO §9 frames "assets disproportionate to known sources of income" as a predicate offence. OSINT is exceptionally well suited to building the **lifestyle side** of that equation cheaply, with corroboration that holds up in court.

**Key signal categories.**

- **Social media.** Posts, check-ins, family accounts. Children and spouses are often less OPSEC-aware than the principal subject. A senior officer's daughter's Instagram is frequently the most candid record of family wealth.
- **Travel patterns.** Open booking-site profiles, geo-tagged photos, family travel pages. Frequent travel to specific destinations (Dubai, London, Toronto) over years is itself an indicator.
- **Property and vehicles.** Property-portal listings, registry data, dealer brochures, social-media reveals of homes and cars. A 2024 Range Rover visible in a holiday photo is hard to argue away.
- **Education and lifestyle.** Children at expensive foreign universities, club memberships, expensive hobbies (yachting, equestrian, polo).

The investigative trick is **layered comparison**. Take the subject's ECP asset declaration. Lay it next to the lifestyle indicators visible in OSINT. Where the two diverge — declared income of X, visible lifestyle implying spending of 10X — you have your starting point.

A practical worked example, anonymized: a mid-level public official declares modest assets to ECP. OSINT pulls the spouse's Instagram (public), shows three foreign holidays in the calendar year, plus children at a UK university whose annual fees alone exceed declared family income. ECP cross-check shows no foreign-property declaration. UK Land Registry search on the spouse's name returns a flat in central London. That single chain — declaration vs. lifestyle vs. registry — is the spine of an UWO-style investigation.

<a id="international"></a>

## 2.6 International money trails

Cross-border laundering leaves traces in **public** registries and **public** tracking systems whose sheer breadth is hard for any single launderer to scrub.

**Cross-border companies.** Beneficial owners in offshore havens — BVI, Cayman, UAE Free Zones, Mauritius, Seychelles. Some of these are increasingly transparent (UK PSC register from 2016; UAE introducing beneficial-ownership requirements from 2021); others remain opaque. The leak databases (Panama, Pandora, Paradise) often fill the gap that statutory registries leave.

**Trade flows.** Bills of lading from C2C shipping platforms; vessel-tracking via [MarineTraffic](https://marinetraffic.com) and [VesselFinder](https://vesselfinder.com), which record AIS data going back years; flight tracking via [FlightRadar24](https://flightradar24.com) and [ADS-B Exchange](https://www.adsbexchange.com). Specific commodity-price benchmarks (London Metal Exchange, ICIS, Platts) are the reference for spotting under- and over-invoicing in TBML.

**Foreign real estate.** UK Land Registry (search by address; downloads include corporate ownership). Dubai Land Department. Provincial Canadian land registries. Spanish Catastro. France's BAN (Base Adresse Nationale) plus cadastral data. These are the registries used in nearly every European laundering case in the last decade.

**Family migration and presence.** Children at foreign universities (alumni pages, society directories, public student-society membership), spouses with foreign nationality (court records of immigration cases sometimes available; LinkedIn employment history), elderly parents in care homes abroad.

**Hawala and remittance.** Patterns of remittance corridors visible in social-media posts, public Telegram channels, and sometimes leaked broker chat archives. Hawala is by design hard to trace — but social-media posts by the brokers' family members frequently fill in the corporate side.

**Exchange of information mechanisms.** Once OSINT identifies the foreign entity, formal cooperation through FATF FIU exchange, the Egmont Group of FIUs, and MLAT requests is how the financial detail is then extracted.

<a id="crypto"></a>

## 2.7 Crypto-enabled money laundering

Cryptocurrency is increasingly relevant to NAO and AMLA investigations — not because of trading (Pakistan's State Bank prohibits trading), but because crypto rails are used for cross-border movement, sanctions evasion, and laundering on top of predicate offences.

The investigative virtue of crypto is also its laundering vulnerability: **every Bitcoin and Ethereum transaction is public, forever**. Following the chain is purely OSINT — no warrants, no MLAT requests.

**What is visible to anyone.**

- Every BTC, ETH, TRX, BSC, SOL transaction — sender, recipient, amount, timestamp.
- Address clustering — the same actor often controls multiple wallets, and those wallets can be linked through co-spending patterns or behavioral fingerprints.
- Exchange-attributed addresses — known Binance, Coinbase, Bybit, OKX deposit and withdrawal addresses are publicly catalogued.
- Sanctioned addresses — OFAC SDN list, FATF VASP advisories, mixer-protocol addresses.

**Tools investigators use.**

- **[blockchain.com](https://blockchain.com)** — Bitcoin explorer.
- **[etherscan.io](https://etherscan.io)** — Ethereum explorer.
- **[tronscan.org](https://tronscan.org)** — Tron explorer (high USDT volume).
- **[Breadcrumbs.app](https://breadcrumbs.app)** — free graph and clustering visualisation.
- **[Arkham Intelligence](https://arkhamintelligence.com)** — entity-tagged dashboards (free tier).
- **[Chainabuse](https://chainabuse.com)** — community scam-wallet reports.
- The **[OFAC SDN list](https://ofac.treasury.gov/sanctions-list-service)** — downloadable as CSV; grep for crypto address types (BTC / ETH / USDT / TRX).

**Common laundering patterns to watch.**

- **Mixers.** Tornado Cash (sanctioned by OFAC in 2022), Wasabi, Samourai. Inflow patterns are visible on chain analytics platforms.
- **Cross-chain bridges.** Money moves ETH → TRX → BSC → back to ETH to break clustering. Each bridge has known canonical contract addresses.
- **Exchange off-ramps.** Deposits to known centralized-exchange addresses indicate fiat off-ramp coming. Subpoenable via MLAT once identified.

**Pakistan-specific framing.** Trading is restricted but **OSINT analysis of public ledgers is observation, not transaction**. Treat every artefact under the same Article 164 chain-of-custody discipline as any other digital evidence — hash the transaction record, log the source explorer's URL, and timestamp.

<a id="court-ready"></a>

## 2.8 Making OSINT court-ready

OSINT artefacts have to survive the same admissibility tests as any other digital evidence. There are four practical steps that, taken together, make almost any OSINT finding defensible.

**1. Capture properly.** Use [Hunchly](https://hunch.ly) or an equivalent forensic-browser tool — not naked screenshots. Hunchly captures the full HTML, all assets, the URL, the timestamp, and the user's session metadata. A naked screenshot lacks half of that and is easy for a defence expert to question.

**2. Hash everything.** SHA-256 every artefact at the moment of collection. Log the hash in your case file *before* any further processing. The defensibility argument is "the hash on the artefact today matches the hash recorded at capture; therefore the artefact has not been altered". That argument works only if the hash exists from the start.

**3. Maintain the artefact log.** A structured log with one row per finding:

| Timestamp | Source URL | Artefact file | SHA-256 | Admiralty grade | Pivot it produced |
|-----------|------------|---------------|---------|-----------------|-------------------|

Keep the log in a per-case folder. Same row format every time. This is the document a defence expert will scrutinise; uniformity is an asset.

**4. Reference Article 164.** Qanun-e-Shahadat 1984 Article 164 makes electronic evidence admissible *provided integrity is demonstrable*. The hashing + chain-of-custody pattern above is what makes integrity demonstrable. When briefing the prosecutor, lead with Article 164.

**The defensibility test.** Can a competent third party reproduce your finding from your log? If yes, it will hold up in NAB court. If you would have to add explanation or interpretation to the log to reproduce the finding, the log is incomplete.

<a id="vignette"></a>

## 2.9 An anonymized case vignette

A worked example, sanitised — never a live or identifying case.

**Subject and signal.** Mid-level public official. Suspicious Transaction Report flagged by a domestic bank for unexplained inflows. Lifestyle visible online appears disproportionate to declared income.

**OSINT path.**

1. SECP director search on the official's name returned a directorship in a small private company. (B-1, registry data.)
2. OpenCorporates pivot on the same name returned a directorship in a UK-incorporated company, registered three years prior. (A-1, Companies House.)
3. ICIJ Offshore Leaks search on the official's name returned a hit in Pandora Papers — a BVI entity with the official as ultimate beneficial owner. (A-2.)
4. Image search on the official's social-media profile photo, combined with reverse-image search of a corporate signing-ceremony photo published on a partner company's website, surfaced the same photograph at an unrelated event — confirming the visible attendee was indeed the subject. (B-2.)

**Asset trace.**

5. UK Land Registry search on the spouse's name (publicly visible from social media) returned a Knightsbridge flat purchased through the BVI entity. (A-1.)
6. Google Earth Pro historical imagery slider showed the flat's exterior matching social-media photos posted by the spouse two years earlier. (B-2.)
7. ECP asset-declaration cross-check confirmed no declaration of the flat. (A-1, registry data.)

**Outcome.** The OSINT chain pre-targeted bank-record requests and an MLAT to the UK. Months of formal cooperation were saved. Court submission used hashed artefacts, each cited under Qanun-e-Shahadat Article 164. The subject's UWO defence had to explain not the existence of the flat — which was now documentary — but its source.

The lesson is not that OSINT replaces formal investigation. It is that OSINT *targets* and *accelerates* formal investigation, and provides an evidentiary chain that survives motion practice.

<a id="limits"></a>

## 2.10 Limits and pitfalls of OSINT

The honest list of where OSINT fails or backfires:

- **Confirmation bias.** Looking only for evidence that supports the theory of the case. Mitigation: explicitly write the disconfirming hypothesis at the start, and search for it first.
- **Stale data.** A registry record from 2019 may be wrong in 2026. A WHOIS record from before the registrar privacy rule may show real owner; after, it shows a proxy. Always confirm a finding with the most current available source.
- **Impersonation.** Parody, fake, and impersonator accounts are routinely mistaken for the subject. A "verified" badge means almost nothing on most platforms now. Cross-check identity claims with at least two independent indicators.
- **AI fabrication.** Large-language-model summaries of OSINT findings frequently hallucinate sources, dates, and connections. Never use an AI summary as evidence; always click through to the underlying source.
- **Over-reach.** Crossing into PECA-restricted territory destroys the case. Even unintentional crossing — say, a Tor session that touches a stolen-data marketplace and then transmits the stolen data back — is a problem.
- **Single source.** One social-media post is suggestive. Never conclusive. Two independent sources is suggestive. Three independent sources from different categories is court-worthy.

The operating principle: **OSINT is corroboration, not conclusion**. Every finding must be second-sourced before it goes into a court submission.

---

<a id="module-3"></a>

# Module 3 — OSINT Frameworks and Methodology

<a id="why-frame"></a>

## 3.1 Why frameworks beat tools

A consistent finding across investigative units is that **structure beats talent over time**. A new analyst with a documented framework outperforms a brilliant analyst with no framework, because:

- **Reproducibility.** Two analysts on the same target produce the same finding from the same artefacts. The case stands up because the method is fixed, not because the people are.
- **Defensibility.** A documented framework is the shield against allegations of cherry-picking or impermissible methods. "We used the standard X framework, recorded every step under it, and produced this finding" is a much better answer in court than "I just searched around".
- **Onboarding.** New officers ramp on the framework, not on tribal knowledge. The unit's capacity scales linearly with hires.

**The investigator's edge is method, not access.** Public information becomes intelligence only when it is collected and reasoned about systematically.

<a id="framework"></a>

## 3.2 The OSINT Framework and Bellingcat Toolkit

Two free reference frameworks dominate the field:

**[osintframework.com](https://osintframework.com)** is a categorised tree of OSINT resources, community-maintained. The site's value is not as a tool — it is as a *coverage check*. Walking the tree from intent → category → tool prompts: *what would I miss if I skipped this?* For a new analyst, it is the best starting point. The tree's main branches:

- **Username** — Sherlock, WhatsMyName, Namechk, KnowEm.
- **Email Address** — Hunter.io, Holehe, EmailRep.
- **Domain Name** — crt.sh, WHOIS lookup, Wayback Machine.
- **IP Address** — Shodan, Censys, RiskIQ.
- **Phone Number** — PhoneInfoga, Truecaller-pivot.
- **Images / Videos** — TinEye, Yandex Images, Google Lens, InVID.
- **Social Networks** — per-platform research tools.
- **People Search Engines** — Pipl, Spokeo (jurisdiction-dependent).
- **Documents** — Google dorking, document scraping.
- **Geolocation Tools / Maps** — SunCalc, Wikimapia, Overpass Turbo.
- **Threat Intelligence** — VirusTotal, AbuseIPDB.

**[Bellingcat Online Investigation Toolkit](https://bellingcat.gitbook.io)** is the field-tested counterpart. Maintained by [Bellingcat](https://www.bellingcat.com), an investigative journalism organisation that has set the modern standard for open-source investigations (MH17, Skripal, ongoing Russia/Ukraine). The toolkit is used in training by NCA, FBI Cyber, and many FATF members. It is more curated than osintframework — fewer tools, more depth on each.

Other resources worth bookmarking:

- **[Intel Techniques tool repository](https://inteltechniques.com/tools/)** — Michael Bazzell's curated list. Updated frequently.
- **[Aware Online OSINT tools](https://www.aware-online.com)** — strong on social-media research.
- **[Start.me OSINT collections](https://start.me)** — community-curated bookmark sets.

**Operational practice:** keep one open browser tab to osintframework.com and one to the Bellingcat toolkit during any investigation. Treat them as the coverage-check sidebars to your case-specific work.

<a id="applied"></a>

## 3.3 The intelligence cycle, applied to a case

In practical terms, what does each step of the cycle look like in an actual NAB / AMLA case?

**01 — PLAN.** Write the PIR on a single page. Subject, question, decision, indicators, boundary, deadline. Get sign-off from the case officer. Without sign-off, the PIR is not real.

**02 — COLLECT.** Map sources to the PIR question. For each source, capture the original (Hunchly or equivalent), record the URL and timestamp, hash the artefact, log it. Resist the urge to read deeply during collection — collection mode and analysis mode are different.

**03 — PROCESS.** Translate non-English documents (Pakistan ML cases routinely involve Arabic, Russian, Chinese filings). De-duplicate findings — the same person referenced 40 times is still one entity. Extract structured rows: entities (people, companies, addresses), relationships (director-of, owner-of, shareholder-of), events (incorporation date, transaction date).

**04 — ANALYZE.** Pivot from each finding to its corroboration source. Apply the Admiralty Code grade to every entry. Build a timeline. Look for inconsistencies — these are the leads. Write conclusions explicitly tied to evidence; never beyond it.

**05 — DISSEMINATE.** Brief the case officer in their preferred format (typically a 1-2 page memo with annexed exhibits). Receive feedback. Update the PIR with new questions raised. Begin the next cycle.

The cycle should typically take **hours to days** for a focused PIR. If a PIR is taking weeks, it is too broad — split it.

<a id="maltego-method"></a>

## 3.4 The Maltego methodology — entities, transforms, pivots

[Maltego](https://maltego.com) is the standard tool for visual link analysis in OSINT. Beyond the tool itself, the **Maltego methodology** — *entities*, *transforms*, *pivots* — is a useful mental model for any investigation, even when not using Maltego.

**Entities** are the nouns: Person, Email, Phone, Domain, IP, URL, Company, Document, Location, Image, Wallet. Each entity has a fixed set of properties. Each entity in your case is a node in the graph.

**Transforms** are the verbs that take one entity and produce another: "Domain → Email Addresses [Search]" produces a list of Email entities from a Domain entity. "Person → OpenCorporates → Director" produces a list of Company entities. "Phone → SocialLinks → Telegram" attempts to produce a Telegram-handle entity. Each transform is one OSINT query, encoded.

**Pivots** are the chains of transforms. A typical pivot starts with one Person entity, runs a transform to extract Emails, runs another transform on each Email to extract Companies, runs another to extract Directors, and so on. The graph expands.

**The pivot principle:** every artefact is a node, every transform is an edge. Each new entity becomes the next query. That *is* the OSINT graph — the visual representation of the case.

**Maltego CE limits.** The free Community Edition caps each transform at 12 results, limiting how far you can pivot before paying. Maltego XL removes the cap and adds collaboration features. Pakistan-focused transform sets exist for SECP, FBR-NTN lookup, court records — built either by Maltego's transform marketplace or by local integrators.

**Workflow tip.** Always start with a single high-confidence entity (a verified email, a registered company name from an official filing). Let the transforms do the discovery — do not pre-judge the graph shape. Surprises in the graph are usually leads.

---

<a id="module-4"></a>

# Module 4 — Kali Linux Toolkit

<a id="kali"></a>

## 4.1 What is Kali Linux

**Kali Linux** is a Debian-based Linux distribution maintained by [Offensive Security](https://www.offensive-security.com). It ships with 600+ security and intelligence tools pre-installed and signed. For OSINT investigators, Kali is essentially the *workstation in a box* — the work of installing, versioning, and updating tools is done for you.

**How investigators run it.** Inside a virtual machine on [VirtualBox](https://www.virtualbox.org) or [VMware Workstation](https://www.vmware.com/products/workstation-player.html). The VM sits fully isolated from the host operating system. A clean snapshot is taken before every research session, and reverted after — eliminating persistent contamination. Kali on a bare metal laptop is uncommon for investigators (the OPSEC discipline of snapshotting is too valuable to give up).

**Why it matters for case work.** Reproducibility (every analyst can stand up the same VM); auditability (the VM's package state is fully recorded); cost (free); and field validation (the same tools NCA, Europol financial-crime, and FATF training partners use day-to-day).

**Reference VM specification:**

- Distribution: Kali Linux 2026.1 (or latest rolling at session time)
- RAM: 8 GB minimum (12 GB recommended for Maltego CE + SpiderFoot in parallel)
- CPU: 4 vCPU minimum
- Disk: 80 GB thin-provisioned
- Network: NAT or Bridged with static MAC
- Snapshot: clean snapshot named `pre-demo` before every session

The remaining sections of this module cover the specific OSINT tools investigators reach for most often. The full hands-on commands for each tool — including expected output, troubleshooting, and pivots — are in the companion **Speaker Notes** PDF.

<a id="harvester"></a>

## 4.2 theHarvester

**[theHarvester](https://github.com/laramies/theHarvester)** is the canonical passive-recon tool. Given a target domain, it aggregates emails, subdomains, hosts, employee names, and IP addresses from public search engines and certificate-transparency logs — *without sending a single packet to the target*.

**Why investigators love it.**

- Seconds to a coverage map of a target domain.
- Passive — the target sees nothing. No probes, no scans.
- Output to JSON / CSV / HTML reports — directly attachable to a case file.
- Sources include crt.sh, DuckDuckGo, Bing, AlienVault OTX, Hunter, Shodan, Hackertarget — the full passive sweep.

**Typical command.**

```
theHarvester -d acme-trading.pk \
    -l 500 \
    -b crtsh,duckduckgo,bing,otx \
    -f harvest_acme
```

**Expected output (abridged).**

```
[*] Target: acme-trading.pk
[*] Searching crtsh, duckduckgo, bing, otx.

[*] Hosts found: 27
hr.acme-trading.pk
mail.acme-trading.pk
finance.acme-trading.pk
vpn-staging.acme-trading.pk
...

[*] Emails: 14
ceo@acme-trading.pk
finance@acme-trading.pk
...

[*] People: 6
- Ali Ahmed - CFO
- Fatima Khan - Compliance Lead
...
```

**Pivots produced.**

- Each email → [HaveIBeenPwned](https://haveibeenpwned.com) (was the email in a breach?), Holehe (which sites use this email?).
- Each subdomain → Amass / subfinder for further enumeration; Eyewitness for a screenshot.
- Each person → Sherlock / LinkedIn for cross-platform footprint.

**The investigative insight.** Subdomains often disclose internal structure — `vpn-staging`, `finance`, `payroll` — revealing what a "shell company" actually runs. Email format leaks naming convention; once you know the convention, every name on LinkedIn becomes a valid email guess.

<a id="recon-ng"></a>

## 4.3 Recon-ng

**Recon-ng** is a *modular framework* for OSINT — closer to Metasploit's structure than to a single-purpose script. The model is a marketplace of 100+ modules, each performing a specific OSINT operation; workspaces that isolate cases; a database that persists hosts, contacts, and profiles automatically.

**Why investigators use it.**

- Marketplace of 100+ modules covering domain, host, contact, profile, vulnerability, and reporting categories.
- Workspaces — every case has its own database. You can return to a workspace months later and re-run modules to refresh the data.
- HTML and CSV reports — one command emits a structured report ready to attach to the case file.

**Typical session.**

```
$ recon-ng

[recon-ng] > marketplace install all
[recon-ng] > workspaces create acme
[recon-ng] > modules load recon/domains-hosts/hackertarget
[recon-ng] > options set SOURCE acme-trading.pk
[recon-ng] > run
[recon-ng] > modules load recon/hosts-hosts/resolve
[recon-ng] > run
[recon-ng] > show hosts
[recon-ng] > modules load reporting/html
[recon-ng] > run
```

The HTML report from the last step is the artefact that goes into the case file — already structured, hashable, and linkable.

<a id="sherlock"></a>

## 4.4 Sherlock and WhatsMyName

**[Sherlock](https://github.com/sherlock-project/sherlock)** and **[WhatsMyName](https://whatsmyname.app)** answer one question: given a username, on which sites does an account with that username exist?

The investigative motivation is **username reuse**. Most people use the same username — `first.last`, `firstlast`, or a personal handle — across many platforms. This is the single biggest OPSEC mistake non-professional subjects make. Once Sherlock returns 5 hits, you have 5 different views of the same person — five chances to cross-corroborate identity.

**Typical run.**

```
$ sherlock john.smith \
    --timeout 5 \
    --print-found \
    --output sherlock_johnsmith.txt

$ sha256sum sherlock_johnsmith.txt >> ~/case/artefact_log.csv
```

**Expected output.**

```
[+] GitHub:    https://github.com/john.smith
[+] Twitter:   https://twitter.com/john.smith
[+] Instagram: https://instagram.com/john.smith
[+] Reddit:    https://reddit.com/user/john.smith
[+] Medium:    https://medium.com/@john.smith
[+] Keybase:   https://keybase.io/john.smith
[+] HackerNews: https://news.ycombinator.com/user?id=john.smith
```

**Caveats.** Sherlock has false positives — its site list ages, and some checks misfire. Always click through each URL to confirm. **WhatsMyName** is a complementary web tool, often slightly different list of platforms.

**Investigative insight.** GitHub is often a goldmine in financial-crime cases — a developer at a target company will publish, in public commits, the company's API endpoints, infrastructure notes, sometimes API keys. Always check.

<a id="spiderfoot"></a>

## 4.5 SpiderFoot

**[SpiderFoot](https://www.spiderfoot.net)** is the automated, full-spectrum OSINT scanner. Throw it an email, IP, domain, person, or wallet, and it runs every applicable module — 200+ — in parallel, deduplicates the results, and graphs them.

**Two modes.**

- **Web UI.** Run as a local server: `spiderfoot -l 127.0.0.1:5001`, then browse to `http://127.0.0.1:5001`. Visual exploration, dashboards, drill-downs.
- **CLI.** `sf -s suspect@company.pk -o csv > sf_email.csv` for scripted runs, suitable for piping into pandas or NetworkX.

**Scope discipline.** 200+ modules also means 200+ ways to drown in noise. On the first run, restrict to "Investigate → Footprint" only. Add categories (Brand, Intelligence Sources, Vulnerabilities) selectively as the investigation needs them. A scan with all categories enabled on a single email can take hours and produce thousands of low-relevance findings.

**When SpiderFoot wins.** Pre-targeting before a formal request. SpiderFoot can give you a 200-source-deep dossier on a subject in 30 minutes — letting you prioritise *which* of the 200 sources to dig into manually.

<a id="maltego"></a>

## 4.6 Maltego Community Edition

**[Maltego](https://maltego.com)** is the standard for visual link analysis. The Community Edition (CE) is free; XL is paid and removes Community-tier limits.

**Workflow.** Drag a Person / Domain / Email entity onto the canvas. Right-click → run a transform. Results expand the graph. Each result entity can be transformed in turn. The graph emerges as you work.

**The visual advantage.** Investigators see relationship structure directly — who is connected to whom, through what paths, with what kind of connection. The graph reveals **clusters** (groups of tightly connected entities, often shell-company networks) and **brokers** (entities that connect otherwise disconnected clusters — typically the controllers or facilitators).

**Transform marketplace.** Free transforms cover the most common pivots; paid transforms (some by Maltego, some by third parties like Sociallinks) cover deeper sources. Pakistan-focused transform sets exist for SECP, FBR-NTN, and court records — built by Maltego's transform marketplace or by local integrators.

**Workflow tip.** Always start with a single high-confidence entity (a verified email, a registered company from an official filing). Let the transforms discover the graph — do not pre-judge the shape. Surprises in the graph are usually leads.

**Note on CE limits.** The 12-result-per-transform cap matters when you are pivoting on a high-degree entity (like a popular email domain). For deeper work, Maltego XL removes the cap; CLERINT Fusion offers similar graph-analytic capability with airgap support.

<a id="exiftool"></a>

## 4.7 ExifTool

**[ExifTool](https://exiftool.org)** reads metadata embedded in documents and images. The aphorism is *every document is a confession* — ExifTool reads the part the author didn't mean to share.

**What it reads.**

- **PDF / Office documents:** Author, Creator, Producer, Company, Create Date, Modify Date, Print Date, Title, Subject, Keywords, edit history (Office documents store full revision history).
- **Photos (JPEG, HEIC, RAW):** Camera Make, Model, Serial Number, GPS Latitude/Longitude, Create Date, Lens, exposure data.
- **Many other formats** — video, audio, archives.

**Typical commands.**

```
$ exiftool leaked-document.pdf

$ exiftool -Author -Creator -Producer -CreateDate -ModifyDate \
    -Title -Subject ~/case/leaked-document.pdf

$ exiftool -GPS:all -CreateDate -Make -Model photo.jpg

$ exiftool -csv -r -ext pdf -ext docx -ext jpg ~/case/leaked/ > metadata.csv
```

**Investigative payoffs.**

- **Author and Company fields** often pin a leaked document to an exact employee or organisation. The ML case literature has multiple examples where a PDF's author field broke open the case.
- **Create vs Modify date** reveals whether a "final" document was recently doctored. A modify date a year after creation is a flag.
- **GPS in photos** — paste coordinates into Google Maps and you stand where the photographer stood. This is the moment in a workshop that converts skeptics every time.
- **Bulk metadata extraction** across a folder of leaked documents reveals the author/department network — effectively, an org chart for free.

**Caveats.** Sophisticated leakers strip metadata. `qpdf --linearize --remove-metadata` does it. If a document returns no metadata, that *itself* is a signal — the leaker is aware. Also try `pdfinfo` as a secondary; sometimes residual XMP survives stripping.

<a id="amass"></a>

## 4.8 Domain reconnaissance — Amass, subfinder, crt.sh

Three tools, one job: enumerate every subdomain of a target domain.

**Amass** is the most thorough. It does both passive (no traffic to target) and active (DNS queries) enumeration, and includes a built-in graph database to track findings over time.

```
$ amass enum -passive -d acme-trading.pk -o passive.txt
$ amass enum -active -d acme-trading.pk -o active.txt
```

**subfinder** is faster, passive-only. Good for first-pass coverage before the slower Amass run.

```
$ subfinder -d acme-trading.pk -all -o subfinder.txt
```

**[crt.sh](https://crt.sh)** is the public certificate-transparency search. Every TLS certificate ever issued is logged to public CT logs by every certificate authority — even certs that have since expired or been revoked. crt.sh searches those logs.

```
$ curl -s "https://crt.sh/?q=%25.acme-trading.pk&output=json" \
    | jq -r '.[].name_value' \
    | sort -u
```

**Why CT logs matter.** A target may have removed a subdomain from DNS, but the certificate is still in the public log forever. CT logs reveal subdomains the target has tried to scrub.

**Combine the three.**

```
$ cat passive.txt active.txt subfinder.txt | sort -u > subdomains.txt
$ wc -l subdomains.txt
```

The combined list usually surfaces 2-5x more subdomains than any single tool alone.

<a id="toolkit-ref"></a>

## 4.9 The full Kali OSINT toolkit reference

A fast reference table for "what to reach for, when":

| Category            | Primary tools                                                |
|---------------------|--------------------------------------------------------------|
| Domain & DNS        | theHarvester · Amass · subfinder · crt.sh                    |
| People search       | Sherlock · WhatsMyName · OSRFramework · Maigret              |
| Email               | Holehe · h8mail · EmailRep                                   |
| Metadata            | ExifTool · pdfinfo · MAT2                                    |
| Visual recon        | Eyewitness · Aquatone · gowitness                            |
| Web crawler         | Photon · Katana · gospider                                   |
| Crypto              | Etherscan CLI · BTC.com explorer                             |
| Phone               | PhoneInfoga · Truecaller-pivot                               |
| Frameworks          | Recon-ng · SpiderFoot · Maltego CE                           |

For any tool not covered above, the Speaker Notes PDF contains commands, expected output, and pivots.

---

<a id="module-5"></a>

# Module 5 — OSINT Sources and Platforms

<a id="dorking"></a>

## 5.1 Google dorking

Google dorking — the precise use of search-engine operators — is your **oldest** OSINT tool, and still one of the highest-yield. Six operators, used in combination, get you to the artefact in five iterations.

**The operators.**

- **`site:`** — restrict to a single domain.
- **`filetype:`** — restrict to a file extension. PDF is the highest-yield in financial-crime work.
- **`intitle:`** — match in the page title.
- **`inurl:`** — match in the URL.
- **Quoted exact match** — `"exact phrase"`.
- **`OR`** — alternation.
- **`-`** — exclusion (e.g. `-jobs` to filter out recruiting noise).

**Typical dorks for a case.**

```
# Site-restricted search
site:acme-trading.pk

# Find disclosed PDFs
site:acme-trading.pk filetype:pdf

# Find spreadsheets — finance leaks live here
site:acme-trading.pk (filetype:xls OR filetype:xlsx OR filetype:csv)

# Login portals (good for footprint, not for attack)
site:acme-trading.pk inurl:login OR inurl:admin

# Indexed directories — real gold
intitle:"index of" site:acme-trading.pk

# Subject across regulators / news
"Mr. Subject Name" (site:secp.gov.pk OR site:nab.gov.pk OR site:dawn.com)

# Email exposure on paste sites
"target@acme-trading.pk" (site:pastebin.com OR site:ghostbin.com)

# Killer dork — disclosure documents naming director
"Mr. Subject Name" (filetype:pdf OR filetype:docx) (intext:"director" OR intext:"shareholder")
```

**Don't stop at Google.** Run the same dorks on [Bing](https://bing.com), [DuckDuckGo](https://duckduckgo.com), and [Yandex](https://yandex.com). Yandex indexes Russian and Central Asian sites significantly better than Google — useful for cross-border ML work involving the CIS.

**Common pitfall.** Google rate-limits aggressive dorking and may serve a CAPTCHA. Switching to DuckDuckGo (no CAPTCHA) or rotating VPN endpoints helps. Repeated CAPTCHA attempts will get the IP hard-blocked — don't push past the warning.

<a id="socmint"></a>

## 5.2 Social media intelligence (SOCMINT)

People leak more on social media than they realise — and senior public-sector subjects in Pakistan are frequently *under*-sanitised, especially their family members.

**Six categories of signal.**

1. **Profile metadata** — bio, location, join date, language, account history. Account history reveals when a persona was built (and is therefore a powerful indicator for sockpuppet detection).
2. **Friend graph** — followers and following expose the network even on protected accounts (you can frequently see the *count* and the partial list).
3. **Posts and comments** — every interaction is a data point. Pinned tweets, replies, hashtags often reveal more than the headline content.
4. **Photos and videos** — faces, locations, vehicles, documents accidentally in frame. Background details are routinely the most informative parts of a photo.
5. **Check-ins** — geo-tagged stories and tagged locations show movement patterns over time.
6. **Connected apps** — third-party services linked to the account. A subject who linked Signal to their public Twitter has revealed their operational chat tool.

**Major platforms relevant in Pakistan ML cases.** Facebook (still dominant for older subjects, family networks), Twitter/X, Instagram (lifestyle visibility — especially second-generation), LinkedIn (corporate networks), Telegram (operational channels for hawala and crypto), WhatsApp (private — not OSINT in the strict sense, but contact-graph metadata via mobile-OS analysis is OSINT-adjacent), TikTok, YouTube.

**OPSEC reminder.** Sockpuppet accounts must be built slowly, with consistent persona, never linked to office IPs. A single login mistake can attribute the entire investigation back to the unit. The sockpuppet discipline is detailed in §7.1.

<a id="image"></a>

## 5.3 Image intelligence

A single photograph carries more investigative information than its uploader usually realises.

**From the image itself.**

- **EXIF metadata** — camera, GPS coordinates (often), timestamp. Per ExifTool §4.7.
- **Faces** — count, gender, approximate age. Some platforms surface this automatically.
- **Vehicles** — make, model, plate (where visible). Plate-readable photos are gold for asset tracing.
- **Documents** — visible text, logos, stamps in the background. A "selfie at the office" routinely shows screen content visible behind the subject.

**Reverse-search engines.** Each has a strength.

- **[Google Lens](https://lens.google.com)** — best for faces and consumer products.
- **[Yandex Images](https://yandex.com/images)** — strongest for faces in Russian / CIS imagery; often returns matches Google misses.
- **[TinEye](https://tineye.com)** — strongest for tracing the *original* source of an image (when it first appeared online).
- **[Bing Visual Search](https://www.bing.com/visualsearch)** — surprisingly effective for buildings and exteriors.

**Geolocation cross-check.** [SunCalc](https://www.suncalc.org) gives the sun's position for any location and date. Combined with shadow direction in a photograph, it can confirm or refute a claimed location with surprising precision. Bellingcat's MH17 work used this technique extensively.

**Practical workflow.** A subject claims a photograph was taken at location A on date B. SunCalc says shadows at A on B should fall NNE. Image shows shadows falling SW. Either the location is wrong, the date is wrong, or both. You have a lead.

<a id="domains"></a>

## 5.4 Domains, WHOIS, DNS, certificate transparency

Infrastructure tells stories people don't.

**WHOIS.** Registrar, registrant org, registration date, name servers. Privacy-proxy services hide the *name* but rarely the *registration date*. A "newly-formed shell" with a domain registered the day before the suspicious wire transfer is a tell. WHOIS history (paid: Whoxy, DomainTools) often reveals pre-privacy snapshots showing the original registrant.

**DNS.** A, MX, TXT records reveal hosting provider, mail provider, and infrastructure patterns. The same MX record across multiple "unrelated" companies is a strong signal that those companies share an operator.

**Certificate Transparency.** Every public TLS certificate is logged to public CT logs by every certificate authority. [crt.sh](https://crt.sh) and [Censys](https://search.censys.io) make those logs searchable. CT reveals every subdomain the target ever issued a certificate for — including ones long since removed from DNS. Wildcard SANs (Subject Alternative Names) often list 50+ domains under a single operator.

**[Wayback Machine](https://web.archive.org).** Reveals what a website said before it was scrubbed. Old "About" pages and team rosters are gold for shell-company traces. The Wayback Machine has captures going back to 1996 for many sites.

**Worked example.** A shell company's website today shows a generic landing page. crt.sh reveals 12 subdomains, including `careers`, `internal`, and `vpn`. Wayback Machine shows the same domain in 2019 had a full team page with three named individuals — none of whom are listed today. Those three names go into the case file as historical principals to investigate.

<a id="corporate"></a>

## 5.5 Corporate records and beneficial ownership

Corporate registries are the foundation of ML / NAO OSINT. Coverage varies by jurisdiction — some are exemplary, some opaque.

**Pakistan-specific.**

- **[SECP eServices](https://eservices.secp.gov.pk)** — directors, charges, filings.
- **FBR-NTN inquiry** — taxpayer existence check at [fbr.gov.pk](https://fbr.gov.pk).
- **[ECP asset declarations](https://ecp.gov.pk)** — for elected officials.
- **[PPRA tenders](https://ppra.org.pk)** — public procurement awards, bidder histories.
- **Provincial land records** — Punjab Land Records MIS, Sindh online deed search, KP digitised mauza records.
- **Court records** — Supreme Court of Pakistan case search, high-court daily-cause-lists.
- **Customs WeBOC** — partial public exposure of importer/exporter declarations.

**International.**

- **[OpenCorporates](https://opencorporates.com)** — 240M+ companies, 140+ jurisdictions.
- **[OCCRP Aleph](https://aleph.occrp.org)** — investigations, leaks, sanctions, PEP.
- **[ICIJ Offshore Leaks Database](https://offshoreleaks.icij.org)** — Panama / Pandora / Paradise / Bahamas / FinCEN.
- **[Sayari Search](https://sayari.com)** — beneficial-ownership focus, free tier limited.
- **[Companies House (UK)](https://find-and-update.company-information.service.gov.uk)** — full historical filings, free.
- **EU Business Register** — multi-state.
- **UAE DMCC, DIFC, ADGM registries** — variable transparency.

**Leaks and investigations.** Panama Papers (2016), Pandora Papers (2021), Paradise Papers (2017), Bahamas Leaks (2016), FinCEN Files (2020), Suisse Secrets (2022). Each is an indexed dataset — search through ICIJ or OCCRP Aleph. Each has been used in successful prosecutions globally.

**Quote-ready in court.** Registry data is documentary evidence under Article 73 of Qanun-e-Shahadat 1984. Always download the registry's official PDF copy and hash it — never rely on a screenshot of a screen-rendered version.

<a id="breaches"></a>

## 5.6 Breach and leak data

Breach-data indices are powerful but legally sensitive. Use them only when properly grounded.

**What they answer.**

- Has this email appeared in past breaches? (HaveIBeenPwned is the cleanest answer.)
- What password / hash style does the subject reuse? (Useful for confirming identity across accounts.)
- What other accounts are tied to this phone number? (Cross-platform exposure.)
- What aliases has this person used elsewhere? (Email-in-multiple-leaks → multiple platforms.)

**Common indices.**

- **[HaveIBeenPwned](https://haveibeenpwned.com)** — free, ethical. Aggregates publicly disclosed breaches. The right starting point.
- **[DeHashed](https://dehashed.com)** — paid, searchable across breaches.
- **[IntelligenceX](https://intelx.io)** — free tier; leaks, paste sites, darkweb.
- **[Snusbase](https://snusbase.com)** / **[LeakPeek](https://leakpeek.com)** — narrower indices.

**PECA boundary.** Use only third-party indexers that have already published the dataset publicly. Never purchase data from underground markets — that crosses into PECA §3 (unauthorised access) territory. When in doubt, get the prosecutor's nod before quoting in a brief. The defensible posture is: "the data is publicly available through commonly-used indexers; we are reading what is already in the public record."

<a id="darkweb"></a>

## 5.7 Dark web monitoring

The dark web — Tor and I2P — hosts illicit markets, leak forums, ransomware victim portals, sanctioned-actor chatter, hawala broker channels, and cryptocurrency mixer ads. For ML / NAO investigations, the relevant questions are: is the subject mentioned? Is their phone, email, or wallet referenced? Are their organisation's documents being leaked or sold?

**How to access.** [Tor Browser](https://www.torproject.org) in a *dedicated VM*. Never on a research-network machine connected to the office. The OPSEC discipline is non-negotiable: revert the VM to clean snapshot after every session.

**What to monitor.**

- Subject names, phone numbers, wallet addresses.
- Company names — leaked corporate documents commonly appear on dump sites.
- NAB officers' names — counter-intelligence concern.

**Tools.**

- **[Ahmia](https://ahmia.fi)** — Tor search engine.
- **DarkSearch** — alternative search.
- **OnionLand** — directory.
- **Specific market indexes** — change frequently as markets are seized.

**Critical safety rule.** Never download or click links on the dark web from a personal machine. Use the VM-snapshot-and-revert pattern after every session. The risk is not just legal — it is malware-driven compromise of investigative equipment.

<a id="geospatial"></a>

## 5.8 Geospatial / GEOINT workflow

Putting the money on a map.

**Imagery sources.**

- **[Google Earth Pro](https://earth.google.com)** — free desktop, historical imagery slider going back to early 2000s in many areas. The historical slider is the single most powerful free GEOINT tool.
- **[Sentinel Hub EO Browser](https://apps.sentinel-hub.com/eo-browser)** — 10-metre resolution, free, weekly cadence, going back years. Excellent for change detection.
- **[Bing Maps](https://www.bing.com/maps)** — different vintage of imagery to Google; sometimes captures what Google misses.
- **Open Maxar samples** — sub-metre commercial samples available periodically.

**Property records.**

- Punjab Land Records MIS.
- Sindh online deed search.
- KP digitised mauza records.
- UK Land Registry, Dubai DLD, Canadian provincial registries, Spain Catastro, France BAN.

**Movement tracking.**

- **[MarineTraffic](https://marinetraffic.com)** / **[VesselFinder](https://vesselfinder.com)** — AIS vessel-tracking, ships' routes for years.
- **[FlightRadar24](https://flightradar24.com)** / **[ADS-B Exchange](https://www.adsbexchange.com)** — flight tracking history. Useful for private-aircraft tracking in PEP investigations.
- **[OpenStreetMap](https://openstreetmap.org)** + **[Overpass Turbo](https://overpass-turbo.eu)** — query buildings, roads, and POIs by polygon.

**[SunCalc](https://www.suncalc.org)** — sun position for any location and date. Cross-check shadows in photographs.

**Layered analysis (the typical investigative move).**

1. Take the subject's declared ECP asset list.
2. Lay it next to satellite imagery over time at the declared address.
3. Check the property registry record for the same address.
4. Compare with social-media photos showing the property.
5. Investigate any discrepancy — in declaration, in registry, in imagery, or in photos.

The discrepancies are the case.

<a id="crypto-detail"></a>

## 5.9 Crypto OSINT in detail

A deeper treatment of cryptocurrency OSINT than the slide-level overview in §2.7.

**Why crypto matters in ML.** Crypto rails enable sanctions evasion, hawala-equivalent cross-border transfer, and laundering on top of predicate offences. Pakistan's State Bank prohibits crypto trading domestically — but illicit actors operate via foreign exchanges and peer-to-peer markets accessible via VPN.

**The on-chain advantage.** Every BTC, ETH, TRX, BSC, SOL, XMR(?) — actually XMR is private — every major chain transaction is publicly logged. Unlike a bank's records, no warrant is required to read them. Following the chain is purely OSINT.

**Block explorers — the basic tools.**

- **Bitcoin** — [blockchain.com](https://blockchain.com), [mempool.space](https://mempool.space), [blockstream.info](https://blockstream.info).
- **Ethereum** — [etherscan.io](https://etherscan.io). The richest tooling.
- **Tron** — [tronscan.org](https://tronscan.org). Heavy USDT volume.
- **BNB Smart Chain** — [bscscan.com](https://bscscan.com).
- **Polygon** — [polygonscan.com](https://polygonscan.com).
- **Solana** — [solscan.io](https://solscan.io).

**A typical workflow on a target wallet.**

1. Open `https://etherscan.io/address/<TARGET>`.
2. Note balance, first / last activity dates, total in / out, contract interactions.
3. Click "Token Holdings" — stablecoins (USDT, USDC) are the laundering staple.
4. "Internal Txns" — reveals contract-call cash-outs not visible in the main tx list.
5. Trace transfers ≥ $10K to the next address. Repeat. Most chains stop laundering at 3-5 hops because the next address is a mixer or an exchange deposit.

**Sanctioned-address checks.** The OFAC SDN list includes crypto addresses (BTC, ETH, USDT, TRX) for sanctioned entities.

```
$ curl -s https://www.treasury.gov/ofac/downloads/sdn.csv -o sdn.csv
$ grep -i 'XBT\|ETH\|USDT\|TRX' sdn.csv | head -20
$ grep -i '<TARGET_WALLET>' sdn.csv
```

**Mixers, bridges, and cash-outs.**

- **Mixers** — Tornado Cash (sanctioned 2022), Wasabi, Samourai. Inflow patterns are publicly known.
- **Cross-chain bridges** — ETH → Tron → BSC laundering tells. Each bridge has known canonical contract addresses.
- **Exchange deposits** — known Binance, Bybit, KuCoin deposit addresses signal fiat off-ramp coming.

**Free graph-analytic platforms.**

- **[Breadcrumbs.app](https://breadcrumbs.app)** — graph BTC/ETH addresses, free tier.
- **[Arkham Intelligence](https://arkhamintelligence.com)** — entity-tagged dashboards.
- **[Chainabuse](https://chainabuse.com)** — community scam reports.

**Pakistan-specific framing.** SBP's restriction on trading does not change the OSINT analysis — you are observing a public ledger, not transacting. Treat artefacts under Article 164 chain-of-custody discipline.

<a id="enterprise"></a>

## 5.10 Enterprise OSINT platforms

When the case spans hundreds of entities and millions of transactions, free tools hit their ceiling. Enterprise OSINT platforms compress weeks of analyst time into hours.

**Maltego XL.** Removes the CE 12-result-per-transform cap. Massive transform marketplace, including paid sets for OFAC, financial-crime, and Pakistan-focused registries. The graph-analytics standard for link analysis.

**Sociallinks Crimewall.** 500+ source connectors across social media, deep web, dark web, and crypto. In use at FIA Pakistan; the strength is breadth — investigators get visibility into platforms a single open-source tool cannot.

**CLERINT OSINT.** Indigenous Pakistan platform. Strong on Crypto-OSINT and Social-OSINT modules tailored for local typologies (hawala patterns, regional social platforms, local crypto P2P markets).

**CLERINT Fusion.** Airgapped, AI-assisted, knowledge-graph fusion of CDR + IPDR + financial transactions + OSINT. Designed for classified environments where outbound network traffic is prohibited.

**The investment calculus.** A single enterprise platform license is typically priced in tens of thousands of USD per analyst per year — significant for a unit budget, but cheap relative to the analyst-time it saves. The unit economics work when the platform handles 5+ active cases per analyst.

---

<a id="module-6"></a>

# Module 6 — CDR and IPDR Analysis

<a id="cdr-what"></a>

## 6.1 What is a CDR

**Call Detail Records (CDRs)** are the metadata records every mobile operator generates for every call. Per call: A-party (caller), B-party (called), start time, duration, IMEI (handset), IMSI (SIM), cell tower (LAC + CellID), call type. In Pakistan, the major operators (Jazz, Telenor, Zong, Ufone) all generate CDRs in real time.

**What CDRs are** — *metadata*. Who called whom, when, for how long, and from approximately where.

**What CDRs are not** — *content*. CDRs do not contain the audio of calls. Audio requires lawful intercept, which is a different (and stricter) legal regime than CDR access. CDR analysis is legally controlled — never analyse a CDR you have not received through proper case authority under NAO §27, AMLA §7, or equivalent.

**How investigators get them.** Through formal request to the operator under the relevant statute. Operators typically deliver as CSV or Excel — millions of rows for a single subject's year of activity.

<a id="cdr-anatomy"></a>

## 6.2 Anatomy of a CDR record

The fields an analyst actually uses:

| Field          | Type            | Investigator value                                          |
|----------------|-----------------|--------------------------------------------------------------|
| `Aparty`       | String (E.164)  | Calling number — your subject if outgoing                   |
| `Bparty`       | String (E.164)  | Called number — pivot to the contact                        |
| `StartTime`    | Timestamp       | Call start; align with financial events                     |
| `Duration`     | Seconds         | Long durations = relationship; bursts = burner              |
| `IMEI`         | String          | Handset identity — survives SIM swaps                       |
| `IMSI`         | String          | SIM identity — tied to CNIC at issuance                     |
| `LAC + CellID` | Tower           | Approximate location at call time                           |
| `CallType`     | String          | MOC / MTC / SMS — voice vs text vs MMS                      |

The IMEI is particularly valuable because it survives SIM swaps. A subject who swaps SIMs to evade tracking is still using the same handset — the IMEI persists across swaps. Conversely, the IMSI binds to the CNIC at issuance (post-2008 SIM-CNIC binding) — providing the link from "this SIM" to "this human".

<a id="cdr-workflow"></a>

## 6.3 CDR analysis workflow

The five-stage workflow:

**01 — INGEST.** Load the CSV / Excel into pandas. Verify schema, fix encodings (operator exports vary), parse timestamps. Always re-validate the schema on each new export — operator column names are inconsistent.

```
import pandas as pd
df = pd.read_csv('cdr_export.csv', parse_dates=['StartTime'])
print(df.columns)
print(len(df))
```

**02 — PROFILE.** Top-N called, top-N callers, daily / nightly distribution. Get a feel for the data before pivoting.

```
# Top contacts
df[df.Aparty == TARGET].groupby('Bparty').agg(
    calls=('Bparty', 'size'),
    minutes=('Duration', lambda s: s.sum() / 60)
).sort_values('calls', ascending=False).head(20)

# Late-night clusters (00:00 – 05:00)
nights = df[df.StartTime.dt.hour.between(0, 4)]
nights[nights.Aparty == TARGET].groupby('Bparty').size().sort_values(ascending=False).head(10)
```

**03 — PIVOT.** Apply the analytical patterns: co-location (same tower, same time, two phones), burst pattern (sudden spike then silence), burner SIMs (short IMEI lifespan), tower co-location.

```
# Co-location at 5-minute granularity
df['ts5min'] = df.StartTime.dt.floor('5min')
pivot = df.groupby(['ts5min', 'LAC', 'CellID'])['Aparty'] \
    .apply(lambda s: set(s)) \
    .reset_index(name='phones')
pivot['together'] = pivot.phones.apply(
    lambda s: TARGET in s and len(s) > 1
)
```

**04 — GRAPH.** Build a NetworkX directed graph. Compute degree (top contacts) and betweenness centrality (brokers — nodes that connect otherwise disconnected sub-groups; these are the hawala / money-mule sweet spots).

```
import networkx as nx
G = nx.from_pandas_edgelist(df, 'Aparty', 'Bparty', create_using=nx.DiGraph)
degree = sorted(G.degree, key=lambda x: x[1], reverse=True)[:20]
betweenness = nx.betweenness_centrality(G, k=200)  # sampled
```

**05 — CORROBORATE.** Cross-reference with bank transactions, asset records, OSINT names. The CDR alone is suggestive; cross-referenced is conclusive.

For one-off cases, [pandas](https://pandas.pydata.org) + [NetworkX](https://networkx.org) in 30 lines of Python is enough. For unit-wide work, CLERINT Fusion ingests CDR + IPDR + financial transactions in one knowledge graph.

<a id="ipdr"></a>

## 6.4 What IPDR adds

**Internet Protocol Detail Records (IPDRs)** are the data-session counterpart to CDRs. Per session: subscriber (MSISDN / IMSI), source IP, destination IP, port, bytes up, bytes down, start and end timestamps, RAT type (4G / 5G), cell ID.

**What IPDR reveals beyond CDR.**

- **App fingerprint by destination IP / ASN.** Telegram's IP ranges are well-documented; Signal's are well-documented; Tor's are well-documented. Mapping destination IPs to known service ranges reveals which apps the subject uses.
- **Volume patterns** — file sharing vs chat. A 500MB upload to a specific IP at 2am is operationally very different from 5MB of chat.
- **Tor / mixer / VPN usage.** All visible in IPDR.
- **Behavioural rhythm** — work hours vs night activity, same as CDR but with finer granularity.

**Key constraint.** **IPDR does NOT carry payload.** You see the subscriber spoke to a Telegram IP — not what they said. Same Article 164 chain-of-custody applies as CDR.

**App fingerprinting by IP.** A starter mapping (real production work needs a much more comprehensive list):

| App      | Common IP prefixes       |
|----------|--------------------------|
| WhatsApp | 157.240. · 31.13. · 173.252. |
| Telegram | 149.154. · 91.108.       |
| Signal   | 13.248. · 76.223.        |
| Tor      | 199.249. · 171.25.       |

```
APP_MAP = { ... as above ... }

def label(ip):
    for app, prefixes in APP_MAP.items():
        if any(ip.startswith(p) for p in prefixes):
            return app
    return 'other'

ipdr['app'] = ipdr['DestIP'].astype(str).map(label)
ipdr[ipdr.MSISDN == TARGET].groupby('app').size().sort_values(ascending=False)
```

<a id="cdr-worked"></a>

## 6.5 A worked example

Reconstructing a day in a suspect's life from CDR + IPDR.

**06:30** — IPDR shows WhatsApp + Gmail traffic from the home tower. CDR shows three short calls to a known facilitator. The day is starting normally.

**09:00 – 17:00** — co-location with two other suspects on the same office tower for 6 hours. Office IPDR shows normal browsing. The work day looks ordinary.

**02:15** — IPDR connection to a Telegram IP for 9 minutes from a residential tower 12 km from the registered home. CDR is silent during this window. This is the anomaly.

**The investigative question:** what was the subject doing at a residential tower 12 km from home at 2:15 AM, using Telegram?

**The corroboration:** the bank-account activity timeline shows a 3 million PKR transfer initiated at approximately 02:30 AM on the same date. The Telegram session preceded the transfer. The recipient account is a previously-known associate.

The pattern — late-night Telegram session from an unexpected location, immediately preceding an off-hours bank transfer — became the focal evidence in the case.

The investigative power is in the **layering**. CDR alone shows nothing unusual. IPDR alone shows a Telegram session at an odd hour. Bank records alone show a transfer. Together, they tell a story.

<a id="cdr-pitfalls"></a>

## 6.6 Common pitfalls

Mistakes that lose CDR / IPDR cases:

- **Tower ≠ location.** Cell coverage overlaps. "Same tower" implies *proximity*, not co-presence in the same room. A defence expert will pull this apart if the case rests on it.
- **SIM ≠ identity.** Who actually held the SIM at call time? CNIC-binding helps but is not proof of physical custody. A case that asserts "subject made the call" rather than "subject's SIM made the call" is overreaching.
- **Time-zone slip.** Operator exports in UTC; analyst overlays in PKT. One bad join and the entire narrative is wrong by 5 hours. Always re-confirm timezone on each new export.
- **Schema drift.** Each operator's column names differ. Always re-validate the schema. A column named `OriginNumber` in one export and `Aparty` in another is a real-world hazard.
- **Sample bias.** Asking only for one subject's records misses peer SIMs. The investigative question is usually about the network around the subject — request the network, not just the subject.
- **Admissibility gap.** Hash the export, log the chain. Without it, a defence motion can exclude the entire dataset.

The discipline IS the case. A CDR analysis built on careful schema validation, hashed inputs, cross-confirmed timezones, and second-sourced findings is bullet-proof. One built on sloppy ingestion is not.

---

<a id="module-7"></a>

# Module 7 — Tradecraft and Closing

<a id="sockpuppets"></a>

## 7.1 Sockpuppets and investigative personas

Sockpuppet accounts — investigative personas — are a *tool*, not a costume. Get them wrong and they discredit the case.

**Build over time.** Real personas are aged at least 60 days before active use. A sudden creation followed by immediate target contact is a flag to any platform's anti-abuse system. Build the persona slowly: post non-controversial content, follow normal accounts, accumulate plausible history.

**Consistent attribution surface.** Same email pattern, same VPN endpoint, same browser fingerprint across the persona's life. Any drift in these breaks the persona — and may link the persona to your real infrastructure.

**One persona per case.** Never reuse a persona across investigations. Reuse links the cases for any future defence attorney: "Officer X used the same sockpuppet to investigate three different subjects, suggesting a pattern of impermissible methods." Don't give them that.

**Stay within entrapment lines.** The sockpuppet is for *observation*. Never solicit, never propose, never agree to a transaction. PECA, procedural law, and the Pakistan Penal Code are strict on entrapment. The lines are not always intuitive — when in doubt, the prosecutor approves the contact.

<a id="attribution"></a>

## 7.2 Attribution chains

How to tie one identity to another with evidentiary weight.

The investigator's chain rule: **any single attribution can be coincidence. Two independent attributions are suggestive. Three is a court-defensible identity claim.**

The categories of attribution:

- **Email reuse.** Same address across forum, marketplace, social — a single edge in the graph.
- **Username reuse.** Sherlock + WhatsMyName surface the recurring handle across 400+ sites.
- **Phone reuse.** Same number registered to multiple accounts (truecaller-pivot, holehe).
- **Wallet reuse.** Same crypto address re-used across scams, tipping, donation pages.
- **Profile photo.** Reverse search a profile pic across multiple platforms.
- **Stylometric.** Recurring phrases, typos, code-switching patterns in posts.

Each by itself is suggestive. Combined, they are court-defensible. A subject who uses the same Gmail across two LinkedIn accounts, the same crypto wallet across two donation pages, and the same stylometric fingerprint across two anonymous forums has, *without realising it*, given you a three-vector identity claim.

<a id="metadata"></a>

## 7.3 Metadata exploitation patterns

Where to look, what it reveals.

| Metadata source     | What it reveals                       | Why it matters                                          |
|---------------------|---------------------------------------|----------------------------------------------------------|
| PDF Author / Company| Exact employee &amp; org             | Pin a leaked document to a specific desk                 |
| Office edit history | Sequence of editors, last save        | Shows whether a "final" file was doctored later          |
| Photo EXIF (GPS)    | Camera, date, coordinates             | Geolocation; lifestyle confirmation                      |
| Email headers       | Originating IP, mail path             | Connect "anonymous" emails back to the sender            |
| HTTP / TLS metadata | Server, ciphersuite, certs            | Infrastructure attribution across sites                  |
| Crypto wallet hist. | First fund tx, behavioural pattern    | Cluster wallets to a single operator                     |

The investigator's habit: every digital artefact gets a metadata pass. Even when you think the metadata won't matter — it usually does.

<a id="discipline"></a>

## 7.4 Operational discipline checklist

The check-list to pin above every analyst's desk:

- [ ] Dedicated research VM with snapshot before each session.
- [ ] VPN with kill-switch; Tor for sensitive lookups.
- [ ] Browser profile separated from any logged-in personal account.
- [ ] Disable WebRTC, autofill, password manager on the research browser.
- [ ] Sockpuppets aged at least 60 days; one persona per case.
- [ ] [Hunchly](https://hunch.ly) (or equivalent) on every browser session.
- [ ] SHA-256 every artefact at the moment of capture.
- [ ] Artefact log row per finding with Admiralty grade.
- [ ] Never log into office systems from the research VM.
- [ ] Revert the VM to clean snapshot at end of session.

**The discipline IS the case.** A perfect finding from a contaminated environment is inadmissible. A modest finding from a clean one is bullet-proof.

<a id="path"></a>

## 7.5 A 90-day learning path

A pace card for any investigator who wants to build OSINT fluency without a budget. One concept per week.

**Weeks 1 – 4 — foundations.**

- Week 1: set up Kali VM. Run pre-flight checklist end-to-end on yourself or your own domain.
- Week 2: theHarvester + crt.sh + WHOIS deep-dive on a Pakistani public corporation.
- Week 3: Google dorking — read [Bishop Fox's Diggity cheatsheet](https://www.bishopfox.com); build your own dork list.
- Week 4: Sherlock + WhatsMyName + reverse image search on a journalist who publicly publishes.

**Weeks 5 – 8 — pivots and documentation.**

- Week 5: ExifTool + Hunchly. Build the artefact-log habit on 10 PDFs from public corporate sites.
- Week 6: Recon-ng workspaces + reporting/html on the same corporation.
- Week 7: Maltego CE; learn the transform chain mindset on a small synthetic case file.
- Week 8: SpiderFoot — read the Quick Start docs; learn module groups on the same case file.

**Weeks 9 – 12 — financial-crime depth.**

- Week 9: OpenCorporates + OCCRP Aleph + ICIJ Offshore Leaks cross-jurisdiction queries on a historical FATF case.
- Week 10: Pakistan SECP, FBR-NTN, ECP asset declarations, court records on one declared public official.
- Week 11: CDR / IPDR pandas recipes on synthetic data — never live-line.
- Week 12: Crypto OSINT — trace a known OFAC-listed wallet through five hops.

By day 90, you are the OSINT person in your unit. The companion Speaker Notes PDF has the full week-by-week plan with exercises.

<a id="resources"></a>

## 7.6 Resources and further reading

**Books.**

- *Open Source Intelligence Techniques* — Michael Bazzell. The bible of the field. Updated every 18 months. The standard reference for tradecraft.
- *The OSINT Handbook* — Dale Meredith / Packt. A practical workbook approach.
- *Bellingcat's Online Investigation Toolkit* (free, GitBook).

**Courses.**

- **[SANS SEC487](https://www.sans.org/cyber-security-courses/open-source-intelligence-gathering)** — Open-Source Intelligence Gathering and Analysis. The premier paid course. Worth it for any unit budget.
- **[OSINT Curious](https://osintcurio.us)** — community blog and YouTube channel. Free.
- **[Bellingcat Workshops](https://www.bellingcat.com)** — periodic, focused on investigative journalism methods.

**Frameworks and reference.**

- **[OSINT Framework](https://osintframework.com)** — coverage map.
- **[Bellingcat Toolkit](https://bellingcat.gitbook.io)** — curated tooling.
- **NATO OSINT Handbook (2001)** — historical baseline.
- **[ACPO / NPCC Good Practice Guide for Digital Evidence](https://www.npcc.police.uk)** — UK reference for chain of custody.
- **NIST SP 800-86** — guide to integrating forensic techniques into incident response.

**Pakistan portals.**

- **[NAB official](https://nab.gov.pk)**
- **[FMU (FIU Pakistan)](https://fmu.gov.pk)**
- **[SECP eServices](https://eservices.secp.gov.pk)**
- **[FBR e-FBR](https://e.fbr.gov.pk)** — NTN inquiry.
- **[ECP](https://ecp.gov.pk)** — asset declarations.
- **[PPRA](https://ppra.org.pk)** — tenders.
- **[Supreme Court of Pakistan](https://supremecourt.gov.pk)** — case search.
- **Customs WeBOC** — `weboc.gov.pk`.

**International registries and leaks.**

- **[OpenCorporates](https://opencorporates.com)**
- **[OCCRP Aleph](https://aleph.occrp.org)**
- **[ICIJ Offshore Leaks](https://offshoreleaks.icij.org)**
- **[OFAC SDN list](https://ofac.treasury.gov/sanctions-list-service)**
- **[UK HMT consolidated list](https://www.gov.uk/government/organisations/office-of-financial-sanctions-implementation)**
- **[UN consolidated list](https://scsanctions.un.org)**
- **[HaveIBeenPwned](https://haveibeenpwned.com)**
- **[Wayback Machine](https://web.archive.org)**
- **[Censys](https://search.censys.io)**
- **[Shodan](https://shodan.io)**
- **[crt.sh](https://crt.sh)**

**Geospatial.**

- **[Google Earth Pro](https://earth.google.com)**
- **[Sentinel Hub EO Browser](https://apps.sentinel-hub.com/eo-browser)**
- **[OpenStreetMap](https://openstreetmap.org)** + **[Overpass Turbo](https://overpass-turbo.eu)**
- **[SunCalc](https://www.suncalc.org)**
- **[FlightRadar24](https://flightradar24.com)** / **[ADS-B Exchange](https://www.adsbexchange.com)**
- **[MarineTraffic](https://marinetraffic.com)** / **[VesselFinder](https://vesselfinder.com)**

**Legal and policy citations used in this lecture.**

- National Accountability Ordinance 1999 (especially §§9, 14, 23, 27).
- Anti-Money Laundering Act 2010 (especially §§3, 7, 8).
- Prevention of Electronic Crimes Act 2016 (especially §§3, 13, 29, 32).
- Qanun-e-Shahadat Order 1984 (especially Articles 2(1)(e), 73, 164).
- FATF Recommendations 24, 25, 40 (beneficial ownership, transparency, international cooperation).
- Egmont Group Operational Standards (FIU information exchange).

---

<a id="glossary"></a>

# Annex A — Glossary

- **Admiralty Code** — 6×6 grid for grading source reliability and information credibility.
- **AIS** — Automatic Identification System; vessel tracking.
- **AMLA** — Anti-Money Laundering Act 2010 (Pakistan).
- **AMR** — Alphabetic Ministry Reference (administrative code; not directly used in OSINT).
- **B2** — Admiralty grade: usually-reliable source, probably-true information.
- **BO** — Beneficial Owner; the natural person who ultimately owns or controls a legal entity.
- **CDR** — Call Detail Record.
- **CT** — Certificate Transparency.
- **CIS** — Commonwealth of Independent States (Russian-language indexing relevant via Yandex).
- **DLD** — Dubai Land Department.
- **ECP** — Election Commission of Pakistan.
- **F3EAD** — Find, Fix, Finish, Exploit, Analyse, Disseminate. Military intel cycle variant.
- **FATF** — Financial Action Task Force.
- **FBIS** — Foreign Broadcast Information Service (US, 1941–2005).
- **FBR** — Federal Board of Revenue (Pakistan).
- **FIU** — Financial Intelligence Unit; Pakistan's is FMU.
- **FMU** — Financial Monitoring Unit (Pakistan FIU).
- **GEOINT** — Geospatial Intelligence.
- **HUMINT** — Human Intelligence.
- **ICIJ** — International Consortium of Investigative Journalists.
- **IMEI** — International Mobile Equipment Identity (handset).
- **IMINT** — Imagery Intelligence.
- **IMSI** — International Mobile Subscriber Identity (SIM).
- **INTs** — Intelligence disciplines (HUMINT, SIGINT, OSINT, …).
- **IPDR** — Internet Protocol Detail Record.
- **LAC** — Location Area Code (cell tower).
- **MASINT** — Measurement and Signature Intelligence.
- **MLAT** — Mutual Legal Assistance Treaty.
- **MOC / MTC** — Mobile Originating Call / Mobile Terminating Call.
- **MSISDN** — Mobile Subscriber ISDN Number (i.e. the phone number in E.164).
- **NAB** — National Accountability Bureau (Pakistan).
- **NACTA** — National Counter Terrorism Authority (Pakistan).
- **NAO** — National Accountability Ordinance 1999 (Pakistan).
- **NTN** — National Tax Number (Pakistan FBR).
- **OCCRP** — Organized Crime and Corruption Reporting Project.
- **OFAC** — Office of Foreign Assets Control (US Treasury).
- **OPSEC** — Operational Security.
- **OSINT** — Open-Source Intelligence.
- **PACA** — Pakistan Anti-Corruption Academy.
- **PEP** — Politically Exposed Person.
- **PECA** — Prevention of Electronic Crimes Act 2016 (Pakistan).
- **PIR** — Priority Intelligence Requirement.
- **PPRA** — Public Procurement Regulatory Authority (Pakistan).
- **RAT** — Radio Access Technology (e.g. 4G, 5G).
- **SAN** — Subject Alternative Name (TLS certificate).
- **SBP** — State Bank of Pakistan.
- **SDN** — Specially Designated Nationals (OFAC sanctions list).
- **SECP** — Securities and Exchange Commission of Pakistan.
- **SIGINT** — Signals Intelligence.
- **SOCMINT** — Social Media Intelligence.
- **STR** — Suspicious Transaction Report.
- **TBML** — Trade-Based Money Laundering.
- **UNODC** — United Nations Office on Drugs and Crime.
- **UWO** — Unexplained Wealth Order (UK; conceptually related to NAO §9).
- **VASP** — Virtual Asset Service Provider (FATF crypto terminology).
- **WHOIS** — Domain registration metadata service.

---

<a id="legal-refs"></a>

# Annex B — Pakistan legal references

- **National Accountability Ordinance 1999** — Sections 9 (offences), 14 (presumption against accused), 23 (powers of investigation), 27 (information collection from any source).
- **Anti-Money Laundering Act 2010 (as amended)** — Sections 3 (offence of money laundering), 7 (FMU powers and information access), 8 (predicate offences and STR).
- **Prevention of Electronic Crimes Act 2016** — Sections 3 (unauthorised access), 13 (use of stolen identity), 29 (data privacy), 32 (cyber-stalking).
- **Investigation for Fair Trial Act 2013** — basis for lawful intercept (separate regime from OSINT).
- **Investigation Act 2022** — federal investigation framework.
- **Qanun-e-Shahadat Order 1984** — Article 2(1)(e) (definition of "document"), Article 73 (documentary evidence), Article 164 (electronic evidence admissibility), Article 165 (electronic evidence integrity).

This document does not constitute legal advice. Investigators should rely on the prosecutor of record for case-specific legal guidance. The references above are provided to help the reader locate the relevant statutory framework.

---

<a id="urls"></a>

# Annex C — Useful URLs

**Pakistan portals**

- nab.gov.pk · fmu.gov.pk · secp.gov.pk · eservices.secp.gov.pk · fbr.gov.pk · e.fbr.gov.pk · ecp.gov.pk · ppra.org.pk · supremecourt.gov.pk · weboc.gov.pk

**International registries**

- opencorporates.com · aleph.occrp.org · offshoreleaks.icij.org · sayari.com · find-and-update.company-information.service.gov.uk

**Sanctions lists**

- ofac.treasury.gov/sanctions-list-service · gov.uk/government/organisations/office-of-financial-sanctions-implementation · scsanctions.un.org · eeas.europa.eu

**Search and discovery**

- crt.sh · search.censys.io · shodan.io · web.archive.org · haveibeenpwned.com · intelx.io

**Geospatial**

- earth.google.com · apps.sentinel-hub.com/eo-browser · openstreetmap.org · overpass-turbo.eu · suncalc.org · marinetraffic.com · vesselfinder.com · flightradar24.com · adsbexchange.com

**Crypto explorers**

- blockchain.com · etherscan.io · tronscan.org · bscscan.com · polygonscan.com · solscan.io · breadcrumbs.app · arkhamintelligence.com · chainabuse.com

**Tools**

- github.com/laramies/theHarvester · github.com/sherlock-project/sherlock · whatsmyname.app · spiderfoot.net · maltego.com · exiftool.org · hunch.ly · torproject.org · ahmia.fi

**Reference frameworks**

- osintframework.com · bellingcat.gitbook.io · inteltechniques.com/tools/ · aware-online.com

---

*This document was produced for the participants of the OSINT for ML / NAO Cases workshop, Pakistan Anti-Corruption Academy, NAB Headquarters Islamabad — 28 April 2026. It may be freely shared for educational purposes. Live demonstrations against any real subject must be pre-authorised, must follow NAO / AMLA / PECA boundaries, and must be logged in the case file. OSINT is corroboration, not conclusion.*

*Speaker: M. Aqib Bangash. Certified OSINT Master Trainer. CEO, Intelligence X One. CTO, Tech Net Group.*
