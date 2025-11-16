# Quick Demo Steps

## Setup (Before Recording)

```bash
npm install
```

## Demo Script (During Recording)

### 1. Show the HTML Page
```bash
open index.html
```

Point out visible issues:
- Form fields without labels
- Low contrast text
- "Click here" link
- Images

### 2. Run Axe-Core CLI
```bash
npm run test:a11y
```

**Talking Points:**
- Shows all accessibility violations
- Exit code 1 means tests failed
- This would block deployment in CI/CD
- Different severity levels: critical, serious, moderate, minor

### 3. Generate Detailed Report (Optional)
```bash
npm run test:a11y-report
cat results.json | head -50
```

**Talking Points:**
- JSON format for integration with other tools
- Includes specific selectors to locate issues
- Can be used for trend analysis

### 4. Show Deployment Protection
```bash
npm run deploy
```

**Talking Points:**
- Deploy command only runs if tests pass
- In real CI/CD (GitHub Actions), this prevents bad code from reaching production
- Forces teams to fix accessibility issues before merging

### 5. Show GitHub Actions (if pushed to GitHub)
- Navigate to repository
- Click "Actions" tab
- Show workflow file
- Show how deployment job depends on accessibility test

## Key Messages for Students

1. **Shift Left**: Catch accessibility issues during development, not after deployment
2. **Automation**: Manual testing doesn't scale - automate it
3. **Standards**: axe-core tests against WCAG standards
4. **Prevention**: Block deployments to enforce quality gates
5. **DevOps**: Accessibility is part of CI/CD, not a separate concern

## Common Questions

**Q: Does this catch all accessibility issues?**
A: No, automated testing catches ~30-50% of issues. Manual testing still needed.

**Q: What if we need to temporarily bypass?**
A: You shouldn't, but technically could use `--allow-failure` flag. Not recommended.

**Q: How do we fix the issues?**
A: axe provides guidance, and you can reference WCAG documentation.

**Q: Performance impact?**
A: Minimal - usually adds seconds to build time.

