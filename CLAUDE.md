# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Knight's Portfolio & Homelab - a personal portfolio website for a security engineer showcasing professional work, cybersecurity expertise, and personal projects. The site is a single-page application built with pure HTML, CSS, and JavaScript with a polished "enterprise security engineer" design: light/dark theming, refined interactions, and toned-down easter eggs.

## Architecture

### Single-File Architecture
- **Complete Self-Contained Application**: Everything is in `index.html` (~1,730 lines)
- **Embedded Styles**: All CSS is within `<style>` tags in the HTML head
- **Embedded JavaScript**: All interactivity handled by vanilla JavaScript in `<script>` tags
- **No Build Process**: Direct deployment - open `index.html` in any browser
- **Minimal External Dependencies**: Cloudflare Turnstile script for bot protection + Google Fonts (Space Grotesk, IBM Plex Sans, IBM Plex Mono)

### Page Structure
The site uses a single-page layout with smooth scrolling navigation:
- **Header/Navigation**: Fixed 72px header (backdrop blur) with links to #home, #about, #projects, #writing, #contact, a theme toggle, and a "Résumé ↓" download button; a 3px scroll-progress bar spans the top edge
- **Hero Section** (#home): Drifting grid-line background, eyebrow label, name, subhead, two CTAs, "verify resume checksum" copy link, and a 4-stat row
- **About Section** (#about): Sticky left rail (HB avatar tile with CISSP badge + vertical career timeline) beside a 7-row single-expand accordion of career/skill highlights, grouped skill pills, and a CISSP/Credly callout
- **Projects Section** (#projects): "Professional Experience" cards (CASE 01-03 with metric pills) and "Personal Projects" cards (category tags with GitHub links)
- **Writing Section** (#writing): Placeholder for future long-form posts ("First post in progress") — do not fabricate posts
- **Contact Section** (#contact): Email (with copy button), LinkedIn, GitHub pills, and a PGP/GPG card with click-to-copy fingerprint, keyserver link, and `gpg --recv-keys` command

### Interactive Features Architecture
- **Theme Toggle**: Light/dark mode via `data-theme` on `<html>`; defaults to `prefers-color-scheme`, persists in `localStorage`
- **Scroll Progress Bar**: Recomputed on scroll, also drives scroll-to-top button visibility (>5%)
- **Accordion**: Single-expand pattern - clicking a row collapses others; chevron rotates 180°; details fade/slide in
- **Copy-to-Clipboard**: Email, GPG fingerprint, and resume SHA-256 checksum copy via `navigator.clipboard` with a bottom-center toast (~1.8s)
- **Easter Eggs (toned down)**: Konami code (↑↑↓↓←→←→BA) and logo double-click both trigger an auto-dismissing "ACCESS GRANTED" card (~2.6s); a console greeting hints at it. Toggle all of this off via the `SHOW_EASTER_EGGS` flag in the script
- **Responsive Nav**: Below 780px the nav collapses to a hamburger with a stacked link panel

### Color Scheme & Design System
- **Primary Indigo**: `#3454D1`; **Accent Amber/Gold**: `#C9A227`
- **Light mode**: bg `#F7F7F5`, alt bg `#EFEEE9`, surface `#FFFFFF`, text `#14171C`/`#4B535E`/`#8A93A0`
- **Dark mode**: bg `#0E1116`, alt bg `#12161D`, surface `#161B22`, text `#E6E8EB`/`#B4B9C2`/`#7C8592`
- All colors are CSS custom properties on `:root` / `html[data-theme="dark"]`
- **Typography**: Space Grotesk (display/headings), IBM Plex Sans (body), IBM Plex Mono (labels, eyebrows, technical strings)
- **Animation Library**: Custom keyframes (fadeUp, gridDrift, accessPop)

## File Structure

This is an extremely simple project with minimal files:
- `index.html` - The entire application (HTML, CSS, and JavaScript)
- `README.md` - Simple project description
- `CLAUDE.md` - This guidance file
- `resume.pdf` - Downloadable resume (linked from header Résumé button)
- `resume_src.html` - Source for the resume PDF
- `github_profile_logo.svg` - Legacy logo asset (the header logo is now a CSS-rendered "HB" monogram tile)

**No package.json, no build tools, no test frameworks, no linting tools, no dependencies.**

## Development Commands

### Local Development
```bash
# Serve locally (any HTTP server works)
python -m http.server 8000
# Or use Node.js
npx serve .
# Or simply open file
open index.html
```

### Version Control
```bash
# Standard git workflow
git add index.html
git commit -m "Update portfolio content"
git push origin main
```

## Content Management

### Adding New Projects
Projects are defined in the `#projects` section. Each personal project card follows this structure:
```html
<div class="project-card project-card--personal">
    <div class="project-tag">CATEGORY</div>
    <h4>Project Title</h4>
    <p>Description with technical details</p>
    <div class="project-links">
        <a href="github-url" class="project-link" target="_blank" rel="noopener">View Code ↗</a>
        <a href="docs-url" class="project-link" target="_blank" rel="noopener">Docs ↗</a>
    </div>
</div>
```
Professional cards use `project-card--pro`, a `CASE 0N` tag, and `<span class="metric">` pills instead of links.

### Current Featured Projects
**Professional Experience Section:**
- Senior Product Security Engineer @ Slack
- Security Engineer @ Amazon
- Senior Security Consultant @ Synopsys

**Personal Projects Section:**
1. **HMAC Implementation & Security Analysis**: Cryptographic security analysis (GitHub: hbhetaria2611/HMAC)
2. **Cloudflare Analytics Dashboard**: Modern Grafana-style dashboard for monitoring Cloudflare analytics in real-time (GitHub: hbhetaria2611/cloudflare-analytics-dashboard-workers)
3. **Homelab Monitoring Stack**: Comprehensive monitoring solution for distributed homelab setups using Grafana, Prometheus, and AlertManager (GitHub: hbhetaria2611/home-lab-management)
4. **AI-Powered CI/CD Security Automation**: LLM-based code review, security gate enforcement, and anomaly detection

### Professional Experience Management
Experience appears in two places in the About section:
- The left-rail vertical timeline (year / role / company)
- The accordion (`.accordion-item` rows with an index, title, blurb, detail list, and italic pull-quote)
- All experience details should match LinkedIn profile accuracy

### Skills Management
Skills are grouped into three pill lists (Security / Cloud & Infrastructure / Dev & Automation) using `<span class="skill-tag">` elements.

### Interactive Elements Customization
- **Easter Eggs**: Set `SHOW_EASTER_EGGS = false` in the script for a fully serious build
- **Konami Code**: Sequence defined in the `seq` array
- **Color Themes**: Swap `--primary`/`--accent` custom properties (alternates explored: teal `#0F766E`/gold, brick `#7C2D12`/slate `#94A3B8`, navy `#1E3A8A`/red `#DC2626`)
- **Animation Speeds**: Adjust `animation-duration` in CSS keyframes

## Important Technical Details

### Performance Considerations
- **Single Request Loading**: All markup/styles/scripts inline; only fonts and Turnstile load externally
- **CSS Transforms**: Hardware-accelerated animations for smooth performance
- **Passive scroll listener** drives the progress bar, active-nav highlight, and scroll-to-top button

### Professional Context
This is a cybersecurity professional's portfolio emphasizing:
- Security engineering expertise and professional experience
- Technical project demonstrations with quantified metrics
- Professional presentation with subtle, credible interactions
- No sensitive information exposure (all content is public-facing)

### Browser Compatibility
- **Modern Browser Features**: Uses ES6+, CSS Grid, CSS custom properties, backdrop-filter
- **Responsive Design**: Single 780px breakpoint collapses nav and the About grid
- **Progressive Enhancement**: Core content accessible even without JavaScript
- **Reduced Motion**: `prefers-reduced-motion` disables animations and smooth scrolling

### Security Features
- **Bot Protection**: Cloudflare Turnstile integration for bot detection and protection
- **Content Security**: No external content dependencies beyond Turnstile and Google Fonts
- **PGP/GPG**: Contact section publishes the key fingerprint with a keyserver verification link

## Important Instructions
- **Single File Architecture**: Do not create additional files - everything belongs in `index.html`
- **No Build Process**: This is intentional - the site deploys by simply serving the HTML file
- **External Dependencies**: Avoid adding more - only Cloudflare Turnstile and Google Fonts are acceptable
- **Security Context**: This is a cybersecurity professional's portfolio; easter eggs are intentionally minimal (Konami code + logo double-click only)
- **Content Accuracy**: All professional experience must match LinkedIn profile details exactly
- **Resume Integration**: Portfolio includes a Résumé download button linking to `/resume.pdf`

## Content Guidelines
- Professional experience should reflect actual responsibilities and achievements
- All job titles and company names must be accurate
- Skills section should represent current technical capabilities
- Project descriptions should include quantifiable metrics where possible
- Maintain professional tone while keeping interactive elements engaging
- The Writing section stays a placeholder until real posts exist - do not fabricate posts
