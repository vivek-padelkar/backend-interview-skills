# Deployment Guide

## Skill Ready for Deployment ✅

Your backend-interview skill is now prepared for deployment to skills.sh with all necessary files in place.

## Directory Structure

```
backend-interview/
├── SKILL.md                          # Main feature documentation
├── README.md                         # Quick start & overview
├── skill.yaml                        # Deployment metadata
├── CHANGELOG.md                      # Version history
├── LICENSE                           # MIT License
├── DEPLOYMENT.md                     # This file
├── evals/
│   └── evals.json                   # Evaluation metrics
└── references/
    ├── question-bank.md             # Question library
    ├── company-styles.md            # Company profiles
    └── resources.md                 # Learning resources
```

## Files Created for Deployment

### Core Files
- **skill.yaml** — Metadata, version, tags, triggers, requirements
- **README.md** — Quick start guide and feature overview
- **SKILL.md** — Full documentation (already existed)
- **LICENSE** — MIT License
- **CHANGELOG.md** — Version tracking

### Supporting Files
- **evals/evals.json** — Evaluation metrics for skill performance
- **references/** — Question bank, company styles, learning resources

## Next Steps

### 1. Create skills.sh Account (if not done)
- Go to https://www.skills.sh/
- Sign up or log in
- Navigate to "Publish" or "Dashboard"

### 2. Prepare for Upload
- Ensure all files are in `/Users/vivekpadelkar/.claude/skills/backend-interview/`
- Verify skill.yaml metadata (check author email matches your account)
- Optional: Update repository URL in skill.yaml if you have a GitHub repo

### 3. Deploy to skills.sh
Follow skills.sh documentation for deployment:
- **Option A: Web UI** — Upload skill zip from dashboard
  ```bash
  cd /Users/vivekpadelkar/.claude/skills/
  zip -r backend-interview.zip backend-interview/
  # Upload backend-interview.zip via skills.sh web dashboard
  ```

- **Option B: CLI (if available)**
  ```bash
  skills deploy /Users/vivekpadelkar/.claude/skills/backend-interview
  ```

- **Option C: API** — Use skills.sh API with your auth token
  ```bash
  curl -X POST https://api.skills.sh/deploy \
    -H "Authorization: Bearer YOUR_API_TOKEN" \
    -F "skill=@backend-interview.zip"
  ```

### 4. Verify Deployment
- Check skills.sh profile for published skill
- Test skill invocation: `/backend-interview`
- Verify all triggers work correctly

### 5. Promote & Share
- Add skill link to your portfolio
- Share on social media
- List on relevant platforms

## Metadata Reference

**skill.yaml** contains:
- **name:** backend-interview
- **version:** 1.0.0
- **author:** Vivek Padelkar
- **description:** Full Node.js backend engineer mock interview
- **license:** MIT
- **triggers:** Multiple natural language triggers for invocation
- **topics:** 8 backend engineering topics
- **experience_levels:** 4 levels (Junior, Mid, Senior, Staff)
- **company_styles:** 5 company interview styles
- **difficulty_levels:** 3 levels (Easy, Medium, Hard)

## Questions Before Deployment?

1. **API Key?** — Check skills.sh account settings → "API Keys"
2. **Repository URL?** — Update `repository` field in skill.yaml if deploying with GitHub
3. **Contact support** — skills.sh should have docs at /docs or support email

## After Deployment

- Monitor usage analytics on skills.sh dashboard
- Collect user feedback and reviews
- Plan updates for v1.1.0+ in CHANGELOG.md
- Consider adding more question scenarios as usage grows

---

**Ready to deploy?** Follow the steps above for your preferred deployment method.
