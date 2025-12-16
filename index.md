---
layout: splash
title: Make Infrastructure Boring Again
---

<style>
:root {
  --bg: #0a0b0d;
  --text: #ffffffff;
  --muted: #a2a8b3;
  --accent: #f2c14e;
  --success: #3abf3a;
  --bottom-pad: 56px;
}

* { box-sizing: border-box; }

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: system-ui, -apple-system, sans-serif;
}

/* kill theme spacing */
.layout--splash .page__content,
.layout--splash .initial-content,
.layout--splash .page,
.layout--splash .page__inner-wrap {
  margin: 0;
  padding: 0;
  max-width: none;
}

/* ===== HERO ===== */

.hero {
  min-height: 100vh;
  position: relative;
}

.hero-grid {
  position: absolute;
  left: 0;
  right: 0;
  bottom: var(--bottom-pad);
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 28px;

  display: grid;
  grid-template-columns: 1.2fr 500px;
  grid-template-rows: auto auto;
  column-gap: 20px;
  row-gap: 32px;
  align-items: end;
}

/* ===== TASK LIST ===== */

.rolodex { width: 450px; }

.rolodex-window {
  --item-h: 44px;
  height: calc(var(--item-h) * 7);
  overflow: hidden;
  border: 1px solid rgba(255,255,255,0.08);
  padding-left: 12px;
  mask-image: linear-gradient(
    to bottom,
    rgba(0,0,0,0.25),
    rgba(0,0,0,1) 50%,
    rgba(0,0,0,0.25)
  );
}

.rolodex-track {
  transform: translateY(0);
  will-change: transform;
}

.roll-item {
  height: var(--item-h);
  display: flex;
  align-items: center;
  font-size: 1.15rem;
  white-space: nowrap;
  color: var(--text);
  transition: opacity 300ms ease-out, color 300ms ease-out;
  /* opacity: 0.35; */
}

/* symmetric brightness curve */
/* .roll-item.level-0 { opacity: 0.35; }
.roll-item.level-1 { opacity: 0.4; }
.roll-item.level-2 { opacity: 0.6; }*/

.roll-item.level-2:not(.completed) {
  opacity: 1;
  font-weight: bold;
  color : yellow;
}
/* completion */
.roll-item.completed { opacity: 0.70 !important; }

.roll-icon {
  width: 24px;
  height: 24px;
  margin-right: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(162,168,179,0.5);
  border-radius: 4px;
}

.roll-icon.checked {
  color: var(--success);
  border: none;
  font-size: 1.6em;
}

.roll-icon.checked::before { content: "✓"; }

/* ===== METRONOME ===== */

.hero-visual {
  display: flex;
  justify-content: flex-end;
}

.metronome {
  position: relative;
  width: 500px;
  height: 500px;
}

.metronome-body {
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 280px;
  height: 390px;
  border: 1px solid rgba(162,168,179,0.35);
  background: linear-gradient(
    to bottom,
    rgba(255,255,255,0.06),
    rgba(255,255,255,0.015)
  );
  clip-path: polygon(10% 100%, 90% 100%, 62% 0%, 38% 0%);
  transform: translateX(-50%);
}

.metronome-arm {
  position: absolute;
  left: 50%;
  bottom: 26px;
  width: 3px;
  height: 360px;
  background: rgba(245,247,250,0.85);
  transform-origin: bottom center;
  transform: translateX(-50%);
  will-change: transform;
}

/* ===== COPY ===== */

.hero-copy { grid-column: 1 / -1; }

h1 {
  font-size: clamp(4.5rem, 9vw, 7.5rem);
  line-height: 1.05;
  margin: 0;
}

.accent {
  color: var(--accent);
  opacity: 0;
  transition: opacity 1.2s ease-out 0.8s;
}

.accent.visible { opacity: 1; }

.subhead {
  margin: 18px 0;
  font-size: 1.25rem;
  color: var(--muted);
}
</style>

<section class="hero">
  <div class="hero-grid">

    <div class="rolodex">
      <div class="rolodex-window">
        <div class="rolodex-track"></div>
      </div>
    </div>

    <div class="hero-visual">
      <div class="metronome">
        <div class="metronome-body"></div>
        <div class="metronome-arm"></div>
      </div>
    </div>

    <div class="hero-copy">
      <h1>Make infrastructure boring. <span class="accent">On purpose.</span></h1>
      <p class="subhead">Calm production beats clever tooling.</p>
    </div>

  </div>
</section>

