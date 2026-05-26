# InAmigos Foundation — Website Improvement Analysis

**Website:** [inamigosfoundation.org.in](https://inamigosfoundation.org.in/)
**Analyst:** Harsh Vanguard
**Date:** May 2025

---

## Executive Summary

This document presents a detailed analysis of the InAmigos Foundation website, identifying key areas for improvement across security, SEO, performance, design, content, user experience, accessibility, and mobile responsiveness. Each finding is categorised by severity and accompanied by an actionable recommendation.

---

## Table of Contents

1. [Critical Security Issues](#1-critical-security-issues)
2. [SEO Deficiencies](#2-seo-deficiencies)
3. [Performance Bottlenecks](#3-performance-bottlenecks)
4. [Design & Layout Problems](#4-design--layout-problems)
5. [Content Structure Issues](#5-content-structure-issues)
6. [User Experience (UX) Gaps](#6-user-experience-ux-gaps)
7. [Accessibility Failures](#7-accessibility-failures)
8. [Mobile Responsiveness](#8-mobile-responsiveness)

---

## 1. Critical Security Issues

> [!CAUTION]
> These issues pose serious risks to the website's reputation and search engine ranking.

### 1.1 Spam Link Injection (Severity: CRITICAL)

**Finding:** Hidden spam links are injected at the very top of every page's `<body>`, before the actual HTML document even starts:

```html
<div style="display:none">
  <a href="https://shopnoit.com/">slot gacor</a>
</div>
<div style="display:none">
  <a href="https://webwideit.solutions/">slot gacor</a>
</div>
<!-- ... 7+ more hidden "slot gacor" links -->
```

These appear on **every single page** — Home, About Us, Causes, etc. This is a strong indicator that the website has been **compromised or hacked**. "Slot gacor" is a gambling term commonly injected by SEO spammers.

**Impact:**
- Google may **penalise or de-index** the website for hosting spam links
- Damages the NGO's credibility and trust
- Violates Google's Webmaster Guidelines

**Recommendation:**
- Immediately audit the server and CMS for malware
- Remove all hidden `<div>` elements containing spam links
- Change all admin passwords and update the CMS
- Submit a malware review request to Google Search Console

---

### 1.2 CSRF Token Exposed in HTML (Severity: MEDIUM)

**Finding:** The CSRF token is rendered in a `<meta>` tag on every page:
```html
<meta name="csrf-token" content="Z5um7F7EJ0Mt47efK71fHioBZIRFJMFp5No1ztAU">
```

While this is standard for Laravel applications, the token changes on every request — if caching is misconfigured, stale tokens could cause form submission failures.

### 1.3 Stripe Test Keys in Production (Severity: HIGH)

**Finding:** On the Causes page, a **Stripe test API key** is hardcoded in the JavaScript:
```javascript
var stripe = Stripe('pk_test_2fR28XACHzyFUmp44ah5KKP000BvS2sjXk');
```

This means the donation payment system is running in **test mode** — real donations may not process correctly.

**Recommendation:** Replace with production Stripe keys and move all API keys to server-side environment variables.

---

## 2. SEO Deficiencies

> [!WARNING]
> The website has significant SEO gaps that limit its visibility on search engines.

### 2.1 Weak Meta Description (Severity: HIGH)

**Finding:** Every page uses the exact same generic meta description:
```html
<meta name="description" content="All funds raised by InAmigos Foundation may be pooled together and allocated towards foods and water, education and social inclusion initiatives across India.">
```

This is the same on Home, About Us, and Causes pages — Google needs **unique descriptions per page** to rank them independently.

**Recommendation:** Write unique, keyword-rich descriptions (150-160 characters) for each page:
- **Home:** "InAmigos Foundation — A Section 8 NGO working across 28 states of India through 6 projects in education, animal welfare, women empowerment & sustainability."
- **About:** "Founded in 2020 by Govind Shukla, InAmigos Foundation is a NITI Aayog registered, ISO 9001:2015 certified non-profit based in Chhattisgarh, India."
- **Causes:** "Support our six causes: Project Seva, Bachpanshala, Jeev, Udaan, Prakriti & Vikas — providing food, education, and empowerment across India."

### 2.2 Only One Keyword (Severity: HIGH)

**Finding:**
```html
<meta name="keywords" content="inamigos foundation">
```

Only a single keyword is used across the entire site.

**Recommendation:** Add relevant long-tail keywords:
```
NGO India, non-profit Chhattisgarh, volunteer India, donate charity,
education underprivileged children, women empowerment NGO,
animal welfare India, environmental conservation, skill development
```

### 2.3 Missing Open Graph & Twitter Cards (Severity: MEDIUM)

**Finding:** No Open Graph or Twitter Card meta tags are present. When the website link is shared on Facebook, LinkedIn, WhatsApp, or Twitter, no preview image, title, or description appears — the platform has to guess, usually showing a poor result.

**Recommendation:** Add to every page:
```html
<meta property="og:title" content="InAmigos Foundation">
<meta property="og:description" content="...">
<meta property="og:image" content="...">
<meta property="og:url" content="...">
<meta name="twitter:card" content="summary_large_image">
```

### 2.4 Missing Structured Data (Severity: MEDIUM)

**Finding:** No Schema.org JSON-LD markup is present. Google cannot identify the site as an NGO or display rich results.

**Recommendation:** Add `@type: NGO` structured data with founder info, location, social links, and contact details.

### 2.5 No Canonical URL (Severity: MEDIUM)

**Finding:** No `<link rel="canonical">` tag on any page. If the site is accessible via multiple URLs (www vs non-www, HTTP vs HTTPS), Google may treat them as duplicate content.

### 2.6 Page Title Format (Severity: LOW)

**Finding:** Title is "Home - Inamigos Foundation" — the organisation name is inconsistently capitalised ("Inamigos" vs "InAmigos").

**Recommendation:** Standardise to "InAmigos Foundation — Empowering Lives, Spreading Compassion"

---

## 3. Performance Bottlenecks

> [!WARNING]
> Slow page loads directly hurt user engagement and search rankings (Google Core Web Vitals).

### 3.1 Outdated jQuery Version (Severity: HIGH)

**Finding:**
```html
<script src=".../jquery-1.12.4.min.js"></script>
```

jQuery **1.12.4** is from 2016 and contains known security vulnerabilities. The current version is 3.7.x.

**Recommendation:** Upgrade to jQuery 3.7+ or replace jQuery-dependent code with vanilla JavaScript.

### 3.2 TinyMCE Loaded on Every Page (Severity: HIGH)

**Finding:** The TinyMCE rich text editor (a heavy admin-only library) is loaded on **every public-facing page**, including the homepage:
```html
<script src=".../tinymce/jquery.tinymce.min.js"></script>
<script src=".../tinymce/tinymce.min.js"></script>
```

This adds ~500KB+ of unnecessary JavaScript that visitors never use.

**Recommendation:** Load TinyMCE only on admin/backend pages.

### 3.3 Excessive CSS & JS Files (Severity: MEDIUM)

**Finding:** Each page loads **16+ separate CSS files** and **20+ JavaScript files**:

| Type | Count | Examples |
|------|-------|---------|
| CSS | 16 | bootstrap, font-awesome, line-awesome, animate, barfiller, magnific-popup, flaticon, owl.carousel, style, responsive, validate, video, aos, countdown, pagination, lightbox |
| JS | 20+ | jquery, popper, bootstrap, wow, waypoints, counterup, owl.carousel, isotope, magnific-popup, sticky, barfiller, main, bvalidator, aos, countdown, video, tinymce (x2), backTop, pagination, lightbox (x2), share |

Each file requires a separate HTTP request, significantly slowing page load.

**Recommendation:**
- Combine and minify CSS into 1-2 files
- Combine and minify JS into 1-2 files
- Use a CDN for common libraries (Bootstrap, jQuery)
- Remove unused libraries (TinyMCE, Stripe on non-donation pages)

### 3.4 No Lazy Loading on Images (Severity: MEDIUM)

**Finding:** All images load immediately when the page opens, including gallery images and volunteer photos below the fold.

**Recommendation:** Add `loading="lazy"` to all images that are not visible on initial page load.

### 3.5 No Image Optimisation (Severity: MEDIUM)

**Finding:** Images are served as full-size JPGs without width/height attributes. No WebP format is used.

**Recommendation:**
- Add `width` and `height` attributes to prevent layout shift (CLS)
- Convert to WebP format with JPG fallback
- Serve appropriately sized images for different devices

---

## 4. Design & Layout Problems

### 4.1 "Donate Now" Button Commented Out (Severity: HIGH)

**Finding:** The primary call-to-action button in the header navigation is **entirely commented out**:
```html
<!--<div class="col-lg-2 text-right">-->
<!--  <div class="header-right-content">-->
<!--    <a href="#" class="main-btn">Donate Now</a>-->
<!--  </div>-->
<!--</div>-->
```

For an NGO, the Donate button is arguably the most important element on the page.

**Recommendation:** Restore the Donate button in the header with a working Razorpay link. Make it visually prominent with a contrasting colour and place it in the top-right corner of the navigation bar.

### 4.2 Login Link Commented Out (Severity: LOW)

**Finding:**
```html
<!--<li class="nav-item">-->
<!--  <a class="nav-link" href=".../login">Login</a>-->
<!--</li>-->
```

If the login functionality exists, hiding it creates confusion. Either remove it cleanly or restore it.

### 4.3 Broken Donate URL in Comments (Severity: MEDIUM)

**Finding:** One of the commented-out donate links has an obviously malformed URL:
```html
<!--<a href="https://inamigosfoundation.org.in/https://rzp.io/l/kWQ87HP">Donate Now</a>-->
```

The URL is a concatenation of the website URL and the Razorpay link — this would never work if uncommented.

### 4.4 Inconsistent Section Spacing (Severity: LOW)

**Finding:** The "Our Causes" section title appears but the section itself is **empty** — no cause cards are displayed. It shows a "View All Causes" button that leads to an equally empty Causes page.

**Recommendation:** Either populate the Causes section with actual cause cards or remove it from the homepage.

### 4.5 Generic Template Design (Severity: MEDIUM)

**Finding:** The website uses a generic charity template without significant customisation. The green colour (#00CC83) is applied via inline CSS that could easily be a template's colour picker output. The design does not feel unique to InAmigos.

**Recommendation:**
- Customise the template with unique visual elements
- Use the brand's actual design language consistently
- Add custom illustrations or icons instead of template defaults
- Consider a design refresh with modern typography and spacing

---

## 5. Content Structure Issues

### 5.1 Wall of Text — About Section on Homepage (Severity: HIGH)

**Finding:** The About section on the homepage is a **single giant paragraph** with no formatting:

> "InAmigos Foundation was founded on September 23, 2020, by Mr. Govind Shukla (Founder & CEO). It is a Section 8 registered non-profit organization, licensed by the Central Government. It has its base at Chhattisgarh. It holds 80G & 12A certifications... Our Key Initiatives 1. Project Seva – Providing food... 2. Project Bachpanshala – Ensuring quality education... 3. Project Jeev – Animal welfare..."

This is approximately **250 words in a single paragraph** with no line breaks, headings, or visual separation.

**Recommendation:**
- Break into short paragraphs (2-3 sentences each)
- Use sub-headings for different topics
- Present projects as visual cards, not inline text
- Add bullet points for certifications
- Keep the About section to 3-4 sentences with a "Read More" link

### 5.2 About Us Page Uses ChatGPT Formatting (Severity: MEDIUM)

**Finding:** The About Us page contains HTML classes like `data-message-author-role="assistant"`, `data-message-model-slug="gpt-4o"`, and CSS classes like `markdown prose dark:prose-invert` — these are **ChatGPT's output HTML classes** that were directly pasted into the CMS:

```html
<div class="min-h-8 text-message relative flex w-full flex-col"
     data-message-author-role="assistant"
     data-message-id="36dbb6df-..."
     data-message-model-slug="gpt-4o">
```

This looks unprofessional and reveals that the content was AI-generated without proper formatting.

**Recommendation:**
- Strip all ChatGPT/AI formatting classes and metadata
- Format the content using the CMS's native editor
- Present the content as clean HTML with proper headings and paragraphs

### 5.3 Empty Causes Page (Severity: HIGH)

**Finding:** The Causes page (`/causes`) loads the full page template (header, footer, all scripts) but shows **zero cause items**. The pagination container exists but has no content:

```html
<div class="turn-page" id="post-pager"></div>
```

A visitor clicking "View All Causes" from the homepage lands on a completely empty page.

**Recommendation:** Populate the Causes page with the six projects, or redirect the link to a populated section.

### 5.4 Social Media Links Lead to Generic Pages (Severity: LOW)

**Finding:** In the header social icons:
- Twitter link goes to `https://twitter.com` (generic homepage, not InAmigos's profile)
- Google link goes to `https://google.com` (no social presence)
- Pinterest link goes to `https://pinterest.com` (generic homepage)

Only Facebook and Instagram have correct profile links.

**Recommendation:** Either add correct profile URLs or remove social links that don't have active accounts. Add the YouTube link: `https://www.youtube.com/@inamigosfoundation`

---

## 6. User Experience (UX) Gaps

### 6.1 No Clear Call-to-Action Hierarchy (Severity: HIGH)

**Finding:** The three feature boxes ("Donate Us", "Become A Volunteer", "Join Us") all look identical with the same green background. There is no visual hierarchy to guide users toward the most important action.

**Recommendation:**
- Make "Donate" the most visually prominent (different colour, larger size)
- Add secondary styling for "Volunteer"
- Use subtle tertiary styling for "Join Us"
- Place the primary CTA (Donate) in the fixed navigation bar

### 6.2 No Search Functionality (Severity: MEDIUM)

**Finding:** The website has no search bar. Users looking for specific information must navigate through multiple pages manually.

**Recommendation:** Add a simple search feature in the navigation bar, especially useful for blogs and events.

### 6.3 No Breadcrumb Navigation (Severity: LOW)

**Finding:** Inner pages (About Us, Causes) have a breadcrumb area visually, but the structure is minimal:
```html
<h6><a href="...">Home</a> / Page</h6>
```

The breadcrumb text says "Page" instead of the actual page name on the About Us page.

**Recommendation:** Use proper breadcrumb markup with Schema.org `BreadcrumbList` for SEO benefits.

### 6.4 Volunteer Cards Lack Information (Severity: LOW)

**Finding:** Volunteer cards show only a name, title, and email. One volunteer's email (`jhfgjufv@gmail.com`) appears to be fake/placeholder data.

**Recommendation:** Verify all volunteer data and remove placeholder entries. Add brief bios or social links where available.

---

## 7. Accessibility Failures

### 7.1 Missing Alt Text and Poor Alt Descriptions (Severity: HIGH)

**Finding:** Many images use generic alt text:
```html
<img src="..." alt="Inamigos Foundation">  <!-- Logo: acceptable -->
<img src="..." alt="Donate Us">            <!-- Feature icon: vague -->
```

Gallery images and slideshow images have no meaningful alt text describing what's shown.

**Recommendation:** Write descriptive alt text for every image, e.g., "InAmigos volunteers distributing food to underprivileged families in Chhattisgarh"

### 7.2 No ARIA Labels (Severity: MEDIUM)

**Finding:** Interactive elements lack ARIA attributes:
- Social media links have no `aria-label`
- The hamburger menu button has `aria-label="Toggle navigation"` (good) but other buttons don't
- No `role` attributes on major sections

### 7.3 Poor Colour Contrast in Some Areas (Severity: MEDIUM)

**Finding:** The green (#00CC83) text on white background in certain areas may not meet WCAG AA contrast ratio requirements (4.5:1 for normal text).

**Recommendation:** Use a darker shade of green (#00875A or similar) for body text, and keep #00CC83 for buttons and large headings only.

### 7.4 No Skip-to-Content Link (Severity: LOW)

**Finding:** No "skip to main content" link for keyboard/screen reader users.

---

## 8. Mobile Responsiveness

### 8.1 Duplicate Media Queries (Severity: LOW)

**Finding:** The responsive CSS has the same `.navbar-toggler-icon` styles written twice for two different breakpoints, but the styles are identical:
```css
@media only screen and (min-width: 768px) and (max-width: 991px) {
  .navbar-toggler-icon { /* ... */ }
}
@media only screen and (max-width: 767px) {
  .navbar-toggler-icon { /* ... same styles */ }
}
```

**Recommendation:** Combine into a single `max-width: 991px` query.

### 8.2 Text-Right on Mobile (Severity: MEDIUM)

**Finding:** Social icons in the header use `text-right` class, which may cause layout issues on small screens where the icons should be centred.

### 8.3 Large Hero Images Not Optimised for Mobile (Severity: MEDIUM)

**Finding:** Slideshow images are full-size desktop images loaded on mobile devices without responsive `srcset` attributes.

**Recommendation:** Use `<picture>` element or `srcset` to serve smaller images on mobile:
```html
<img srcset="image-sm.jpg 480w, image-md.jpg 768w, image-lg.jpg 1200w"
     sizes="100vw" src="image-lg.jpg" alt="...">
```

---

## Summary of Priority Actions

| Priority | Issue | Severity |
|----------|-------|----------|
| 1 | Remove spam "slot gacor" links (security breach) | CRITICAL |
| 2 | Replace Stripe test keys with production keys | HIGH |
| 3 | Restore the "Donate Now" button in navigation | HIGH |
| 4 | Fix the empty Causes page | HIGH |
| 5 | Break the About section wall-of-text | HIGH |
| 6 | Clean ChatGPT HTML from About Us page | MEDIUM |
| 7 | Upgrade jQuery from 1.12 to 3.7+ | HIGH |
| 8 | Remove TinyMCE from public pages | HIGH |
| 9 | Add unique meta descriptions per page | HIGH |
| 10 | Add Open Graph / Twitter Card tags | MEDIUM |
| 11 | Add image alt text and lazy loading | MEDIUM |
| 12 | Fix generic social media links (Twitter, Google, Pinterest) | LOW |
| 13 | Combine and minify CSS/JS files | MEDIUM |
| 14 | Add structured data (JSON-LD) | MEDIUM |
| 15 | Improve mobile image delivery | MEDIUM |

---

## Tools Used for Analysis

- Manual HTML source code inspection
- Live URL content fetching and parsing
- WCAG colour contrast guidelines reference
- Google SEO best practices documentation


*Prepared as part of the InAmigos Foundation Web Development Internship — Task 2*
