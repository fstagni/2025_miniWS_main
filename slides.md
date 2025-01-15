---
colorSchema: light
favicon: /public/images/diracx-logo-square.png
color: orange-light
layout: cover
routerMode: hash
title: Status of Dirac
theme: neversink 
neversink_string: "Dirac&Rucio mini-WS 2025"
---

# Status of Dirac

**Federico Stagni** <Email v="federico.stagni@cern.ch" />

January 16th 2025
__ <a href="https://indico.cern.ch/event/1443765" class="ns-c-iconlink"><mdi-open-in-new />Dirac & Rucio mini-workshop and hackathon</a>  


---
layout: section 
color: lime-light
---

<div style="display: flex; align-items: center; justify-content: center;">
    <img id="DIRAC" src="/public/images/DIRAC-logo-extended.png" alt="DIRAC logo" style="width: 300px;">
    <span style="margin: 0 50px;">--></span>
    <img id="DiracX" src="https://raw.githubusercontent.com/DIRACGrid/management/master/branding/diracx/svg/diracx-logo-full.svg" alt="DiracX" style="width: 300px;">
</div>


<!-- 
This is not the first time that we rewrite DIRAC, but this time it is more profound, and to enforce this we decided to slightly change the name, adding a "fashionable" X at the end, and using a slightly different color scheme for the logo
-->


---
layout: top-title-two-cols
color: gray-light
align: c-rt-lt
title: requirements
---

<StickyNote color="gray-light" textAlign="center" width="260px" title="Developers and maintainers requirements" v-drag="[350,300,320,100]">
Easy to test (will make it easier to code), but also modern, fun, and accessible to new developers
</StickyNote>

<StickyNote color="amber-light" textAlign="center" width="260px" title="Paramount requirement" v-drag="[365,420,290,70]">
We need to ensure business continuity
</StickyNote>



:: title ::

# Minimum Requirements

:: left ::

## Communities/Users requirements

Ease of use, including ease of access

Fast and responsive interfaces

Scalable and flexible

:: right ::

## Administrator requirements

Ease of installation and update

Up-to-date documentation

Clear confguration

Ready-to-use dashboards


<!--
I gave an extensive presentation at CHEP about the motivations, check that if you want

We decided that the best way of satisfying the requirements was to code a new Dirac
-->



---
layout: side-title
side: left
color: gray-light
titlewidth: is-5
align: rm-lm
title: DiracX
---

:: title ::

# What is DiracX?

:: content ::

- A cloud native app
- Multi-VO from the get-go
- Standards-based

<AdmonitionType type='important' >
Still Dirac, in terms of functionalities.
</AdmonitionType>


---
layout: side-title
color: gray-light
title: Architecture
align: cm-lm
titlewidth: is-3
---


:: title ::

# Architecture diagram

:: content ::

<img id="D_X" src="/public/images/architecture.png" class="mx-auto"> </img>


---
layout: top-title
color: gray-light
align: c
title: Versions
---

:: title ::

# Versions

:: content ::

```mermaid
%%{init: { 'logLevel': 'debug', 'theme': 'base', 'timeline': {'disableMulticolor': true}}}%%
timeline
    May 2022 : DIRAC v8.0
    Oct 2023 : EOL DIRAC v7.3
             : First DiracX demo
    Q1 2025  : DIRAC v9.0
             : DiracX v0.0.1
             : can start using DiracX services
```

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[20,211,148,240]">
Current production and only supported version, used by all DIRAC installations
</SpeechBubble>


<SpeechBubble position="l" color='amber' shape="round"  v-drag="[780,265,140,175]">
DIRAC v9 and DiracX 0.0.1 will be released together.
</SpeechBubble>

---
layout: top-title-two-cols
color: gray-light
align: c-lm-lm
title: DiracX v0.0.1
---

:: title ::

# Getting to **DiracX 0.0.1** -- [road map](https://github.com/DIRACGrid/diracx/blob/main/docs/ROADMAP.MD)

