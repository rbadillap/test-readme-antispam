# test-readme-antispam

This repository includes automated spam detection for the README.md file using @vercel/ai-action.

## How It Works

The spam detection workflow is triggered automatically when:
- The README.md file is updated via push
- A pull request modifies the README.md file

The workflow uses AI to analyze the README content and detect potential spam based on:
- Excessive promotional content
- Unrelated links or advertisements
- Suspicious URLs or phishing attempts
- Repetitive content
- Content not related to the project
- Malicious links

## Workflow

The spam detection is implemented in `.github/workflows/spam-detection.yml` and uses `@vercel/ai-action` to analyze the README content and provide:
1. Classification (SPAM or NOT_SPAM)
2. Confidence score (0-100)
3. Brief explanation of the decision