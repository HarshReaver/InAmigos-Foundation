# InAmigos Foundation — NGO Awareness Webpage

A clean, responsive awareness webpage for **InAmigos Foundation**, a Section 8 registered non-profit organisation working across 28 states of India.

Built with plain **HTML & CSS** (no frameworks, no build tools) as part of the Web Development Internship Task.

**Live Demo:** [harshreaver.github.io/InAmigos-Foundation](https://harshreaver.github.io/InAmigos-Foundation/)

---

## Project Structure

```
18. InAmigos Website/
├── index.html      # Main webpage (single-page layout)
├── style.css       # All styles, responsive design, animations
├── LICENSE         # MIT License
└── README.md       # This file
```

Both files are self-contained. Open `index.html` in any browser to view the page — no server or build step needed.

---

## Sections

| Section       | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| **Hero**      | Auto-sliding banner with 5 images from the official site, key stats, CTAs   |
| **About**     | NGO introduction, founding details, certifications (80G, 12A, ISO, etc.)    |
| **Projects**  | 6 initiative cards — Seva, Bachpanshala, Jeev, Udaan, Prakriti, Vikas       |
| **Impact**    | Key numbers: 200+ volunteers, 28 states, 6 projects, 50K+ beneficiaries    |
| **Gallery**   | Grid of images sourced from the official InAmigos gallery                   |
| **Events**    | 3 recent events with dates, categories, and descriptions                   |
| **Join Us**   | Call-to-action with Donate, Volunteer, and Spread the Word cards            |
| **Footer**    | Quick links, project links, contact info, social media                     |

---

## Tech Stack

- **HTML5** — Semantic elements (`<article>`, `<section>`, `<nav>`, `<footer>`)
- **CSS3** — Custom properties, Grid, Flexbox, scroll animations, responsive breakpoints
- **Font Awesome 6** — Icons (loaded via CDN)
- **Google Fonts** — DM Sans (body) + Lora (headings)

No JavaScript frameworks, no npm, no build process.

---

## How to View

1. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
2. Or use VS Code with the **Live Server** extension for hot-reloading

---

## SEO Features

- Descriptive `<title>` and `<meta description>`
- Open Graph tags (Facebook, LinkedIn sharing)
- Twitter Card tags
- JSON-LD structured data (Schema.org `NGO` type)
- Canonical URL
- `rel="noopener noreferrer"` on all external links
- Lazy loading on below-the-fold images (`loading="lazy"`)
- ARIA labels and roles for accessibility
- Semantic heading hierarchy (single `<h1>`, proper `<h2>`–`<h5>` nesting)

---

## Content Sources

All content and images are sourced from official InAmigos Foundation channels:

- **Website:** [inamigosfoundation.org.in](https://inamigosfoundation.org.in/)
- **Instagram:** [@inamigos](https://www.instagram.com/inamigos/)
- **Facebook:** [InAmigos Foundation](https://www.facebook.com/inamigos.inamigos)

No third-party or AI-generated images are used. All visuals are official assets from the foundation's website.

---

## External Links

| Link                                                      | Purpose                    |
|-----------------------------------------------------------|----------------------------|
| [Donate (Razorpay)](https://rzp.io/l/kWQ87HP)            | Donation page              |
| [Volunteer Form](https://forms.gle/AB4c1hLaDDmtrKGU7)    | Google Form for volunteers |
| [Official Website](https://inamigosfoundation.org.in)     | InAmigos Foundation site   |

---

## Colour Palette

| Colour          | Hex       | Usage                     |
|-----------------|-----------|---------------------------|
| Primary Green   | `#00CC83` | CTAs, highlights, accents |
| Dark            | `#1a1d23` | Backgrounds, text         |
| Off-white       | `#f5f6f8` | Alternate section bg      |
| Text            | `#3a3f4b` | Body text                 |
| Text Light      | `#6b7280` | Secondary text            |

---

## Browser Support

Tested on modern browsers. Uses CSS Grid, Flexbox, `backdrop-filter`, and `IntersectionObserver` — all supported in Chrome 80+, Firefox 80+, Safari 14+, Edge 80+.

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

All content and images belong to InAmigos Foundation and are used here for educational and awareness purposes.
