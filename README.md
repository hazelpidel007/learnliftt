# Learnliftt

**Stop searching. Start studying.**

Learnliftt is a study navigator for college students. Instead of answering questions like a chatbot, it tells a student **what to study, from which resource, in what order, and how ready they are**. It was built for the Pitch Pulse 2026 innovation competition.

Live prototype: https://learnliftt.netlify.app

## The problem

Students have hundreds of PDFs, slides, videos and past papers, but no clear order to study them in. The gap is not access to information. It is prioritization.

## What it does

- **Accounts:** sign up with name, college, branch, semester and the way your college shares material. Each account starts empty at 0%.
- **Upload your material:** upload a syllabus or notes as PDF, Word, TXT or Markdown. Files are read in the browser and topics are ranked High, Medium or Low.
- **Smart Search and Study Path:** a sentence such as "I have CAT tomorrow..." becomes an exam, topic, level, time and priority, then a ranked, time-boxed path.
- **Study Plan:** plans add up exactly to the time you have. Edit durations, reorder, add or delete blocks, and shift the start time.
- **Pomodoro study sessions:** pressing Start on a block opens a session with a countdown beside your document, the AI lesson, puzzles and questions.
- **AI Study Studio:**
  - AI Teacher: a simple lesson with voice narration, which can be saved as a captioned video
  - Memory puzzles: mnemonics, matching and flashcards
  - Mind maps
  - Level Up: five levels from recall to college-exam style, with AI feedback on written answers
  - Assignment coach: an outline, marking guide and common mistakes. The student writes their own answer.
- **Exports and feedback:** PDF export for puzzles, mind maps and questions, and a "report this as wrong" button.
- **Progress:** readiness, topic mastery, weak areas and an automatic recovery plan.
- **Sample material:** a "Try sample material" button loads demo notes, useful for presentations.

## Tech stack

| Layer | Details |
|---|---|
| Front end | Single-file HTML, CSS and vanilla JavaScript (no build step) |
| Storage | Browser `localStorage`, one record per account |
| AI | Anthropic Claude API, called through a Netlify Function so the key stays on the server |
| Libraries (via cdnjs) | PDF.js 3.11.174, Mammoth.js 1.6.0, QRCode.js 1.0.0, jsPDF 2.5.1 |
| Hosting | Netlify (static site + serverless function) |

## Project structure

```text
index.html                    the whole app
netlify.toml                  Netlify settings
netlify/functions/ai.js       server function that calls the AI model
README.md
```

## Run locally

1. Download or clone the repository.
2. Serve the folder, for example `python3 -m http.server 8000`, and open http://localhost:8000.
3. For AI features, install the Netlify CLI (`npm i -g netlify-cli`), set your key and run `netlify dev`. Without the function, the app shows clearly labelled sample content instead of AI content.

## Deploy to Netlify

1. Push this folder to a GitHub repository.
2. In Netlify choose **Add new site, then Import an existing project**. Leave the build command empty and set the publish directory to `.`.
3. Under **Site configuration, then Environment variables**, add:
   - `ANTHROPIC_API_KEY` (required)
   - `AI_MODEL` (optional, defaults to `claude-sonnet-5-5`)
   - `ALLOWED_ORIGIN` (optional, for example `https://learnliftt.netlify.app`)
   - `DAILY_LIMIT_PER_IP` (optional, defaults to 60)
4. Redeploy and test AI Study Studio.

Every AI generation uses API credits, so set a spending limit in your Anthropic console.

## What is real and what is simulated

- **Real:** accounts, uploads, topic extraction, study plans, timers, study sessions, progress tracking, PDF export and AI content generation.
- **Simulated or limited:**
  - Resource ranking and the readiness formula are simple prototype logic and have not been validated against real exam results.
  - The "video" is an animated lesson with captions, not AI-generated footage.
  - Accounts and passwords are stored in the browser only. A real launch needs a backend with proper authentication.
  - Scanned PDFs cannot be read, because there is no OCR.
  - AI-generated content can contain mistakes and should be reviewed.

## Colleges and portals

Different colleges use different systems, so Learnliftt is designed around connectors (university portal, Moodle, Google Classroom, Canvas, or syllabus upload). Live portal sync, such as VTOP, needs each college's approval and an official integration (LMS API, LTI or single sign-on). It is not built. Students currently import material by uploading it.

## Roadmap

1. Pilot with one class at VIT-AP.
2. Faculty-verified resources and a validated readiness model.
3. College connectors, a proper backend and login, and department-level analytics.

## References

- Anderson, L. W., & Krathwohl, D. R. (Eds.). (2001). *A taxonomy for learning, teaching, and assessing.* Longman.
- Cirillo, F. (2018). *The Pomodoro Technique.* Currency.
- Dunlosky, J., et al. (2013). Improving students' learning with effective learning techniques. *Psychological Science in the Public Interest, 14*(1), 4-58.
- Mayer, R. E. (2009). *Multimedia learning* (2nd ed.). Cambridge University Press.
- Roediger, H. L., & Karpicke, J. D. (2006). Test-enhanced learning. *Psychological Science, 17*(3), 249-255.
- Sweller, J. (1988). Cognitive load during problem solving. *Cognitive Science, 12*(2), 257-285.

## Author

Abheek Guha Ray [CODEHORIZON], VIT-AP University, Computer Science & Engineering.

## License

Add your preferred license here (for example MIT) before publishing the repository.
