# Learnliftt: deploy with the AI service on your own domain

This folder is a complete site: `index.html` (the app) and `netlify/functions/ai.js` (a small server function that
calls the AI model). Your API key lives only on the server and is never sent to the browser.

## Deploy (Netlify)
1. Put this folder in a GitHub repository (or use the Netlify CLI: `npm i -g netlify-cli`, then `netlify deploy --prod`).
2. In Netlify choose **Add new site > Import an existing project**, pick the repo.
   Build command: leave empty. Publish directory: `.` (already set in `netlify.toml`).
3. Open **Site configuration > Environment variables** and add:
   - `ANTHROPIC_API_KEY` (required): your key from console.anthropic.com
   - `AI_MODEL` (optional): defaults to `claude-sonnet-5-5`
   - `ALLOWED_ORIGIN` (optional): e.g. `https://learnliftt.netlify.app`, so other sites cannot use your key
   - `DAILY_LIMIT_PER_IP` (optional): defaults to 60 requests per visitor per day
4. Redeploy. Open the site, go to **AI Study Studio**, upload notes and press Generate.

Notes
- Every generation uses your API credits. Set a spending limit in your Anthropic console.
- The per-visitor limit is best effort (it resets when the function restarts). For a public launch add real
  logins and server-side rate limits.
- I have not verified that Netlify's drag-and-drop upload includes functions. Use Git or the CLI.
- Until the function is deployed, the app shows clearly labelled sample content instead of AI content.
