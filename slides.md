---
marp: true
theme: default
paginate: true
header: 'Search Extension Project'
footer: 'Presentation by Alan Baines'
---

<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

# Verifiable Multi-Highlight Tool: A Case Study in Privacy-First Development and AI Collaboration

### A Technical Deep Dive

Alan Baines

2025 October

<!--
🎈 speaker notes show up like this! 👋
-->

---

## About Me & My Philosophy

### The "Why" Behind the "How"

- Lead Software Engineer, Developer Experience (DevEx) Champion, and Team Catalyst 🧡
- Core Principles
- Mentorship
- Mission

<!-- 
Core Principles: Technology choices should prioritize long-term sustainability, transparency, and maintainability.

Mentorship: Empowering colleagues, pair programming, and growth-focused code reviews.

Mission: To create tools and processes that help teams do their best work. Force Multiplier.
 -->

---

## Project Selection Context

### Why a Personal Project?

- Chose open-source project for transparency
- Explored Chrome Extension dev, AI coding, full product lifecycle

<!--
Much of my professional work is proprietary and covered by NDAs.

This project was a personal exploration into:

- Modern Chrome Extension development

- The practical boundaries of AI-assisted coding

- The full product lifecycle: from idea to the official Chrome Web Store
-->

---

## The Problem Statement

### The Search for a Trustworthy Tool

- Needed multi-keyword highlighter extension
- No open-source, privacy-first options
- Tools required invasive permissions

<!--
Goal: Find a browser extension to highlight multiple keywords on a page.
🟠 Reduce cognitive load; Universal design

Problem: Existing solutions lacked a critical feature: Trust.

Extensions with this functionality require invasive permissions ("read all your data on all websites").

No available options were open-source, making it impossible to verify that user data wasn't being tracked or sent to a third party.

This presented an unacceptable privacy and security risk.
-->

---

## The Solution: A Verifiable Highlighter

### If you want it done right, build it yourself.

- Built my own extension
- 100% local, source-available, auditable
- Highlights user keywords, saves lists

<!--
A Chrome extension to find and highlight multiple keywords.

Core Mandate #1: Privacy First. All operations are 100% local to the browser. No network calls, no data exfiltration.

Core Mandate #2: Verifiable. Fully source-available so anyone can audit the code and confirm the privacy claims.

Functionality:

- Accepts a list of words

- Highlights all occurrences on a page

- Persists word lists using local storage
-->

---

## Requirements Gathering

### Core User Needs

- Source-available, no network calls
- Add/remove keywords
- Save keywords

<!--
Initial Requirements:

- Must be open-source and make no network calls

- Users can add/remove multiple keywords

- Keywords are saved between sessions

-->

---

## Requirements Gathering: An Iterative Process

### From Static Pages to a Dynamic Web

- Single Page App problem
- Ergonomics / Usability
- Must handle dynamic content (SPAs)

<!--
Evolved Requirement (Discovered during use):

- The SPA Problem: On sites like LinkedIn, content loads dynamically without a full page refresh. 
The initial highlighting logic would miss this new content.

- New Requirement: The extension must detect page content changes and re-apply highlighting automatically.
-->

---

## The Core Experiment: AI as a Pair Programmer

### A Human-in-the-Loop, AI-Driven Approach

- I wrote mostly prompts, not code
- Acted as architect, reviewer, mentor
- Explored AI’s strengths and limits

<!--
The "Pseudo-Requirement": I would not write any of the functional code myself.

My Role: Acted as the senior engineer/architect.

- Provided clear, technical prompts to the AI (GitHub Copilot)

- Performed rigorous code reviews on every line of generated code

- Asked the AI to explain complex or unfamiliar concepts

The Goal: To explore the capabilities and limitations of AI as a development partner and learn how to leverage it effectively.
-->

---

## Technology Selection: The Power of Simplicity

### Why Plain JavaScript?

- Used plain JavaScript for transparency
- No build step, easy to audit

<!--
Primary Goal: Verifiability and Transparency.

While tools like TypeScript or Rust/WASM are powerful, they add a compilation/transpilation step.

This obfuscates the final code, making it harder for a non-expert to audit and trust.

Plain JavaScript ensures that "what you see is what you get." The code in the repository is the code that runs in the browser.

This decision directly supports the core mission of creating a provably private tool.
-->

---

## My AI Toolkit: The Right Tool for the Job

### Delineating AI Roles

- Copilot: code generation
- Gemini: docs, prose, compliance, brainstorming

<!--
Two primary AI partners were used for distinct tasks:

GitHub Copilot:
- Role: The Code Generator
- Tasks: Writing functions, implementing logic, modifying the manifest file, navigating the Chrome extension APIs

Gemini:
- Role: The Prose & Documentation Generator
- Tasks: Authoring the justifications for store permissions, writing the "About" page, answering the Chrome Store's compliance questionnaire
-->

---

