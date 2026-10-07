# VisionWatch AI — Video Surveillance Intelligence Platform

**VisionWatch AI** is an enterprise-grade visual surveillance intelligence and video analytics platform that converts hours of raw CCTV and security footage into structured, searchable, timestamped visual intelligence using multimodal Gemini models and temporal vision analysis.

---

## Guiding Principle: Direct Observation Over Speculation
The platform operates on the forensic principle of **Direct Observation Over Speculation**:
- **Layer 1: Direct Observations** — Measurable physical facts (speed, trajectory, dwell time, posture, entry/exit vectors). Zero speculation about human intent, emotions, or legal guilt.
- **Layer 2: Detected Anomalies** — Configurable rule deviations (sudden velocity variance, loitering past benchmark limits, off-hours perimeter ingress, clustering).
- **Layer 3: System Recommendations** — Operator action items (credential log audits, magnetic latch inspection, camera repositioning, automated surveillance reports).

---

## Core Capabilities

1. **Resilient Video Ingestion & HTML5 Processing**
   - Chunked/multipart uploads up to 200MB (MP4, WebM, MOV, AVI)
   - Synchronized storage in Supabase Storage (`cctv-videos` bucket)
   - Local hardware-accelerated playback with live HUD and scrub console
   - Pollable background pipeline: `uploaded` → `queued` → `extracting_metadata` → `analyzing_frames` → `generating_timeline` → `completed`
2. **Synchronized Bidirectional Timeline**
   - Scrubbing the video updates the timeline playhead in real time
   - Clicking any event instantly scrubs the video (`currentTime = targetTime`)
   - Severity-coded markers: Low (blue), Medium (amber), High (rose), Critical (purple)
   - Loop clip region toggle for instant continuous segment looping
3. **People Tracking & Occupancy Analytics**
   - Unique identity allocation (`Person 1`, `Person 2`, ...)
   - Ingress/egress zones, dwell duration, and visual attire description
   - Continuous Recharts area curve plotting crowd density over time
   - Activity distribution donut chart
4. **Natural Language Semantic Search**
   - Search queries like *"Show someone running"* or *"lingering near rear exit"*
   - Instant jump-points and highlighted event cards
5. **Grounded "Ask AI" Co-Pilot**
   - In-context multimodal assistant powered by Gemini
   - Cites every observation with clickable `[MM:SS]` timestamp badges
6. **Multi-Tier Alert Dispatch Center**
   - Severity triage view (`Critical`, `High`, `Medium`, `Low`)
   - Status actions: `Acknowledge`, `Dismiss`, `Escalate` with resolution notes
   - Event inspect drawer with physical evidence and contextual reasoning
7. **Automated Executive Surveillance Synthesis Report**
   - Comprehensive post-audit report generator
   - Client-side PDF download (`jspdf` + `html2canvas`)
   - Structured JSON export and Markdown copy
8. **Offline Demo Workspace**
   - Preloaded with realistic CCTV datasets (`Main Transit Concourse Cam 04`, `Server Vault Corridor`)
   - Zero immediate upload or API configuration needed for evaluation

---

## System Architecture

```
visionwatch-ai/
├── client/                     # React 18 + Vite + TypeScript + Tailwind CSS
│   ├── src/
│   │   ├── api/client.ts       # REST client for backend communication
│   │   ├── components/         # Modular tactical UI components
│   │   │   ├── alerts/         # AlertInbox triage table & inspection modal
│   │   │   ├── analytics/      # OccupancyChart & ActivityDistributionChart
│   │   │   ├── copilot/        # AskAiPanel with [MM:SS] clickable seek badges
│   │   │   ├── layout/         # AppHeader & SidebarNav
│   │   │   ├── report/         # ReportView with PDF/JSON export
│   │   │   ├── search/         # SemanticVideoSearch engine
│   │   │   ├── timeline/       # InteractiveTimeline & TimelineEventCard
│   │   │   ├── tracking/       # PersonTrackList with trajectory summaries
│   │   │   ├── upload/         # VideoDropzone with progress bar
│   │   │   └── video/          # VideoPlayer & PlaybackScrubber
│   │   ├── context/            # AuthContext & VideoPlaybackContext
│   │   ├── pages/              # 12 Route pages matching specification
│   │   └── utils/              # Time formatters and severity tokens
│
├── server/                     # Node.js + Express + TypeScript
│   ├── src/
│   │   ├── config/             # Supabase & Gemini SDK configurations
│   │   ├── controllers/        # VideoController, AnalysisController, CopilotController, AlertController
│   │   ├── middleware/         # Auth, RateLimiter, UploadMiddleware
│   │   ├── routes/             # videoRoutes, alertRoutes
│   │   ├── services/           # GeminiService, FFmpegService, StoreService, DemoService
│   │   ├── schemas/            # Zod validation schemas
│   │   └── server.ts           # Express entry point
│
└── shared/
    └── types/                  # Shared Zod schemas & TypeScript contracts
```

---

## Getting Started

### 1. Prerequisites
- Node.js v20+ LTS

### 2. Running Backend (Port 5000)
```powershell
cd server
npm run dev
```

### 3. Running Frontend (Port 3000)
```powershell
cd client
npm run dev
```

Visit **`http://localhost:3000`** in your browser.
