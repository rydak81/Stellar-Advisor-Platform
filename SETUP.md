# Setup Guide: GitHub → Vercel

## Quick Start (5 Minutes)

### Step 1: Create GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon (top right) → **New repository**
3. Configure:
   - **Name:** `stellar-advisor`
   - **Description:** `Lead generation platform for Amazon sellers`
   - **Visibility:** Public or Private
   - ✅ Check "Add a README file"
4. Click **Create repository**

### Step 2: Upload Files

**Option A: Browser Upload (Easiest)**
1. On your repo page, click **Add file** → **Upload files**
2. Drag ALL files from the project folder
3. Write commit message: `Initial platform upload`
4. Click **Commit changes**

**Option B: GitHub Desktop (Better for ongoing work)**
1. Download [GitHub Desktop](https://desktop.github.com)
2. Clone your repo: File → Clone Repository
3. Copy project files into the folder
4. Commit and push

### Step 3: Connect Vercel

1. Go to [vercel.com](https://vercel.com)
2. Click **Sign Up** → **Continue with GitHub**
3. Authorize Vercel
4. Click **Add New...** → **Project**
5. Find `stellar-advisor` → Click **Import**
6. Keep default settings → Click **Deploy**
7. Wait ~30 seconds for deployment

### Step 4: Get Your Live URL

After deployment, you'll get:
- **Production URL:** `stellar-advisor.vercel.app`
- **Dashboard:** `vercel.com/your-username/stellar-advisor`

---

## Making Updates

### Quick Edits (Browser)

1. Go to github.com/your-username/stellar-advisor
2. Click the file you want to edit (e.g., `index.html`)
3. Click the **pencil icon** (Edit)
4. Make changes
5. Scroll down, add message: `Updated hero copy`
6. Click **Commit changes**
7. **Vercel auto-deploys in ~30 seconds!**

### Bigger Changes (GitHub Desktop)

1. Open GitHub Desktop
2. Click "Fetch origin" (download latest)
3. Edit files in your code editor
4. Changes appear in GitHub Desktop
5. Write commit message
6. Click **Commit to main**
7. Click **Push origin**

---

## Custom Domain Setup

### In Vercel:

1. Go to your project dashboard
2. Click **Settings** → **Domains**
3. Add your domain: `stellaradvisor.com`
4. Follow DNS instructions

### At Your Domain Registrar:

Add these DNS records:

| Type | Name | Value |
|------|------|-------|
| A | @ | 76.76.21.21 |
| CNAME | www | cname.vercel-dns.com |

Wait 24-48 hours for propagation.

---

## Troubleshooting

### "Changes not showing"
- Wait 30-60 seconds for Vercel to redeploy
- Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
- Check Vercel dashboard for build errors

### "Deploy failed"
- Check Vercel dashboard → Deployments → Click failed deploy
- Look at build logs for errors
- Most common: typo in HTML or missing file

### "Can't push to GitHub"
- Make sure you committed first
- Check you're signed into GitHub Desktop
- Try: `git push origin main` in terminal

---

## Best Practices

### Commit Messages

Write clear, descriptive messages:
- ✅ `Add new FAQ question about pricing`
- ✅ `Fix calculator margin formula`
- ✅ `Update agency partner list`
- ❌ `Update`
- ❌ `Fixed stuff`

### Branching (Optional)

For bigger changes, create a branch:
1. GitHub Desktop → Branch → New Branch
2. Name it: `feature/new-calculator`
3. Make changes
4. Create Pull Request
5. Review and merge

This creates a preview URL in Vercel before going live.

---

## Resources

- [GitHub Docs](https://docs.github.com)
- [Vercel Docs](https://vercel.com/docs)
- [GitHub Desktop Guide](https://docs.github.com/en/desktop)
