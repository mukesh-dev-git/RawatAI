<div align="center">

<img src="https://capsule-render.vercel.app/api?type=shark&color=0:0B3D91,100:E11D48&height=200&section=header&text=RawatAI&fontSize=58&fontColor=ffffff&animation=blinking&fontAlignY=36&desc=Malaysia%20Public%20Healthcare%20Agentic%20AI&descAlignY=58&descSize=18" width="100%" alt="RawatAI banner"/>

<a href="#screenshots"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&pause=1200&color=60A5FA&center=true&vCenter=true&width=760&lines=Describe+symptoms+%C2%B7+get+the+right+hospital;4+AI+agents%3A+vision+%C2%B7+triage+%C2%B7+routing+%C2%B7+assignment;3%2C304+MoH+facilities+with+live+bed+utilisation;English+and+Bahasa+Malaysia+%C2%B7+voice+input" alt="Typing summary"/></a>

<br/>

[![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-4-06B6D4?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
<br/>
[![Groq](https://img.shields.io/badge/LLM-Groq%20gpt--oss--20b-F55036)](https://groq.com)
[![Leaflet](https://img.shields.io/badge/Maps-Leaflet-199900?logo=leaflet&logoColor=white)](https://leafletjs.com)
[![Hackathon](https://img.shields.io/badge/Adaptive%20Malaysia%20Hackathon-2026-E11D48)](#project-overview)

</div>

---

## <img src="https://api.iconify.design/lucide/target.svg?color=%230B3D91" width="26" align="top" alt=""/> Project Overview

RawatAI is an AI patient triage and hospital routing system for Malaysian public healthcare, built for the **Adaptive Malaysia Hackathon 2026**. A patient types or speaks their symptoms, optionally uploads a photo, and a pipeline of four AI agents works out how urgent the case is, what it might be, where to go and who to see, with no human in the loop.

### Key Features

- <img src="https://api.iconify.design/lucide/siren.svg?color=%23E11D48" width="18" align="top" alt=""/> **Urgency triage**: every case is classed P1 (emergency), P2 (urgent) or P3 (non-urgent), with the reasoning shown.
- <img src="https://api.iconify.design/lucide/stethoscope.svg?color=%238B5CF6" width="18" align="top" alt=""/> **Condition prediction**: the likely condition, the matching department and the key symptoms.
- <img src="https://api.iconify.design/lucide/map-pin.svg?color=%230EA5E9" width="18" align="top" alt=""/> **Nearest suitable facility**: ranks 3,304 Ministry of Health facilities by distance and bed utilisation, and reroutes if the top hospital is at critical capacity.
- <img src="https://api.iconify.design/lucide/user-check.svg?color=%2310B981" width="18" align="top" alt=""/> **Specialist assignment**: matches a doctor from a virtual pool of 16 across 9 specialties, with one-tap call and appointment booking.
- <img src="https://api.iconify.design/lucide/mic.svg?color=%23F59E0B" width="18" align="top" alt=""/> **Voice and language**: speak symptoms with the Web Speech API, and switch the whole flow between English and Bahasa Malaysia.
- <img src="https://api.iconify.design/lucide/history.svg?color=%2364748B" width="18" align="top" alt=""/> **Medical history as context**: chronic conditions and medications are fed into the triage prompt.

## <img src="https://api.iconify.design/lucide/image.svg?color=%230B3D91" width="26" align="top" alt=""/> Screenshots

All screenshots are from a local run with the demo patient account.

**Landing page**

![Landing page](docs/screenshots/landing.png)

**Patient dashboard**

![Patient dashboard](docs/screenshots/dashboard.png)

**Step 1: choose or type symptoms**

![Symptom selection](docs/screenshots/triage-symptoms.png)

**Step 2: AI follow-up questions**

![AI follow-up questions](docs/screenshots/triage-followup.png)

**Result: priority, predicted condition, specialist and nearest hospital**

![Triage result](docs/screenshots/triage-result.png)

**Medical history**

![Medical history](docs/screenshots/history.png)

## <img src="https://api.iconify.design/lucide/clipboard-list.svg?color=%230B3D91" width="26" align="top" alt=""/> Requirements

- Node.js 20 or newer
- A free [Groq API key](https://console.groq.com)

## <img src="https://api.iconify.design/lucide/zap.svg?color=%230B3D91" width="26" align="top" alt=""/> Quick Start

```bash
git clone https://github.com/mukesh-dev-git/RawatAI.git
cd RawatAI
npm install

# Add your Groq key
echo "GROQ_API_KEY=your_key_here" > .env.local

npm run dev
```

Open http://localhost:3000 and sign in with a demo patient (password `demo123`):

| Name | Phone | Conditions |
|---|---|---|
| Ahmad Razif | `0123456789` | Hypertension |
| Siti Nurhaliza | `0198765432` | Type 2 diabetes |

## <img src="https://api.iconify.design/lucide/network.svg?color=%230B3D91" width="26" align="top" alt=""/> How It Works

```mermaid
flowchart TD
    A[Patient input<br/>symptoms · optional photo · location] --> B[Agent 1: Vision<br/>reads the uploaded photo]
    B --> C[Agent 2: Triage<br/>P1 / P2 / P3, predicted condition, department]
    C --> D[Agent 3: Routing<br/>distance + bed utilisation, surge reroute]
    D --> E[Agent 4: Assignment<br/>matches a specialist]
    E --> F[Result<br/>priority · condition · specialist · hospital map · booking]

    classDef in fill:#F1EFE8,stroke:#888780,color:#222
    classDef ai fill:#EEEDFE,stroke:#7F77DD,color:#222
    classDef logic fill:#DBEAFE,stroke:#0B3D91,color:#222
    classDef out fill:#E11D48,stroke:#0B3D91,color:#fff
    class A in
    class B,C ai
    class D,E logic
    class F out
```

Triage rules add safeguards on top of the model, for example fever for more than two days is at least P2, and hypertension or diabetes with fever is at least P2.

## <img src="https://api.iconify.design/lucide/database.svg?color=%230B3D91" width="26" align="top" alt=""/> Data

Facility data comes from Ministry of Health Malaysia open data: 3,304 facilities with GPS coordinates, plus bed utilisation rates for 149 hospitals. The raw CSVs are in `datasets/`, and the app reads the pre-processed `lib/facilities.json`. A few source rows have impossible utilisation values (negative or above 100%), and routing treats those as unknown.

## <img src="https://api.iconify.design/lucide/folder-tree.svg?color=%230B3D91" width="26" align="top" alt=""/> Project Structure

```
RawatAI/
├── app/
│   ├── page.tsx               # landing page
│   ├── login/
│   ├── patient/               # dashboard, triage, history
│   └── api/                   # questions, triage, vision, routing, assign, notify
├── lib/
│   ├── routing.ts             # haversine distance and facility scoring
│   ├── doctors.ts             # virtual specialist pool
│   ├── locations.ts           # 29 Malaysian cities
│   └── facilities.json        # processed MoH data
├── components/                # navigation, facility map
├── datasets/                  # source CSVs
└── docs/screenshots/
```

There is no database: cases are held in memory and reset when the server restarts.

## <img src="https://api.iconify.design/lucide/heart-handshake.svg?color=%230B3D91" width="26" align="top" alt=""/> Acknowledgments

- Ministry of Health Malaysia for the open facility and bed utilisation data
- The Adaptive Malaysia Hackathon 2026 organisers
- Built with Next.js, Groq and Leaflet

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:E11D48,100:0B3D91&height=110&section=footer&animation=twinkling" width="100%" alt=""/>

</div>