:: left ::

* First release contains:
    * All service/client underpinnings
    * Extension support
    * JobStateUpdateHandler can be replaced by DiracX

:: right ::

**To complete before declaring that is "ready"**

- [ ] Finish any DIRAC v9 cleanups
- [ ] Get LHCbDIRAC certification running stably with DIRAC v9
- [ ] Finish legacy adapter for JobStateUpdateClient
- [ ] Admin VO
- [ ] Ensure the helm chart is stable for updates
- [ ] Make sure the docs are complete

---
layout: top-title
color: gray-light
align: cm
title: Status
---

:: title ::

# Today's status

:: content ::

- All our development efforts are dedicated to creating DIRAC v9 and DiracX v0.1
- **We are finally not that far from releasing DIRAC v9.0 and DiracX v0.0.1**
- We would have loved to be faster (having it already in 2024), but... LHC (and LHCb)!
  - effectively, we are 1 year late on planned schedule

<!--
- In the previous 2 days we ran a DiracX hackathon where some of the effort was on moving the test instances of few DIRAC installations to DIRAC v9-preX and DiracX v0.1-preY
-->

---
layout: top-title
color: gray-light
align: cm
title: v9
---

:: title ::

# And which functionalities are in **DIRAC v9**?

:: content ::

- The concept of "Setup" is disappearing
- You will need OpenSearch (or ElasticSearch)
- Using DIRAC's RSS (Resource Status System) is mandatory
- DIRAC's ARC and ARC6 Computing Element are not supported anymore

&nbsp;
&nbsp;


Basically: no new functionalities, but many changes for DiracX. Lots of database schema changes.


---
layout: section
color: cyan-light
title: security
---

# Something about security

---
layout: top-title
color: gray-light
align: c
title: tokens
---

:: title ::

# What are proxies and/or tokens needed for?

:: content ::

## Internal to DIRAC and DiracX:

