# arthlabs — TODO

**Type:** EdTech Web App (AI-Powered Educational Platform)  
**Stack:** HTML/CSS/JS, Firebase, Gemini 2.5 Pro API  
**Status:** ~20% complete (frontend only, no backend)

---

## Actions To Take

- [ ] **Refactor monolithic `index.html` into modular structure** — Split into components using plain JS modules or a lightweight framework (Vite); move to `src/` with a proper build process
- [ ] **Create Firebase Cloud Functions backend** — Implement server-side functions for Gemini API calls, image generation, and quiz generation; never expose API keys to the frontend
- [ ] **Move API keys to Firebase Secrets / Cloud Functions** — Remove any hardcoded keys from `index.html`; proxy all AI API calls through Cloud Functions with proper rate limiting
- [ ] **Add unit and integration tests** — Set up Jest or Vitest for component logic and Firebase function tests; add a GitHub Actions workflow to run them on push
- [ ] **Document local development setup** — Create `DEVELOPMENT.md` with Firebase Emulator setup, local run instructions, `.env.local` template, and staging vs production deploy workflow
