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

## Billing overview (monday board view)

`billing/index.html` is a monday.com board view, served at `/billing/`. Same idea as the checklist app, but it runs on the whole board and is plain HTML plus the monday SDK. No build step, no Vibe.

It gives one tab per group plus a whole-board tab, and for each it shows:

- total paid, adspend budgeted, management owed, and whether the client is in credit or over-allocated
- live Meta spend, read from the Social Campaigns board by matching campaign names
- a forecast of how many campaigns the month will end up with, and the management each one should carry
- a recommended adspend and management figure per campaign: management is the same for every campaign and the rest of each payment goes to adspend
- a "what if we add more campaigns" row for planning

Management is a flat fee per campaign up to a cap per group (defaults 500 and 1500, change them under Settings in the view). Groups are months, named like "November 2026".

The forecast blends a weighted average of the last three months' campaign counts with this month's pace, leaning on the pace more as the month goes on. It is saved and holds still until someone clicks **Re-forecast** on the group, so recommendations don't shift every time a campaign is added. The view says when the saved forecast has drifted from what it would be now.

Finished campaigns are held at what they actually spent, and a running campaign is never recommended less than it has already spent.

### Board columns

Matched by title, case doesn't matter: `Amount Paid`, `Total Adspend Budget`, `Status`, `Start Date`, `End Date`. The first two are required.

### Install in monday

1. Developers → Create app → Features → add a **Board View**
2. Deployment: **External hosting**, URL `https://<this site's Vercel domain>/billing/`
3. OAuth & Permissions: add `boards:read`
4. Open the billing board → add view → Apps → pick the app

Open `/billing/?demo=1` in a normal browser tab to see it with made-up data.
