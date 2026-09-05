# Hi, I'm Garvit 👋

**AI Product & Program Manager | Kellogg MBA | I build the quality and evaluation layer that makes AI products work in production**

Most AI products don't fail because the model is bad. They fail because nobody built the layer underneath — the error taxonomy, the human feedback loop, the audit trail, the operating discipline that catches a confident wrong answer before a customer sees it.

That layer is what I've spent the last three years building. Before that, nearly nine years shipping education and AI products across content, operations, and platform teams at scale.

📍 Evanston, IL → open to US-based Technical Program Manager, Technical Product Manager, Product Operations, and Strategy & Operations roles.

---

## 🎯 What I Work On

- AI products where reliability, safety, and human oversight are the hard part
- Human-in-the-loop quality systems — error taxonomies, audit logic, engineering feedback loops
- LLM evaluation: scoring rubrics, calibration, and knowing when a score is not trustworthy
- Cross-functional delivery across engineering, data, customer success, and operations
- Product operations at scale — onboarding, SOPs, OKRs, incident and escalation design
- Regulatory and compliance workstreams in AI-in-hiring contexts

---

## 🏆 Selected Highlights

- **Built and led a 40-person human-in-the-loop quality and monitoring function** at ConverzAI (Series A voice-AI for US staffing), covering OKRs, error taxonomies, and audit logic — supporting 10x client growth.
- **Diagnosed a healthcare recruiting failure mode through recruiter and candidate research**, then launched an ATS-integrated, text-first screening workflow: +30% candidate engagement, contributing to 20% revenue growth.
- **Ran the product response to a new FCC regulation** that threatened operations in a high-growth vertical — cohort experiments to reconfigure the product rather than exit the market.
- **Scaled a synchronous learning platform to 20M+ users during COVID** at BYJU'S, contributing to roughly $200M in year-one revenue.
- **Rebuilt a content operating model** across 10M+ textbook questions: −83% cost, −66% turnaround time, 3x throughput, conversion from 3% to 7%.
- **Managed the Disney–BYJU'S content delivery program** across 20+ international studios — 200+ hours of 3D media, launch accelerated by 90 days.
- **Kellogg 1Y MBA**, June 2026 — Dean's List (4.0/4.0), Dean's Distinguished Service Award, GMAT Focus 755 (100th percentile).

---

## 🧩 Featured Projects

### 📊 [Job Signal Board](https://github.com/a-garvit/job-signal-board-public)
**An LLM evaluation pipeline disguised as a job search tool.**

A judge-first job discovery and screening system. It scans ~200 company career boards plus a licensed LinkedIn feed, strips out only hard disqualifiers, then has Claude score every surviving posting 0–100 against a written candidate profile and promotes anything above the threshold into a working tracker — with a one-sentence rationale attached to every decision.

The interesting part isn't the scraping. It's the design principle:

> **Nothing is filtered on keywords. Judgement is the filter.**

The first version had a title whitelist built from my own prior job titles. It was silently discarding Chief of Staff, Business Lead, GTM Manager, Corporate Development — the entire class of roles an MBA is actually for. The filter was screening for *resemblance to my past*, which is exactly backwards for a career pivot.

**What it does**
- 8 hand-built company adapters + 3 bulk ATS scanners across 200+ seeded boards (Ashby, Greenhouse, Lever)
- Every ingestion path routes through one Queue → judge → promote pipeline; nothing writes to the tracker unjudged
- Runs unattended on daily triggers, re-judges the top 20 on full uncapped job descriptions, and emails a digest flagging any score that dropped by 15 or more
- Web dashboard for scanning, manual ingestion, application tracking, and networking
- Built on Google Apps Script and Sheets — a platform with a hard six-minute execution ceiling, which forced most of the interesting engineering

**What I measured, and what I learned**
- Two rows carrying **byte-identical** job descriptions score the same under fixed batch order and **3.7 points apart when shuffled**. Identical text, so nothing about the posting explains the gap — it isolates the effect of a job's batch neighbours alone. That, not temperature, is where the scoring noise lives.
- The HTML stripper was deleting `&ndash;` before the judge ever saw the text, so a model quoting a salary range faithfully produced a span that appeared nowhere in the input, and the verbatim gate recorded the rejection **against the model**. Quote accuracy went from 84–94% to 24 of 24 once the two code paths were unified. The general lesson: a validator that can be wrong will blame the thing it validates.
- I wrote an operating contract for the AI coding agent building this — read before you write, numbered regression invariants each naming the failure that produced it, and a rule that uncertainty about an external API is resolved by running a diagnostic, never by generating code against an inferred schema. Four of those rules say plainly that the originating failure wasn't recorded, rather than supplying a plausible one.

