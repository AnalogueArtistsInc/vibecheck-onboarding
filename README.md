# VibeCheck Client Onboarding

Standalone client profile wizard for VibeCheck commercial onboarding. Deployed as a static site via GitHub Pages.

## Setup

### 1. Create the Supabase table

Run `scripts/supabase_client_profiles_setup.sql` (from the main VibeCheck_Unified repo) in your Supabase SQL Editor.

### 2. Configure the anon key

In `index.html`, replace `YOUR_SUPABASE_ANON_KEY` with your Supabase project's anon key:

```js
const SUPABASE_ANON_KEY = 'eyJ...your-anon-key...';
```

The anon key is safe to embed publicly — RLS restricts it to INSERT-only on the `client_profiles` table.

### 3. Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings > Pages**
3. Set Source to **Deploy from a branch**, select `main` / `root`
4. The wizard will be available at `https://<username>.github.io/vibecheck-onboarding/`

### 4. Share with clients

Send the link to clients along with the access code: **vibecheck**

## How it works

- Client opens the link and enters the access code
- Fills out the 8-section music profile wizard
- On submit, profile is inserted directly into Supabase via the anon key
- The VibeCheck instance pulls profiles using `ClientProfileService.pull_from_supabase()` with the service_role key
- Themes are generated locally on the VibeCheck instance
