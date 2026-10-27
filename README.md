# Ad comments

Single-page tool to view, hide, delete and reply to comments on Meta ads (Facebook + Instagram, including page-backed Instagram accounts) across every ad account a token can see.

Static HTML, no build step. Deployed on Vercel.

## Token

Use a Business Manager **system user** token so it never expires:

1. business.facebook.com → Settings → Users → System users → Add (Admin)
2. Assign assets: all ad accounts (Manage) and all Pages (Full control)
3. Generate token → pick/create an app → permissions:
   `ads_read`, `ads_management`, `pages_read_engagement`, `pages_manage_engagement`, `pages_show_list`, `instagram_basic`, `instagram_manage_comments` → expiry Never
4. Paste into the app. Stored in the browser's localStorage only.

## Limits (Meta-side)

- Advantage+ catalog ads and Stories can't be moderated via the API
- Replying from a page-backed Instagram account isn't possible (hide/delete work)