<script>
const arm = document.querySelector('.metronome-arm');
const track = document.querySelector('.rolodex-track');
const accent = document.querySelector('.accent');

const TASKS = [
  "",
  "",
  "",
  "Lock deployment window",
  "Verify change approval",
  "Confirm maintenance mode",
  "Disable external traffic",
  "Drain load balancers",
  "Freeze background jobs",
  "Snapshot databases",
  "Verify snapshot integrity",
  "Check disk capacity",

  // BoringOps injection
  "Confirm no engineers required",

  "Confirm rollback artifacts",
  "Validate config templates",
  "Sync configuration repo",
  "Verify environment variables",
  "Pull release artifacts",
  "Validate artifact checksums",
  "Stage release binaries",
  "Verify dependency versions",
  "Confirm runtime versions",

  // BoringOps injection
  "Confirm deploy proceeding on schedule",

  "Check feature flags state",
  "Disable nonessential alerts",
  "Notify on-call rotation",
  "Confirm pager silence",
  "Lock schema migrations",
  "Validate migration order",
  "Run preflight checks",
  "Confirm cluster health",
  "Check node availability",

  // BoringOps injection
  "Confirm on-call still sleeping",

  "Verify quorum status",
  "Confirm leader election",
  "Validate service discovery",
  "Check DNS propagation",
  "Verify TLS certificates",
  "Rotate expiring certificates",
  "Reload certificate stores",
  "Confirm cipher support",
  "Validate secrets access",

  // BoringOps injection
  "Confirm security posture unchanged",

  "Sync secrets store",
  "Confirm key permissions",
  "Check encryption status",
  "Validate backup schedules",
  "Pause scheduled jobs",
  "Confirm job suspension",
  "Disable autoscaling",
  "Lock scaling policies",
  "Verify resource quotas",

  // BoringOps injection
  "Confirm system operating with margin",

  "Check CPU headroom",
  "Check memory headroom",
  "Check IO thresholds",
  "Confirm network capacity",
  "Validate firewall rules",
  "Verify security groups",
  "Confirm ingress rules",
  "Validate egress rules",
  "Check rate limits",

  // BoringOps injection
  "Confirm no tuning required",

  "Confirm throttling config",
  "Stage database migrations",
  "Run migration dry run",
  "Verify migration output",
  "Apply schema migrations",
  "Confirm migration success",
  "Unlock schema changes",
  "Deploy application services",
  "Deploy background workers",

  // BoringOps injection
  "Confirm deploy remains boring",

  "Deploy scheduled tasks",
  "Verify service startup",
  "Confirm process health",
  "Check startup logs",
  "Validate log ingestion",
  "Confirm metrics emission",
  "Verify tracing enabled",
  "Check error rates",
  "Validate health endpoints",

  // BoringOps injection
  "Confirm metrics behaving normally",

  "Confirm readiness probes",
  "Confirm liveness probes",
  "Re-enable autoscaling",
  "Unlock scaling policies",
  "Gradually restore traffic",
  "Monitor latency",
  "Monitor error budgets",
  "Confirm SLO compliance",
  "Verify cache connectivity",

  // BoringOps injection
  "Confirm no manual intervention occurred",

  "Warm critical caches",
  "Confirm cache hit rates",
  "Re-enable background jobs",
  "Resume scheduled tasks",
  "Validate job execution",
  "Confirm queue depth",
  "Check message lag",
  "Verify consumer offsets",
  "Confirm idempotency guards",

  // BoringOps injection
  "Confirm reclaimed engineer capacity",

  "Validate retry policies",
  "Check circuit breakers",
  "Confirm fallback behavior",
  "Verify feature flags",
  "Enable new feature flags",
  "Confirm flag propagation",
  "Monitor flag impact",
  "Validate user flows",
  "Run smoke tests",

  // BoringOps injection
  "Confirm user experience unchanged",

  "Confirm API responses",
  "Validate authentication",
  "Confirm authorization paths",
  "Check session handling",
  "Verify token issuance",
  "Confirm token expiry",
  "Check audit logging",
  "Validate audit events",
  "Confirm compliance hooks",

  // BoringOps injection
  "Confirm compliance without escalation",

  "Re-enable external alerts",
  "Confirm alert routing",
  "Validate alert thresholds",
  "Test alert firing",
  "Confirm alert recovery",
  "Monitor system stability",
  "Monitor resource usage",
  "Verify no memory leaks",
  "Check file descriptor usage",

  // BoringOps injection
  "Confirm stability without heroics",

  "Confirm thread counts",
  "Verify connection pools",
  "Check database performance",
  "Validate query plans",
  "Confirm index usage",
  "Monitor replication lag",
  "Verify replica health",
  "Confirm failover readiness",
  "Test failover simulation",

  // BoringOps injection
  "Confirm failure paths unused",

  "Restore normal traffic",
  "Confirm traffic balance",
  "Monitor geographic regions",
  "Validate regional health",
  "Confirm CDN behavior",
  "Verify cache invalidation",
  "Check edge propagation",
  "Validate client compatibility",
  "Confirm backward compatibility",

  // BoringOps injection
  "Confirm change now invisible",

  "Verify API versioning",
  "Check deprecation warnings",
  "Confirm no regressions",
  "Review deployment logs",
  "Archive deployment logs",
  "Tag release version",
  "Update release registry",
  "Confirm version reporting",
  "Verify build metadata",

  // BoringOps injection
  "Confirm deploy did not require explanation",

  "Update runbook notes",
  "Record deployment outcome",
  "Notify stakeholders",
  "Confirm business metrics",
  "Validate revenue paths",
  "Confirm billing integrity",
  "Verify payment processing",
  "Check webhook delivery",
  "Confirm integration health",

  // BoringOps injection
  "Confirm operational calm preserved",

  "Validate third-party deps",
  "Monitor partner endpoints",
  "Confirm SLA compliance",
  "Verify uptime metrics",
  "Check error budgets",
  "Confirm incident-free window",
  "Release maintenance mode",
  "Unlock deployment window",
  "Close deployment ticket",
  "Enjoy another Boring deployment"
];



