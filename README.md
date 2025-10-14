# test-readme-antispam
@nonexistinguser
This repository includes automated spam detection for the README.md file using @vercel/ai-action.

## How It Works

The spam detection workflow is triggered automatically when:
- A pull request modifies the README.md file

The workflow:
1. Checks out the code with full git history
2. Gets the git diff between the PR and the destination branch for README.md
3. Passes the diff to @vercel/ai-action for analysis
4. The AI categorizes the changes as: **spam**, **unknown**, or **none**

The workflow uses AI to analyze the README changes and detect potential spam based on:
- Excessive promotional content
- Unrelated links or advertisements
- Suspicious URLs or phishing attempts
- Repetitive content
- Content not related to the project
- Malicious links

## Configuration

The workflow uses `@vercel/ai-action@v2` with the following configuration:
- **prompt**: Instructions for the AI to analyze the git diff and categorize spam
- **schema**: JSON schema that structures the output with `type` and `reason` fields
- **model**: `openai/gpt-4o` for AI-powered analysis
- **api-key**: Uses `AI_GATEWAY_API_KEY` secret for authentication

## Workflow Output

The spam detection is implemented in `.github/workflows/spam-detection.yml` and uses `@vercel/ai-action` to analyze the README changes and provide structured JSON output:

```json
{
  "analysis": {
    "type": "spam" | "unknown" | "none",
    "reason": "Brief explanation"
  }
}
```

- **type**: The classification of the changes (spam, unknown, or none)
- **reason**: An explanation of why the changes were flagged
