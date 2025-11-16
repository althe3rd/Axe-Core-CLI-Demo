# Axe-Core CLI Demo

A demonstration project showing how to use `@axe-core/cli` to detect accessibility issues and prevent deployments when violations are found.

## 🎯 Purpose

This project demonstrates:
- How to integrate axe-core CLI into your development workflow
- How to automatically block deployments when accessibility issues are detected
- Common accessibility violations and how they appear in axe reports
- Setting up GitHub Actions for automated accessibility testing

## 🚀 Quick Start

### 1. Install Dependencies

```bash
npm install
```

### 2. Run Accessibility Tests Locally

```bash
# Run axe-core and exit with error if issues found (using file:// protocol)
npm run test:a11y

# Generate a detailed JSON report
npm run test:a11y-report

# Or test with a local server (recommended for CI/CD simulation)
npm run test:a11y-server
```

### 3. Serve Locally (Optional)

```bash
npm run serve
```

Then visit http://localhost:8080

## 🐛 Intentional Accessibility Issues

This demo page contains the following accessibility violations:

1. **Missing h1 / Skipped Heading Levels** - Uses h3 instead of h1 for main heading
2. **Form Inputs Without Labels** - Text and email inputs lack associated labels
3. **Button Without Accessible Text** - Submit button has no text or aria-label
4. **Images Without Alt Text** - All images in the gallery are missing alt attributes
5. **Low Contrast Text** - Gray text on light gray background fails WCAG contrast requirements
6. **Non-Descriptive Link Text** - "click here" link doesn't describe destination
7. **Empty Heading** - h2 element with no content
8. **Improper Interactive Element** - Div with onclick instead of proper button/link

## 📊 Understanding the Output

When you run `npm run test:a11y`, you'll see output like:

```
Running axe-core on index.html

Violation of "color-contrast" with 1 occurrences!
  Impact: serious
  Description: Ensures the contrast between foreground and background colors...
  
Violation of "image-alt" with 3 occurrences!
  Impact: critical
  Description: Ensures <img> elements have alternate text...

# Additional violations...

Process exited with code 1
```

The `--exit` flag causes the command to exit with a non-zero code when violations are found, which blocks the deployment pipeline.

## 🔄 CI/CD Integration

The `.github/workflows/a11y-check.yml` file demonstrates:

1. **Automated Testing** - Runs on every push and pull request
2. **Deployment Blocking** - Deploy job only runs if accessibility tests pass
3. **Artifact Upload** - Saves accessibility report for review when tests fail

### Setting Up GitHub Pages Deployment

1. Push this repository to GitHub
2. Go to Settings → Pages
3. Source: Deploy from a branch
4. Branch: `gh-pages`

Once set up, the workflow will:
- ✅ Run accessibility tests on every push
- ❌ Block deployment if issues are found
- 🚀 Deploy to GitHub Pages only when all tests pass

## 🎬 Demo Script for Screen Recording

### Part 1: Show the Issues

1. Open `index.html` in a browser
2. Point out the visible accessibility problems (low contrast, missing labels, etc.)

### Part 2: Run Axe-Core CLI

```bash
npm run test:a11y
```

3. Show the detailed error output
4. Explain the severity levels (critical, serious, moderate, minor)
5. Show how the command exits with code 1 (deployment would be blocked)

### Part 3: Generate Detailed Report

```bash
npm run test:a11y-report
cat results.json
```

6. Show the JSON report with detailed information for each violation

### Part 4: Demonstrate Deployment Protection

```bash
npm run deploy
```

7. Show how the deployment script fails due to accessibility issues
8. Explain that in CI/CD, this would prevent code from reaching production

### Part 5: Show GitHub Actions (Optional)

9. Navigate to the Actions tab on GitHub
10. Show a failed workflow run
11. Show the accessibility report artifact

## 🔧 Fixing the Issues

To demonstrate remediation, you could fix issues one by one:

### Example: Fix Missing Alt Text

```html
<!-- Before -->
<img src="https://via.placeholder.com/150">

<!-- After -->
<img src="https://via.placeholder.com/150" alt="Placeholder image 1">
```

Then re-run tests to show fewer violations.

## 📚 Additional Resources

- [axe-core CLI Documentation](https://github.com/dequelabs/axe-core-npm/tree/develop/packages/cli)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Deque University](https://dequeuniversity.com/)

## 🎓 Teaching Points

- Accessibility testing should be automated, not manual
- Catching issues early prevents costly remediation later
- Accessibility is not optional - it's a legal and ethical requirement
- axe-core helps teams maintain accessibility standards consistently
- CI/CD integration ensures accessibility is part of the definition of "done"

## 📝 License

MIT

