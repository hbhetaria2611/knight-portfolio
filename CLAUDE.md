# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Knight's Portfolio & Homelab - a personal portfolio website for a security engineer showcasing professional work, cybersecurity expertise, and personal projects. The site is a single-page application built with pure HTML, CSS, and JavaScript with extensive interactive animations and effects.

## Architecture

### Single-File Architecture
- **Complete Self-Contained Application**: Everything is in `index.html` (~1,069 lines)
- **Embedded Styles**: All CSS is within `<style>` tags in the HTML head
- **Embedded JavaScript**: All interactivity handled by vanilla JavaScript in `<script>` tags
- **No Build Process**: Direct deployment - open `index.html` in any browser
- **Minimal External Dependencies**: Only Cloudflare Turnstile script for bot protection

### Page Structure
The site uses a single-page layout with smooth scrolling navigation:
- **Header/Navigation**: Fixed header with links to #home, #about, #projects, #contact
- **Hero Section** (#home): Animated landing with typing effects and floating particles
- **About Section** (#about): Personal information, skills grid, and CISSP certification
- **Projects Section** (#projects): Featured work with GitHub links and live demos
- **Contact Section** (#contact): Professional contact information and social links

### Interactive Features Architecture
- **Floating Particles System**: 50 dynamically generated particles with random animations
- **Custom Cursor Effects**: SVG-based cursor with trailing dots that follow mouse movement
- **Click Effects**: Random emoji generation (💥⭐✨🎉🔥) at click coordinates
- **Scroll Animations**: Intersection Observer API for fade-in effects and bounce animations
- **Easter Eggs**: Konami code detection (↑↑↓↓←→←→BA) triggering rainbow background mode

### Color Scheme & Design System
- **Primary Purple**: `#4a154b` and `#350d36` (gradients throughout)
- **Accent Green**: `#10b981` for homelab cards and highlights
- **Text Colors**: `#1d1c1d` (primary), `#616061` (secondary), `#4a5568` (descriptions)
- **Interactive States**: Enhanced hover effects with transforms, shadows, and color transitions
- **Animation Library**: Custom keyframes (pulse, float, bounce, wiggle, shake, rainbow-bg)

## File Structure

This is an extremely simple project with minimal files:
- `index.html` - The entire application (1,056 lines containing HTML, CSS, and JavaScript)
- `README.md` - Simple project description
- `CLAUDE.md` - This guidance file

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
Projects are defined in the `#projects` section. Each project follows this structure:
```html
<div class="project-card">
    <div class="project-image">🔐</div>
    <div class="project-content">
        <h3>Project Title</h3>
        <p>Description with technical details</p>
        <div class="project-links">
            <a href="github-url">View Code</a>
            <a href="live-demo-url">Live Demo</a>
        </div>
    </div>
</div>
```

### Current Featured Projects
1. **HMAC Implementation & Security Analysis**: Cryptographic security analysis (GitHub: hbhetaria2611/HMAC)
2. **Meal Planning Website**: Full-stack application (GitHub: hbhetaria2611/meal-planning, Live: meal.hnbhetaria.com)
3. **Cloudflare Analytics Dashboard**: Modern Grafana-style dashboard for monitoring Cloudflare analytics in real-time (GitHub: hbhetaria2611/cloudflare-analytics-dashboard-workers, Live: analytics.hnbhetaria.com)
4. **Homelab Monitoring Stack**: Comprehensive monitoring solution for distributed homelab setups using Grafana, Prometheus, and AlertManager (GitHub: hbhetaria2611/home-lab-management)

### Skills Management
Skills are individual `<span class="skill-tag">` elements in the About section with interactive hover effects including star animations and color transitions.

### Interactive Elements Customization
- **Particle Count**: Modify `particleCount = 50` in JavaScript for performance tuning
- **Animation Speeds**: Adjust `animation-duration` in CSS keyframes
- **Konami Code**: Sequence defined in `correctCode` array for easter egg customization
- **Color Themes**: All color variables are in CSS custom properties for easy theme changes

## Important Technical Details

### Performance Considerations
- **Single Request Loading**: All assets inline for minimal HTTP requests
- **CSS Transforms**: Hardware-accelerated animations for smooth performance
- **Intersection Observer**: Efficient scroll-based animations without performance impact
- **Memory Management**: Cursor trail cleanup prevents memory leaks during extended use

### Professional Context
This is a cybersecurity professional's portfolio emphasizing:
- Security engineering expertise and professional experience
- Technical project demonstrations with quantified metrics
- Professional presentation with engaging, memorable interactions
- No sensitive information exposure (all content is public-facing)

### Browser Compatibility
- **Modern Browser Features**: Uses ES6+, CSS Grid, Intersection Observer API
- **Responsive Design**: Mobile-first approach with comprehensive media queries
- **Progressive Enhancement**: Core content accessible even without JavaScript animations

### Security Features
- **Bot Protection**: Cloudflare Turnstile integration for bot detection and protection
- **Content Security**: No external content dependencies beyond Turnstile script
- **Security Easter Eggs**: Hidden flags and console commands for security demonstrations (see HTML comments in index.html:4-15)

## Important Instructions
- **Single File Architecture**: Do not create additional files - everything belongs in `index.html`
- **No Build Process**: This is intentional - the site deploys by simply serving the HTML file
- **External Dependencies**: Avoid adding any - only Cloudflare Turnstile is acceptable
- **Security Context**: This is a cybersecurity professional's portfolio with security-themed easter eggs