**Limitations stated in the repo, not discovered by the reader:** no labelled ground truth, so this measures reproducibility rather than accuracy. The promotion threshold is a judgment call, not an optimised parameter. The shuffled-order spread got *worse* between measurements and the recorded explanation is plausible but unproven. It's a single-user personal tool with no auth and no tests, and the architecture says so.

🔗 [Source and full write-up](https://github.com/a-garvit/job-signal-board-public)

---

### 🧠 MindMate AI
**A mental health companion for the moments between breakdown and support.**

Full product definition — MRD, PRD, personas, key paths, MVC architecture, metrics, unit economics, and a 12-week scrum plan — built for Kellogg's Product Management course.

MindMate is positioned as a daily emotional companion for high-stress micro-moments, not a therapist and not a meditation app. The core insight from user interviews: people abandon wellness tools at exactly the moment they need them, because those tools assume emotional readiness the user doesn't have. Journaling needs articulation. Meditation needs bandwidth. Therapy needs a calendar.

**What I defined**
- Three personas grounded in interview synthesis, converging on one pattern: emotional overwhelm arrives in short windows when support is least available and least usable
- Five unmet needs written as **testable hypotheses with stated validation methods** — not assertions
- Six key path scenarios including a safety and escalation flow, because in this category the trust path is a core path, not an edge case
- MVC information architecture with the model layer decoupled from UI, so therapist integration or employer dashboards can be added later without a rewrite
- Metrics with exact event-based definitions — activation, time-to-first-value, D7/D30 retention, helpfulness, and safety escalation rate, which is explicitly *not* a lower-is-better metric
- Unit economics: $12/mo subscription, $1.50–$4.50 variable cost, contribution margin $7.50–$10.50, sub-3-month target payback
- Directional TAM/SAM/SOM with transparent assumptions and a written section on why growth will be slow, cohort-driven, and retention-led rather than explosive

Built as a single self-contained page with a **local-first, bring-your-own-key architecture** — the user supplies their own OpenAI key, it stays in browser storage, and check-ins and journal entries never leave the device. That diverges from the PRD, which specified a native app with a HIPAA-aligned cloud backend. For a prototype whose premise is that someone will trust it with what they wouldn't tell a friend, holding nothing is the faster way to earn that trust.

🔗 [Source and write-up](https://github.com/a-garvit/mindmate-ai) · [Live prototype](https://melodic-bubblegum-224343.netlify.app) · [12-week scrum board](https://a-garvit.github.io/Mindmate-Scrum-Board/)

---

### ⚽ FIFA World Cup 2026 — Analytical Consulting Lab
**Forecasting demand for an event with no historical ground truth.**

Worked on a five-person Kellogg Analytical Consulting Lab team supporting food-and-beverage demand and revenue planning across US stadium contexts for FIFA World Cup 2026.

The analytical challenge wasn't maximizing in-sample accuracy. It was selecting a *useful, interpretable* approach that could generalize from an imperfect proxy dataset and actually support operating decisions. We evaluated multiple modeling approaches and deliberately chose a fit-for-purpose architecture to limit overfitting risk on limited, high-variance data — the harder call was rejecting the more sophisticated option.

Delivered a multi-stage forecasting model, an interactive self-serve planning tool for stadium- and match-level scenarios, and a product-bundling strategy for cross-sell and concession revenue planning.

FIFA's analytics team requested the working model after the engagement for potential internal use.

*Engagement details are governed by an NDA; specifics are limited accordingly.*

---

## 🚀 Building Things Before It Was a Job Title

A long pattern of finding an unmet need, building something practical with almost no resources, and improving how it runs.

**At Manipal** — launched a student-focused digital publication in the visual-listicle format, built and published shareable visual stories end to end (concept, headline, curation, sequencing, captions, publishing), and helped establish an early video-journalism community on campus. No budget, no editorial structure, all of it learned by shipping and watching what people actually read.

**E-commerce operations** — supported an early-stage dropshipping venture across operations, customer service, and catalog management. Identified consistently high-selling SKUs and helped shift those products from pure dropshipping to a hybrid stocked model, cutting delivery time for selected SKUs from 30–40 days to 4–5. The lesson stuck: a low-capital model is fine until demand becomes predictable and customer experience becomes the constraint — then the operating design has to change.

**Service business operations** — coordinated client and contractor communication for a residential and commercial painting business, running in-project and post-completion follow-ups. Proactive communication and post-completion follow-through aren't administrative extras in a service business; they *are* the product.

---

## 💼 Career Background

**ConverzAI** — Product Operations Manager, founding member of the product team (2023–2025)
Series A US startup building AI voice recruiters for the staffing industry. Built the 40-person human-in-the-loop quality and monitoring function from scratch. Owned PRDs, user stories, sprints, UAT, releases, and incidents alongside 40 engineers and 6 data professionals. Designed controlled experiments across call-first and text-first candidate journeys, analyzing 100K+ interactions through funnel analysis. Led ATS integration specifications, product-line expansion into light industrial and healthcare, and the compliance response to new FCC regulation.

**BYJU'S** — Product Manager → Associate PM → Assistant PM → Associate, Product Development (2016–2023)
Nearly seven years across content, platform, and growth products at 20M+ user scale. Scaled a synchronous live-learning platform during COVID. Ran the Disney–BYJU'S delivery program across 20+ studios. Rebuilt a content operating model spanning 10M+ questions. Redesigned an underperforming B2B classroom product after direct school visits, lifting partner-school adoption 60%. Recipient of the Eureka Award for distinguished excellence.

**Kellogg School of Management** — MBA, June 2026 (One-Year Accelerated)
Strategy, Economics, Marketing, with a focus on AI & Analytics. VP – 1Y Kellogg Student Association and India Business Conference. Director – KelloggCares and KelloggPaws.

**Manipal Institute of Technology** — B.Tech, Automobile Engineering. Top 5% of class.

---

## 💡 My Product Strengths

**Quality and evaluation systems for AI**
I've built the function that catches what the model gets wrong — error taxonomies, audit logic, sampling design, and the feedback loop back into engineering. I know what an unauditable confident score costs, because I've paid for it.

**Diagnosis before building**
Recruiter interviews before a workflow redesign. School visits before a B2B product redesign. User interviews before a PRD. The pattern is consistent and it's the part most people skip.

**Operating at scale with cross-functional teams**
Engineers, data scientists, designers, customer success, vendors, quality teams, and frontline operators — across the US, India, and the Middle East, on products serving millions.

**Measurement discipline**
I distinguish what was measured from what was asserted, and I write down which is which. When there's no ground truth, I say so instead of inventing a number.

**Directing AI-assisted development**
I'm not a software engineer. I've shipped a 7,500-line system by specifying it precisely, defining invariants, reviewing adversarially, and refusing to accept a confident answer that's actually a guess — which is the same discipline as directing an engineering team.

---

## 🛠️ Tools and Capabilities

**Product**
Product discovery · User research · PRDs and user stories · Roadmapping · Prioritization · Agile/Scrum · Sprint and release management · UAT · Incident and escalation design · Go-to-market

**AI and Data**
LLM evaluation and scoring rubrics · Prompt design · Human-in-the-loop quality systems · A/B testing and controlled experiments · Funnel and cohort analysis · Statistical sampling · SQL · R / RStudio · AI-assisted development (Claude Code, Lovable)

**Systems and Delivery**
API and ATS integrations · Google Apps Script · Workflow automation (n8n, Zapier) · Jira · Confluence · Notion · Figma · Git

---

## 🌍 Beyond Product

I'm happiest building something with my hands or moving fast enough that
thinking gets out of the way.

**Things I build.** LEGO, mostly — I like anything where a thousand small
parts have to be right for the whole to work. Same reason I cook: a recipe
is a spec, and improvising against it is more fun once you know why each
step is there.

**Things that move.** Go-karting for the split-second decisions, sailing
for the opposite — reading wind and current and committing to a line
before you can see whether it was right. I follow Formula 1 obsessively
and made it to Silverstone for an experience day.

**Badminton**, seriously enough to play at state level in Maharashtra
(under-16, District Thane). Still swim. Still lose to people half my age
at both.

**Manchester United**, logo tattooed on my arm, which I did before knowing
how the next decade would go. Old Trafford was the first stop on my first
trip to the UK, and worth every minute of the pilgrimage.

**Animals.** I moderate a Bangalore canine-feline group that keeps an
emergency blood-transfusion database for pets and interviews prospective
adopters. It's the least glamorous volunteering I've done and the one I'd
give up last.

**Also:** mentoring GMAT aspirants, collecting stamps in the passport, and
a mental well-being club I started at BYJU'S during COVID that grew to
800 members — which taught me more about product-market fit than any
course did.

---

## 📫 Connect

[LinkedIn](https://www.linkedin.com/in/garvitagrawal22/) · garvit.agrawal@kellogg.northwestern.edu

---

<sub>Currently recruiting for US-based Technical Program Manager, Technical Product Manager, Product Operations, and Strategy & Operations roles. Open to conversations.</sub>
