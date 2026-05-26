# InAmigos Foundation — Website Improvement Analysis

**Website:** https://inamigosfoundation.org.in/
**Prepared by:** Harsh
**Date:** May 2025

---

## 1. Hidden Spam Links Found on Every Page

When you right-click and "View Page Source", the very first lines of code contain **hidden spam links** that say "slot gacor" (a gambling term). These links are invisible to visitors but search engines can see them.

This means the website may have been **hacked or injected with malicious code**. Google can penalise or remove the site from search results because of this.

**Where to find it:** Open any page → Right Click → View Page Source → Look at the very first lines before `<!DOCTYPE html>`

```
<div style="display:none">
  <a href="https://shopnoit.com/">slot gacor</a>
</div>
```

There are **9 such hidden links** on every page.

**Fix:** Remove all these hidden divs immediately and scan the server for malware.

---

## 2. "Donate Now" Button is Disabled

The most important button for any NGO — the **Donate Now button** in the navigation bar — is completely **commented out** (hidden using `<!-- -->`). Visitors have no quick way to donate from the header.

**Where to find it:** Inspect the navigation bar → Look for commented-out code in the top-right area of the navbar.

```
<!--<a href="#" class="main-btn">Donate Now</a>-->
```

One of the commented-out donate links also has a **broken URL** — it joins two URLs together which would never work:

```
https://inamigosfoundation.org.in/https://rzp.io/l/kWQ87HP
```

**Fix:** Uncomment the Donate button and use the correct Razorpay link: `https://rzp.io/l/kWQ87HP`

---

## 3. Causes Page is Completely Empty

The homepage has a section called "OUR CAUSES" with a button that says "View All Causes". But when you click it, the Causes page (`/causes`) is **completely blank** — no causes, no content, nothing.

**Where to find it:** Visit https://inamigosfoundation.org.in/causes — you'll see just the header and footer with empty space in between.

**Fix:** Either add the six project causes to this page, or remove the "View All Causes" button from the homepage so visitors don't land on an empty page.

---

## 4. About Us Section is a Wall of Text

The "About Us" section on the homepage has **everything crammed into one giant paragraph** — the founding story, certifications, all six projects, the mission statement — all without any line breaks, headings, or formatting.

No one is going to read a 250-word paragraph on a website. Users scan, they don't read.

**Where to find it:** Scroll down to the "Get to Know Us Better" section on the homepage.

**Fix:** Break it into short paragraphs. Use bullet points for the certifications. Show the projects as separate cards instead of listing them in a paragraph.

---

## 5. About Us Page Has ChatGPT Code Left In

The About Us page (`/page/About-Us`) has been written using ChatGPT, which is fine — but the **raw ChatGPT HTML code** was pasted directly into the page without cleaning it up. If you inspect the code, you can see:

```
data-message-author-role="assistant"
data-message-model-slug="gpt-4o"
```

These are ChatGPT's internal code tags. It looks unprofessional and anyone who inspects the page can tell the content was copy-pasted from ChatGPT.

**Where to find it:** Visit the About Us page → Right Click → Inspect → Look at the `<div>` elements inside the content area.

**Fix:** Copy only the text from ChatGPT and paste it as plain text in the website editor. Remove all the extra code classes.

---

## 6. Social Media Links Go Nowhere

The header has social media icons for Facebook, Twitter, Google, Pinterest, and Instagram. But only **Facebook and Instagram** have correct links. The rest go to generic homepages:

| Icon | Where it Links | Problem |
|------|---------------|---------|
| Facebook | facebook.com/inamigos.inamigos | Correct |
| Twitter | twitter.com | Just the homepage, not their profile |
| Google | google.com | Not a social media platform |
| Pinterest | pinterest.com | Just the homepage, not their profile |
| Instagram | instagram.com/inamigos/ | Correct |

Also, the **YouTube channel** is missing entirely — they have one at `youtube.com/@inamigosfoundation`.

**Where to find it:** Look at the green top bar of the website with the small social icons.

**Fix:** Remove icons for platforms they don't use. Add their YouTube link. Fix Twitter to point to their actual profile.

---

## 7. Same Meta Description on Every Page

Every page on the website — Home, About, Causes — uses the **exact same description** in the code:

```
"All funds raised by InAmigos Foundation may be pooled together and
allocated towards foods and water, education and social inclusion
initiatives across India."
```

This hurts SEO because Google needs each page to have its own unique description. The description is also quite generic and doesn't mention what makes InAmigos special.

**Where to find it:** View Page Source on any page → Search for `<meta name="description"`.

**Fix:** Write a unique, specific description for each page (keep it under 160 characters).

---

## 8. Website Loads Too Many Unnecessary Files

The website loads **16 CSS files and 20+ JavaScript files** on every page. One of them is **TinyMCE** — a text editor meant for admins to write content — which is loaded even for regular visitors who will never use it.

This slows down the website and wastes the visitor's data.

**Where to find it:** Right Click → Inspect → Go to the "Network" tab → Reload the page → Count the CSS and JS files.

**Fix:** Remove TinyMCE and other admin-only scripts from public pages. Combine multiple CSS files into one. This will make the site load much faster.

---

## Summary Table

| # | Issue | Why It Matters |
|---|-------|---------------|
| 1 | Spam links hidden in code | Site may be hacked, Google can penalise it |
| 2 | Donate button disabled | Visitors can't easily donate |
| 3 | Causes page is empty | Bad user experience, broken navigation |
| 4 | About section is a wall of text | No one will read it |
| 5 | ChatGPT code visible in About page | Looks unprofessional |
| 6 | Social links go to wrong pages | Misleading, missing YouTube |
| 7 | Same meta description everywhere | Hurts search engine ranking |
| 8 | Too many files loaded | Slows down the website |


