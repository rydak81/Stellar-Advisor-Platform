# GitHub & Vercel Setup Guide
## Step-by-Step Instructions for StellarAdvisor

---

## PART 1: Understanding the Structure

### How GitHub Organizes Files

Think of GitHub like a Google Drive folder specifically for code:

```
Your GitHub Account
└── stellar-advisor-platform (this is a "repository" or "repo")
    ├── index.html          ← The main website file
    ├── README.md           ← Description that shows on GitHub
    ├── docs/               ← Folder for documentation
    │   ├── ARCHITECTURE.md
    │   ├── ROADMAP.md
    │   └── CHANGELOG.md
    └── src/                ← Folder for source files
        └── data/
            └── agencies.json
```

**Key terms:**
- **Repository (repo):** A project folder on GitHub
- **Commit:** Saving changes (like "Save As" but tracks history)
- **Push:** Uploading your commits to GitHub
- **Branch:** A version of your code (we'll use "main")

---

## PART 2: Creating Your GitHub Repository

### Step 1: Create a GitHub Account (if needed)
1. Go to [github.com](https://github.com)
2. Click "Sign up"
3. Use your email
4. Choose username: something professional like `ryanbeaconpath`

### Step 2: Create New Repository
1. Once logged in, click the **+** icon (top right) → "New repository"
2. Fill in:
   - **Repository name:** `stellar-advisor-platform`
   - **Description:** "Lead generation platform connecting Amazon sellers with agencies"
   - **Public** (free tier, visible to all) or **Private** (only you see it)
   - ✅ Check "Add a README file"
3. Click **"Create repository"**

### Step 3: Upload Your Files
**Option A: Upload via Browser (Easiest)**
1. On your repo page, click **"Add file"** → **"Upload files"**
2. Drag ALL the files from the downloaded folder
3. Scroll down, type a message: "Initial platform upload"
4. Click **"Commit changes"**

**Option B: Use GitHub Desktop (Better for ongoing updates)**
1. Download [GitHub Desktop](https://desktop.github.com)
2. Sign in with your GitHub account
3. Clone your repo: File → Clone Repository → Select `stellar-advisor-platform`
4. Copy the project files into the cloned folder on your computer
5. In GitHub Desktop: Type commit message → Click "Commit to main" → Click "Push origin"

---

## PART 3: Connecting to Vercel

### Step 1: Create Vercel Account
1. Go to [vercel.com](https://vercel.com)
2. Click "Sign Up"
3. Choose **"Continue with GitHub"** (this links them automatically)
4. Authorize Vercel to access GitHub

### Step 2: Import Your Repository
1. On Vercel dashboard, click **"Add New..."** → **"Project"**
2. Find `stellar-advisor-platform` in the list
3. Click **"Import"**

### Step 3: Configure (Keep Defaults)
1. Framework Preset: Leave as "Other"
2. Root Directory: Leave as `./`
3. Build Command: Leave empty
4. Output Directory: Leave empty
5. Click **"Deploy"**

### Step 4: Wait for Deployment
- Takes 30-60 seconds
- You'll see a preview of your site
- Get your URL: something like `stellar-advisor-platform.vercel.app`

### Step 5: (Optional) Add Custom Domain
1. On your project, go to **Settings** → **Domains**
2. Add your domain: `stellaradvisor.com`
3. Follow DNS instructions (add CNAME record at your registrar)

---

## PART 4: Making Updates

### Simple Updates (Browser)
1. Go to your repo on github.com
2. Navigate to the file you want to edit
3. Click the **pencil icon** (Edit)
4. Make changes
5. Scroll down, add commit message: "Updated pricing section"
6. Click **"Commit changes"**
7. **Vercel automatically deploys!** (within 30 seconds)

### Bigger Updates (GitHub Desktop)
1. Open GitHub Desktop
2. Click "Fetch origin" (downloads latest)
3. Edit files in your local folder
4. Changes appear in GitHub Desktop
5. Type commit message
6. Click "Commit to main"
7. Click "Push origin"
8. Vercel auto-deploys

---

## PART 5: Best Practices

### Commit Messages
Write clear messages about what changed:
- ✅ "Added new agency partner: Canopy Management"
- ✅ "Fixed calculator margin calculation"
- ✅ "Updated hero section copy"
- ❌ "Update"
- ❌ "Changes"
- ❌ "asdfasdf"

### Folder Organization

```
stellar-advisor-platform/
├── index.html          # MAIN FILE - the website
├── README.md           # Project description
├── .gitignore          # Files to ignore
│
├── public/             # Static assets served directly
│   └── favicon.ico
│
├── src/                # Source files
│   ├── components/     # Reusable code (future)
│   ├── styles/         # CSS files (if separated)
│   └── data/           # JSON data files
│       └── agencies.json
│
├── docs/               # Documentation
│   ├── ARCHITECTURE.md # How it works
│   ├── ROADMAP.md      # Future plans
│   └── CHANGELOG.md    # Version history
│
└── assets/             # Media
    ├── images/
    └── icons/
```

### When to Create New Files vs Edit

| Scenario | Action |
|----------|--------|
| Fix a typo | Edit existing file |
| Change colors/styling | Edit index.html |
| Add new agency | Edit agencies.json |
| Add new tool | Create new section in index.html |
| Separate CSS | Create src/styles/main.css |
| Add documentation | Create file in docs/ |

---

## PART 6: Quick Reference

### URLs You'll Use
| Service | URL |
|---------|-----|
| GitHub repo | github.com/YOUR-USERNAME/stellar-advisor-platform |
| Vercel dashboard | vercel.com/dashboard |
| Live site | stellar-advisor-platform.vercel.app |

### Common Tasks

**Edit the main page:**
1. GitHub → index.html → Edit → Commit

**Add an agency to the database:**
1. GitHub → src/data/agencies.json → Edit → Add entry → Commit

**Check deployment status:**
1. Vercel dashboard → Click project → See deployments

**View previous versions:**
1. GitHub → Commits → Click any commit to see that version

---

## Troubleshooting

### "My changes aren't showing"
- Wait 30-60 seconds for Vercel to deploy
- Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
- Check Vercel dashboard for errors

### "I broke something"
- Go to GitHub → Commits
- Find the last working commit
- Click "..." → "Revert changes"
- This creates a new commit undoing the broken one

### "I can't find my file"
- Make sure you committed AND pushed
- Check you're on the right branch (should be "main")

---

## Next Steps

1. ✅ Download the project files
2. ✅ Create GitHub account
3. ✅ Create repository
4. ✅ Upload files
5. ✅ Connect Vercel
6. ✅ Test your live site
7. 🎯 Connect forms to Airtable (next step)

---

*Questions? The README.md in your repo has additional documentation.*