## Challenge 1: Taming Single Page Applications (SPAs)

- Dynamic content not highlighted
- Used network call monitoring to re-apply highlights
- Removed duplicates for clean results

<!--
1. Trigger: Monkey patch network calls, a reliable heuristic for when new content might have appeared.
🟠 Avoid cyclic refreshes because I was also changing the DOM

2. Logic: When a network call completes, trigger the highlighting function.

3. Refinement: Re-running the highlighter created duplicate highlights. The process was updated to be a two-step sequence:
    - First, find and remove all existing highlight tags.
    - Then, perform a fresh highlighting pass on the entire document.

Outcome: A robust solution that works seamlessly on modern, dynamic websites.
-->

---

## Challenge 2: Resisting the Urge to "Just Fix It"

- AI struggled with simple changes
- Treated AI like a junior engineer, guided with prompts
- Learned strengths/weaknesses of AI
- Bidirectional Rubber Ducky

<!--
The Problem: The AI often struggled with simple tasks (e.g., changing a width from 50px to 100px), proposing overly complex solutions. The temptation to manually intervene was immense.

The Approach:

- I treated the AI like a junior I was pair programming with.

- Instead of taking over, I refined my prompts, corrected its course, and guided it to the simple, correct solution.

Why? This adhered to the project's experimental goal and provided deep insight into the AI's strengths (boilerplate, discovery) and weaknesses (context, simple edits). This was an exercise in patience and mentorship.
-->

---

## Challenge 3: Becoming an AI-Assisted Artist

<div class="container">
<div style="flex:2">

- Needed many icons/images for Chrome Store
- Used AI to generate SVGs, then converted to PNGs
- Automated image resizing with script

</div>
<div class="col">

<img src="images/icon-128.png" alt="ext-icon" width="256" style="padding-left: 24px;margin-left:24px;">

</div>
</div>

<!--
The Problem: The Chrome Store requires numerous icons and promotional images, but I'm not an artist.
The Process:

1. Experiment: Used an AI to create icon concepts as SVGs, iteratively refining them with prompts ("make the handle longer").

2. Roadblock: Discovered the Chrome Store does not accept SVG files.

3. Pivot: I had a perfect vector source but needed dozens of specific PNG sizes.

4. Automation: Prompted the AI to write a command-line script to take the master SVG and automatically convert it into all required PNG dimensions.
-->

---

## Challenge 4: The Publishing Gauntlet

- Used Gemini for permission justifications
- Chrome Web Store review was slow and strict
- Careful with updates to avoid extra waiting for approvals

<!--
The Problem: The Google Chrome Web Store review process.

Key Hurdles:
- Manual Review: Due to the powerful permissions required, the extension was flagged for a mandatory human review.
- Slow Iteration Cycle: Each submission, even for a minor text change on the store page, took up to half a week for approval.
- Thorough Justification: Required detailed explanations for why each permission was necessary.

How I Overcame It:
- Used Gemini to help draft clear, concise justifications for the reviewers.
- Learned to plan submissions to minimize delays.
-->

---

## Final Outcome & Impact

### Published, Private, and Polished

- ✅ Extension published and meets all goals
- ✅ 100% source-available, private, verifiable
- ✅ Learned full Chrome extension lifecycle
- ✅ Learned a lot more about interactions with Copilot

<!--
Project Goals Achieved:

- Fully functional extension that meets all core and evolved requirements
- Published and available on the official Google Chrome Web Store
- 100% source-available, private, and verifiable, with clean, auditable code
- Professional-looking assets and a complete store listing

Personal Impact:

- Gained a deep, practical understanding of AI-assisted development workflows
- Learned the entire modern Chrome extension development and publishing lifecycle
-->

---

## Key Takeaways

- AI accelerates, but doesn’t replace expertise
- Simplicity is its own feature
- Personal projects = high learning, low risk

<!--
On AI Development: AI is a powerful accelerator, not a replacement for engineering expertise. The senior developer's role shifts towards architecture, review, and precise prompt engineering.

On Privacy: Building trustworthy software requires deliberate choices. Simplicity and transparency (like using plain JS) are features in themselves.

On Personal Projects: They are invaluable for exploring new technologies and processes in a low-risk, high-learning environment.
-->

---

## Questions?

**Links:**
- **GitHub Repo:** [github.com/abaines/search-extension](https://github.com/abaines/search-extension)
- **Chrome Store:** [OpenHighlighter](https://chromewebstore.google.com/detail/openhighlighter/keflkfcjfkljbafefaemchogmlnanjgi)
- **LinkedIn:** [in/alan-baines](https://www.linkedin.com/in/alan-baines)
- **This presentation:** [abaines.github.io/marp-search-extension](https://abaines.github.io/marp-search-extension)

## Thank You! 🍰

<!--
Credits:
Marp-team for Marp, which has been awesome!
Github Copilot
Gemini
-->

