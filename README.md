# Cutting downtime tracker

Single-file web app. No build step, no npm. Drop `index.html` into any static host and it runs.

## Files

- **`index.html`** — the entire app. This is the only file that needs to be served.
- **`schema.sql`** — run this once in Supabase to create the tables. Covered in the "Supabase setup" section below.

## Deploy to GitHub Pages

1. Create a new repo on GitHub (public, any name).
2. Upload `index.html` to the root of the repo. (Drag-and-drop in the GitHub web UI works fine.)
3. Repo → **Settings → Pages**
4. Under **Build and deployment → Source**, pick **Deploy from a branch**.
5. Branch: `main`, folder: `/ (root)`. Save.
6. Wait ~30 seconds. Your app is live at `https://<your-username>.github.io/<your-repo>/`.

That's it. No Actions workflow, no build pipeline.

## Supabase setup (do this before first use)

1. Create a free Supabase project at [supabase.com](https://supabase.com).
2. Open **SQL Editor → New query**. Paste the contents of `schema.sql`. Run it.
3. **Settings → API** — copy the **Project URL** and the **anon public** key.
4. Open your live app in a browser. It'll ask for the URL and key the first time.
5. Paste them in and hit "Save and connect". They're stored in localStorage on that device only.

## How it works

- The app is a single HTML file with inline CSS and a module `<script>` that imports `@supabase/supabase-js` from the esm.sh CDN.
- Credentials are saved in localStorage per browser. Each tablet/laptop sets them up once.
- Click ⚙ Settings in the top right to change or clear credentials later.
- All session data lives in Supabase — anyone with the same credentials sees the same data.

## Security note

The anon key is safe in a browser because Row Level Security in the schema restricts what clients can do. For a production multi-factory setup, replace the `anon` RLS policies with auth-scoped ones and wire up Supabase Auth.