const itemHeight = 44;
const visibleItems = 7;
const activeIndex = 3;
const transitionDuration = 300;

const period = 3000;
const maxAngle = 20;
const peakThreshold = maxAngle - 0.1;

let taskIndex = 0;
let hasTicked = false;
let listDone = false;
let start = performance.now();

// --- START: MODIFIED CODE ---

// Fade in "on purpose" after 7 seconds
setTimeout(() => {
  accent.classList.add('visible');
}, 4500);

// The CSS already handles the transition:
// .accent {
//   opacity: 0;
//   transition: opacity 1.2s ease-out 0.8s; // Transition takes 1.2s
// }
// --- END: MODIFIED CODE ---


function createItem(text) {
  const el = document.createElement('div');
  el.className = 'roll-item';
  el.innerHTML = `<div class="roll-icon"></div>${text}`;
  return el;
}

function applyDepthStyling() {
  const items = track.querySelectorAll('.roll-item');

  items.forEach((item, i) => {
    item.classList.remove('level-0','level-1','level-2','level-3');

    const d = Math.abs(i - activeIndex);
    if (d === 0) item.classList.add('level-3');
    else if (d === 1) item.classList.add('level-2');
    else if (d === 2) item.classList.add('level-1');
    else item.classList.add('level-0');
  });
}

/* preload */
for (let i = 0; i < visibleItems; i++) {
  if (taskIndex < TASKS.length) {
    track.appendChild(createItem(TASKS[taskIndex++]));
  }
}
applyDepthStyling();

function tick(now) {
  const t = ((now - start) % period) / period;
  const angle = Math.sin(t * Math.PI * 2) * maxAngle;
  arm.style.transform = `translateX(-50%) rotate(${angle}deg)`;

  const atPeak = Math.abs(angle) > peakThreshold;

  if (atPeak && !hasTicked && !listDone) {

    const items = track.querySelectorAll('.roll-item');
    const active = items[activeIndex];

    if (active) {
      active.classList.add('completed');
      active.querySelector('.roll-icon').classList.add('checked');
    }

    if (taskIndex < TASKS.length) {
      track.appendChild(createItem(TASKS[taskIndex++]));
    }

    if (taskIndex >= TASKS.length && track.children.length === 4) {
        listDone = true;
      }

    applyDepthStyling();

    requestAnimationFrame(() => {
      track.style.transition = `transform ${transitionDuration}ms ease-out`;
      track.style.transform = `translateY(-${itemHeight}px)`;
    });

    setTimeout(() => {
      track.style.transition = 'none';
      track.style.transform = 'translateY(0)';
      if (track.firstElementChild) track.firstElementChild.remove();
      track.offsetHeight;
      track.style.transition = `transform ${transitionDuration}ms ease-out`;
    }, transitionDuration);

    hasTicked = true;
  }

  if (!atPeak) hasTicked = false;
  requestAnimationFrame(tick);
}

requestAnimationFrame(tick);
</script>