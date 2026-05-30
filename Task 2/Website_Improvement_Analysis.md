# InAmigos Foundation — Website Improvement Analysis

**Website:** https://inamigosfoundation.org.in/
**Prepared by:** Harsh Vanguard
**Date:** May 2025

---

## 1. Spelling Mistake — "Sewa" Instead of "Seva"

The project name "Seva" is misspelled as "Sewa" on the homepage hero banner. This is a small but noticeable error that can confuse visitors and looks careless.

**Screenshot:**

[Insert screenshot of hero banner showing "SEWA" text]

**Suggestion:** Correct the spelling to "Seva" on the slider to match the actual project name used everywhere else on the site.

---

## 2. Gallery Zoom is Broken

When you click on any image in the Gallery section, instead of showing a zoomed-in version of the photo, it just puts a **dark shadow over the entire page**. The actual image never loads. The only way to exit is by clicking the small X button in the top-right corner.

This is a bad user experience because visitors expect to see the image bigger, not a blank dark screen.

**Screenshot:**

[Insert screenshot showing the dark overlay with no image loading]

**Suggestion:** Fix the lightbox/popup plugin so it actually displays the full-size image when clicked.

---

## 3. Causes Page is Completely Empty

The homepage has a section called "OUR CAUSES" with a "View All Causes" button. But when you click it, the Causes page shows **"No Results"** — it's completely empty with no content at all.

This is one of the main pages of an NGO website and it has nothing on it.

**Screenshot:**

[Insert screenshot of empty Causes page showing "No Results"]

**Suggestion:** Add the six projects (Seva, Bachpanshala, Jeev, Udaan, Prakriti, Vikas) as cause cards on this page, or remove the "View All Causes" button until the page is ready.

---

## 4. Hidden Spam Links in the Source Code

When you view the page source code (Right Click → View Page Source), the very first lines contain **hidden spam links** with the text "slot gacor" (a gambling-related term). There are 9 such links on every single page.

These links are invisible to normal visitors but Google can read them. This usually means the website has been **hacked or injected with malicious code**. Google can penalise the website for this and remove it from search results.

**Screenshot:**

[Insert screenshot of page source showing the hidden "slot gacor" divs]

**Suggestion:** Remove all these hidden divs from the code immediately. Change all admin passwords and check the server for any malware or unauthorized access.

---

## 5. Social Media Links Point to Wrong Pages

The footer has a "Follow us" section with social media icons. But most of these links just go to the **homepage of that platform**, not to InAmigos's actual profile:

- **Facebook** → Goes to their actual page (Correct)
- **Twitter** → Goes to twitter.com homepage (Wrong)
- **Google+** → Google+ doesn't even exist anymore (Wrong)
- **Pinterest** → Goes to pinterest.com homepage (Wrong)
- **Instagram** → Goes to their actual page (Correct)

Also, the foundation's **YouTube channel** is not linked anywhere on the site even though they have one.

**Screenshot:**

[Insert screenshot of footer showing the social media icons]

**Suggestion:** Remove Google+ since the platform is shut down. Remove Pinterest and Twitter if they don't have active profiles. Add their YouTube channel link (youtube.com/@inamigosfoundation).

---

## 6. Same Meta Description on Every Page

Every page on the website uses the exact same description in the HTML code. Whether you visit Home, About Us, or Causes — the description tag is identical:

*"All funds raised by InAmigos Foundation may be pooled together and allocated towards foods and water, education and social inclusion initiatives across India."*

Google uses this description to show results in search. When every page has the same one, Google can't tell them apart and may rank the site lower.

**Suggestion:** Write a short, unique description for each page that tells Google what that specific page is about.

---

## Summary

| # | Issue Found | Impact |
|---|------------|--------|
| 1 | "Seva" is misspelled as "Sewa" | Looks careless, confuses visitors |
| 2 | Gallery zoom doesn't show images | Bad user experience |
| 3 | Causes page is empty | Main page has no content |
| 4 | Spam links hidden in source code | Website may be hacked, SEO risk |
| 5 | Social media links go nowhere | Misleading, missing YouTube |
| 6 | Same meta description everywhere | Hurts search engine ranking |

---

*Prepared as part of the InAmigos Foundation Web Development Internship — Task 2*