- For **Verifying a user's identity** (or a service identity)
  - **DIRAC** uses only X509 proxies and certificates to verify identities 
  - **DiracX** uses only tokens ([link to security model](https://github.com/DIRACGrid/diracx/blob/main/security_model.md))

---
layout: top-title-two-cols
color: gray-light
align: c-cm-cm
title: proxies+tokens
columns: is-2
---

:: title ::

# DIRAC&DiracX internal verification of users' identities

:: left :: 

DiracX: Authorization with "standard" <a href="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow" class="text-blue-600 hover:underline">Authorization Code Flow</a> redirecting to IdP

```mermaid {theme: 'forest', scale: 0.45}
%%{init: { 'theme': 'forest' }}%%
sequenceDiagram
    create actor U as User
    create participant DiracX
    U->>DiracX: Login
    DiracX->>U: Redirect
    create participant External_IdP
    U->>External_IdP: 
    destroy External_IdP
    External_IdP->>DiracX: ID token
    DiracX->>U: DiracX token
```

<AdmonitionType type='Note' >
DiracX mints its own tokens, which are not the same tokens used for the Grid endpoints
</AdmonitionType>


:: right ::

DIRAC+DiracX: working with proxies and tokens

```mermaid {theme: 'forest', scale: 0.40}
%%{init: { 'theme': 'forest' }}%%
sequenceDiagram
    create actor U as User
    create participant dirac-proxy-init
    U->>dirac-proxy-init: 
    create participant VOMS
    dirac-proxy-init->>VOMS: 
    destroy VOMS
    VOMS->>dirac-proxy-init: VOMS proxy
    create participant DIRAC
    dirac-proxy-init->>DIRAC: exchange proxy for token
    destroy DIRAC
    DIRAC->>dirac-proxy-init: DiracX token
    dirac-proxy-init->>U: proxy+token bundle
    U->>DIRAC_service: proxy
    U->>DiracX: token
```

<Line :x1=420 :y1=120 :x2=420 :y2=520 :width=1 />

---
layout: top-title
color: gray-light
align: c
title: tokens-3
---

:: title ::

# What are proxies and/or tokens needed for? /2

:: content ::

For **interacting with external resources**:

- **Submitting pilots**: The computing elements right now prefer the tokens
  - this is in DIRAC v8 since long time
- **Data access**: at least in WLCG, VOMS proxies. One day, will be token
  - discussions later today

---
layout: top-title
color: gray-light
align: c
title: tokens-3
---

:: title ::

# What are proxies and/or tokens needed for? /3

:: content ::

For **Identity (community membership)**: 

- **DIRAC** interfaces with VOMS and with OAuth2 Identity Providers
  - These are effectively hard dependencies since we are in the Grid world...
- **DiracX** interfaces with OAuth2 Identity Providers 

&nbsp;


Notes:
- **VOMS** is inside IAM now
 - See [this pres](https://indico.cern.ch/event/1341205/contributions/5972952/attachments/2881641/5048712/auth_now_then.pdf) for the DIRAC migration VOMS->IAM
- We tried IdPs: IAM, EGI Check-in
  - Check-in tokens (for compute) needed some discussions before becoming useful
  - VOMS -> Check-in synchronization?

---
layout: section
color: cyan-light
title: toV9
---

# From DIRAC v8 to v9+0.0.1

---
layout: top-title-two-cols
color: gray-light
align: c-lm-lm
title: Deployments
---

:: title :: 

# DiracX is deployed on Kubernetes

:: left ::

Kubernetes - <devicon-kubernetes class="text-3xl align-middle inline-block mx-0"></devicon-kubernetes> Standard to define a distributed system

<ul class="text-sm">
  <li>Separates infrastructure from applications
    <ul>
      <li class="text-xs">"Please IT department(/cloud provider) run this for me"</li>
    </ul>
  </li>
</ul>


Helm <devicon-helm class="text-3xl align-middle inline-block mx-0"></devicon-helm> gives the ability:

<ul class="text-sm">
  <li>to parameterise</li>
  <li>to distribute a kubernetes config</li>
</ul>

:: right ::

<ul class="text-sm">
  <li><a href="https://github.com/DIRACGrid/diracx-charts">DiracX Helm chart</a>
    <ul>
      <li>If your institution provides a kubernetes service: use it</li>
      <li>If you work with public clouds: use their container services</li>
      <li>Alternatively, follow these <a href="https://github.com/DIRACGrid/diracx-charts/tree/master/k3s">k3s instructions</a></li>
    </ul>
  </li>
  <li>Used for:
    <ul>
      <li>DiracX testing (GitHub actions)</li>
      <li>Local development instance</li>
      <li>Running a demo instance</li>
      <li>Running test and productions instances</li>
    </ul>
  </li>
</ul>


<StickyNote color="gray-light" textAlign="center" width="260px" title="What to run on K8" v-drag="[175,430,600,100]">
The helm charts provide "everything", inclusing MySQL and Opensearch. You are in no obligation to run all available services on K8
</StickyNote>



---
layout: top-title
color: gray-light
align: c
title: v9-migration
---

:: title ::

# What is in practice needed to migrate to v9?

:: content ::

Use this [skeleton](https://codimd.web.cern.ch/5C44tUJTReacVOcIn_0Bfg#), but first of all:

- You need an IdP (IAM...) -- you probably already have one instance!
  - Probably one for every VO you host (?)
- Register a DiracX `client` in the IdP, will be needed in order for DiracX (server) to authenticate
- if you have a VODIRAC extension:
  - update it considering the many changes.
  - code an "empty" `vodiracx` extension
- if you have a WebAppDIRAC extension:
  - code an "empty" `vodiracx-web` extension
- have a k8 project ready for hosting (vo)diracx
- deploy (vo)diracx 

---
layout: top-title
color: gray-light
align: c
title: FutureExtensions
---

:: title ::

# DiracX extensions

:: content ::

<span class="bg-cyan-100 text-cyan-600 text-center p-4 border-l-6 border-2 border-cyan-400 rounded-lg pl-8 pr-8 w-full block">
    By now, we know that it is sometimes necessary to extend all Dirac(X) components 
    
    DiracX aims to provide an easy way to do so.
</span>


```toml
# entrypoints in pyproject.toml

[project.entry-points."diracx.db.sql"]
AuthDB = "diracx.db.sql:AuthDB"
JobDB = "<extension>.db.sql:ExtendedJobDB"
```

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[400,310,220,140]">
For DiracX and DiracX-Web we already provide reference extensions
</SpeechBubble>


---
layout: top-title
color: gray-light
align: c
title: Migration
---

:: title ::

### Business continuity for DIRAC communities is our top priority
Services of DIRAC v9 and DiracX will need to live together for some time


:: content ::

<Arrow x1="300" y1="170" x2="370" y2="170" />
<Line :x1=345 :y1=200 :x2=345 :y2=500 :width=1 />

<Arrow x1="610" y1="170" x2="680" y2="170" />
<Line :x1=633 :y1=200 :x2=633 :y2=500 :width=1 />

<div style="display: flex; align-items: center; justify-content: center;">
    <img id="D_X" src="/public/images/legacy_before_Adaptor.png" class="mx-auto w-1/4"> </img>
    <img id="D_Ad" src="/public/images/legaxyAdaptor.png" class="mx-auto w-1/4"> </img>
    <img id="X" src="/public/images/legacy_after_Adaptor.png" class="mx-auto w-1/4"> </img>
</div>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[100,350,40,60]">
1
</SpeechBubble>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[370,350,40,60]">
2
</SpeechBubble>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[660,350,40,60]">
3
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[160,350,120,180]">
DIRAC and DiracX share the databases
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[430,350,160,180]">
A legacy adaptor moves traffic from DIRAC to DiracX services
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[720,350,120,140]">
DIRAC services can be removed
</SpeechBubble>

---
layout: section
color: cyan-light
title: Demos
---

# Demonstrations


---
layout: iframe-right
title: Web API
url: https://diracx-cert.app.cern.ch/api/docs
class: webAPI
slide_info: false
color: gray-light
align: lm
---

# DiracX Web API

<AdmonitionType type='caution' >
What is on the right is the certification Web API (VOs: `dteam` and `gridpp`), loaded live. Use with caution!
</AdmonitionType>

DIRAC Web APIs with <devicon-fastapi-wordmark class="text-7xl align-middle inline-block mx-0"></devicon-fastapi-wordmark>

<ul class="text-sm">
  <li>
    Nicely documented by 
    <devicon-swagger-wordmark class="text-7xl align-middle inline-block mx-0"></devicon-swagger-wordmark>
    <ul class="text-xs ml-4">
      <li class="text-xs">--> this is what you see on the right</li>
    </ul>
  </li>
  <li>
    Follows the <devicon-plain-openapi-wordmark class="text-7xl align-middle inline-block mx-1"></devicon-plain-openapi-wordmark> specification, with the (python) client generated by <a href="https://github.com/Azure/autorest/blob/main/docs/introduction.md">AutoREST</a>.
  </li>
</ul>


<!-- 
- there is also redoc
- AutoREST supports several langagues, not only python
-->


---
layout: top-title
color: gray-light
align: c
title: CLI
---

:: title ::

# CLI Interactions

:: content ::

1. Logging in (using the `diracx cli`):

```bash
❯ dirac login gridpp
Logging in with scopes: ['vo:gridpp']
Now go to: https://diracx-cert.app.cern.ch/api/auth/device?user_code=XYZXYZXYZ
...Saved credentials to /home/fstagni/.cache/diracx/credentials.json
Login successful!
```

2. Submitting a job (using Python `requests`):

```python
import requests

requests.post('https://diracx-cert.app.cern.ch/api/jobs/', headers={'accept': 'application/json', 'Authorization': 'Bearer eyJhbG...', 'Content-Type': 'application/json'}, json=jdl)
```

3. Getting its status (using `curl`):

````md magic-move
```bash
curl -X 'GET' \
  'https://diracx-cert.app.cern.ch/api/jobs/status?job_ids=8971' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJhbG...'  | jq
```
```json
{
  "8971": {
    "Status": "Done",
    "MinorStatus": "Execution Complete",
    "ApplicationStatus": "Unknown"
  }
}
```
````


---
layout: iframe-left
title: WebApp
url: https://diracx-cert.app.cern.ch
class: webapp
slide_info: false
color: gray-light
align: lm
---

# DiracX web

We are also rewriting [the Web App](https://github.com/DIRACGrid/diracx-web) from scratch.

Software stack:
- NextJS <devicon-nextjs-wordmark class="text-4xl align-middle inline-block mx-2" />
- Material UI <devicon-materialui class="text-3xl align-middle inline-block mx-2" />
- TypeScript <devicon-typescript class="text-3xl align-middle inline-block mx-2" />

<AdmonitionType type='caution' >
What is on the left is the certification WebApp, loaded live. Use with caution!
</AdmonitionType>

---
layout: section
color: cyan-light
title: Conclusions
---

# To conclude

---
layout: side-title
color: gray-light
title: Contribute
align: cm-lm
titlewidth: is-3
---

:: title ::

# *"I want to contribute"*

:: content ::

## The obvious ways:

<ul class="text-sm">
    <li>
        <a href="https://github.com/DIRACGrid/diracx" class="text-blue-600 hover:underline">code (github.com/DIRACGrid)</a>
    </li>
    <li>
        tests: (as you could see we have a somewhat open test deployment infrastructure). Try something out, and let us know!
    </li>
</ul>

**Run the demo (on your laptop):**

```sh
git clone https://github.com/DIRACGrid/diracx-charts
diracx-charts/run_demo.sh # this is run for each and every commit in Github Actions
```
 

## Discuss:
<ul class="text-sm">
  <li><strong>mattermost</strong>: <a href="https://mattermost.web.cern.ch/diracx/" class="text-blue-600 hover:underline">https://mattermost.web.cern.ch/diracx/</a></li>
  <li><strong>meetings</strong>: (almost) every week on Thursday morning (CET)</li>
  <li><strong>hackathons</strong>: we have been doing 2-days DiracX hackathons every quarter, at CERN
    <ul class="text-xs ml-4">
      <li>--> <a href="https://indico.cern.ch/event/1458873/" class="text-blue-600 hover:underline">Last one yesterday and the day before</a></li>
      <li>--> <a href="https://indico.cern.ch/event/1501369/" class="text-blue-600 hover:underline">Next will be 28 and 29 April -- you can register even now!</a></li>
    </ul>
  </li>
  <li><strong>workshops</strong>: once per year, more or less
    <ul class="text-xs ml-4">
      <li>--> <a href="https://indico.cern.ch/event/1433941/" class="text-blue-600 hover:underline">Next one in September 2025, in Beijing</a></li>
    </ul>
  </li>
</ul>



<!-- 
- You might have seen that we set up 2 VOs: **gridpp** and **dteam**. For **dteam** we do not import all members, but if you want to...
-->


---
layout: top-title
color: gray-light
align: c
title: FAQ
---

:: title :: 

Q/A

:: content ::

- I am using {Rucio|dask|another_tool}. I could use DiracX as WMS but do not want to fiddle with DIRAC

--> It will probably be possible, but we do not know when.

- What is in a DiracX token (is it "special")?

--> It carries the `dirac_properties` (which are the same as in current DIRAC)

- Where is the DiracX documentation?

--> only here for now: https://github.com/DIRACGrid/diracx/tree/main/docs


---
layout: top-title-two-cols
align: cm-cm-lm
color: orange-light
columns: is-4
title: summary
--- 
:: title ::

# Summary

:: left :: 

<img id="DiracX" src="https://raw.githubusercontent.com/DIRACGrid/management/master/branding/diracx/svg/diracx-logo-square.svg" class="mx-auto w-4/5"> </img>

:: right ::

<ul class="text-base">
  <li>DiracX is "the neXt Dirac incarnation", ensuring the future of the widely used Dirac
    <ul class="text-sm">
      <li>We are rewriting the code, but it is still Dirac that you love!</li>
    </ul>
  </li>
  <li>DiracX will ease the interoperability with Rucio and/or dask and/or any other tool out there
    <ul class="text-sm">
      <li>DiracX will still have the Data Management part, but its Workload Management functionalities will come first</li>
    </ul>
  </li>
  <li>The first DiracX release will soon be here
    <ul class="text-sm">
      <li>It will live together with DIRAC v9 for a while, until it will replace it completely</li>
    </ul>
  </li>
</ul>


---
layout: credits
color: navy
loop: true
speed: 1.0
title: credits/people
---


<div class="grid text-size-4 grid-cols-3 w-3/4 gap-y-10 auto-rows-min ml-auto mr-auto">
    <div class="grid-item text-center mr-0- col-span-3">
        <strong>People</strong><br> 
    </div>
    <div class="grid-item text-right mr-4 col-span-1">
        <strong>Current Developers, maintainers, supporters</strong>
    </div>
    <div class="grid-item col-span-2">
        Chris Burr <i>CERN, LHCb</i><br/>
        Christophe Haen <i>CERN, LHCb</i><br/>
        Alexandre Boyer <i>CERN, LHCb</i><br/>
        Natthan Piggoux <i>LUPM (FR), CTA</i><br/>
        Cedric Serfon <i>Brookhaven National Laboratory (US), Belle2</i><br/>
        Ryunosuke O'Neil <i>CERN, LHCb</i><br/>
        Daniela Bauer <i>Imperial college (UK), GridPP</i><br/>
        Simon Fayer <i>Imperial college (UK), GridPP</i><br/>
        Janusz Martyniak <i>Imperial college (UK), GridPP</i><br/>
        Xiaomei Zhang <i>Beijing, Inst. High Energy Phys. (CN), Juno</i><br/>
        Luisa Arrabito <i>LUPM (FR), CTA</i><br/>
        André Sailer <i>CERN</i><br/>
        Jorge Lisa Laborda <i>Univ. of Valencia and CSIC (ES), LHCb</i><br/>
        Bertrand Rigaud <i>IN2P3 (FR)</i>
    </div>
    <div class="grid-item text-right mr-4 col-span-1">
        <strong>Project lead</strong>
    </div>
    <div class="grid-item col-span-2">
        Federico Stagni <i>CERN, LHCb</i><br/>
        Andrei Tsaregorotsev <i>CPPM (FR), EGI and LHCb</i>
    </div>
</div>

&nbsp;
&nbsp;
&nbsp;

<div class="grid-item col-span-3 text-center mt-180px mb-auto font-size-1.5rem">
    <strong>Questions?</strong>
</div>

---
layout: section
color: cyan-light
title: Backup
---

# Backup

---
layout: top-title
color: gray-light
align: c
title: CVMFS
---

:: title :: 

# CVMFS: consolidation and organization

:: content ::

NB: DIRAC pilots do not depend on CVMFS, but its presence is of great help

- `/cvmfs/dirac.egi.eu` is the CVMFS repo for Dirac-related business
  - Managed at RAL (stability seems better...?)
  - DIRAC ready-to-source releases are added here by the CI when created
  - DIRAC pilot code
- `/cvmfs/grid.cern.ch` is the default repo used for CAs and CRLs, voms-related
pointers
  - De-facto source of truth for security files
  - `vomsdir` and `vomses` can be added here for any VO
- Pilots use it for quickly setting up the releases
  - Extensions can define a different (list of) CVMFS location(s) in `cvmfs_locations`, but
the CVMFS structure should be the same
