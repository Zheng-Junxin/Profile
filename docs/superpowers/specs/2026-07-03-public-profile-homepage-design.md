# Public Profile Homepage Design

## Goal

Convert the existing resume project into a polished public personal profile website for Zheng Junxin. The page should feel like a professional homepage rather than a paper resume, while still keeping the useful resume content already present in the repository.

## Scope

- Rebuild the project as a static GitHub Pages friendly site using the existing `index.html`, `avatar.jpg`, and `transcript.pdf`.
- Keep all Chinese content as valid UTF-8 and verify the final page contains no mojibake.
- Add the work experience requested by the user:
  - `2026.07.01-至今 深圳市盛能杰科技有限公司 嵌入式软件工程师`
- Keep the site as plain static HTML/CSS/JavaScript. No React, Vue, build step, package manager, or external deployment dependency.
- Preserve links to the transcript PDF and existing contact information.

## Page Structure

1. Header navigation
   - Name/brand text.
   - Anchor links for About, Experience, Skills, Projects, Honors, Contact.

2. Hero
   - Prominent name: `郑俊鑫`.
   - Role: `嵌入式软件工程师`.
   - Short profile summary focused on embedded software, STM32/HAL/RTOS, hardware debugging, PCB experience, and practical AI-assisted development.
   - Avatar image from `avatar.jpg`.
   - Primary actions: contact by email, view transcript.

3. Highlights
   - Compact facts such as university, major, GPA/ranking, CET-6, location, and technical focus.

4. Work Experience
   - Place before education and projects because this is now the newest professional credential.
   - Show the Shenzhen Shengnengjie Technology role with date range and title.
   - Use concise responsibility bullets appropriate for an embedded software engineer profile. If no detailed duties are provided, keep them conservative and general.

5. Education
   - 汕头大学, 电子与计算机工程本科, 2022.10-2026.06.
   - GPA 3.63/5.0, professional ranking 13.33%.
   - Transcript link to `transcript.pdf`.
   - Core courses already present in the original page.

6. Skills
   - Group skills instead of showing one long tag row:
     - Embedded software: STM32, HAL, RTOS, C/C++.
     - Hardware and PCB: EDA, AD, Multisim, Proteus.
     - Software and AI: Python, PyTorch, Scikit-learn, MySQL, Redis, AI Agent development.

7. Projects
   - Present selected projects as readable cards/sections:
     - AI resume optimization website.
     - Ultrasonic vehicle speed measurement system based on frequency difference.
     - Agent-based intelligent recruitment matching website.
     - Deep learning parasite diagnosis system.
     - STM32 tracking and obstacle avoidance car.
   - Keep project descriptions concise and outcome-oriented.

8. Honors
   - Keep current honors, correcting all Chinese encoding.

9. Contact / Footer
   - Phone, email, location, personal website link.
   - Include copyright or simple closing text.

## Visual Direction

- Use a clean public homepage layout with a strong hero section, restrained professional colors, and clear spacing.
- Avoid a traditional resume sheet container as the main visual form.
- Use responsive layout: desktop two-column hero, mobile single-column stacking.
- Keep cards modest and avoid nested card structures.
- Use local assets where possible. Font Awesome may be removed or replaced with text/icons if it complicates loading.

## Behavior

- Anchor links should scroll to page sections.
- Transcript link opens `transcript.pdf` in a new tab.
- Email action uses `mailto:2323857919@qq.com`.
- The page should work by opening `index.html` directly and through a static web server.

## Verification

- Validate that `index.html` contains no mojibake strings such as `閮`, `涓`, `鍩`, or the Unicode replacement character.
- Verify required content appears:
  - `郑俊鑫`
  - `嵌入式软件工程师`
  - `深圳市盛能杰科技有限公司`
  - `2026.07.01-至今`
  - `transcript.pdf`
  - `avatar.jpg`
- Verify HTML parses with a lightweight script or browser check.
- Start a local static server and confirm the page returns HTTP 200.
- Inspect the page at desktop and mobile widths where practical.
