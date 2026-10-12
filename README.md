# Daily Tech News Digest

An email-only digest of 5–8 recent stories about technology, AI, cybersecurity, and startups. It uses RSS feeds for source links, Gemini for plain-language summaries, Gmail SMTP for delivery, and GitHub Actions for the daily schedule.

## Preferences

- Schedule: 8:00 AM every day, Asia/Kolkata
- Topics: top technology news, AI, cybersecurity, startups
- Language and style: clear, beginner-friendly English
- Delivery: email

## GitHub Actions setup

1. Create a **private** GitHub repository and upload this folder's contents to its root (including `.github/workflows/daily-digest.yml`).
2. In the repository, open **Settings → Secrets and variables → Actions → New repository secret**. Add the secrets listed below. Never put secret values in source files or commit them.
3. Create a Gemini API key in Google AI Studio and save it as `GEMINI_API_KEY`.
4. For Gmail delivery, turn on 2-Step Verification on the sending Google account, create an App Password, then save it as `SMTP_APP_PASSWORD`. Use the sending Gmail address as `SMTP_USERNAME`.
5. Add `EMAIL_TO` with the destination email address. Optionally add `EMAIL_FROM`; it normally can be the same as `SMTP_USERNAME`.
6. Open the **Actions** tab and enable workflows if GitHub prompts you. Run **Daily tech news digest → Run workflow** once to check setup.

Required repository secrets: `GEMINI_API_KEY`, `SMTP_USERNAME`, `SMTP_APP_PASSWORD`, `EMAIL_TO`.

Optional secret: `EMAIL_FROM`.

## Schedule and limitations

The workflow uses GitHub's schedule trigger with the `Asia/Kolkata` timezone. GitHub Actions may delay scheduled jobs during high load, so an 8:00 AM schedule is not guaranteed to start precisely at 8:00. Keep secrets in GitHub's encrypted repository secrets. Free service quotas and model availability can change. Check current Gemini API pricing and GitHub Actions included usage before enabling any paid billing.

The workflow currently uses `gemini-3.8-flash`. Headlines, publishers, timestamps, and source links are retained from the RSS feeds; Gemini writes short summaries based on each feed's title and description.

## Files

- `main.py`: fetches feed items, asks Gemini to select and summarize stories, and emails the digest.
- `.github/workflows/daily-digest.yml`: daily and manual GitHub Actions triggers.
