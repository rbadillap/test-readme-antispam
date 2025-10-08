# test-readme-antispam

This repository includes a GitHub Actions workflow that automatically analyzes README.md changes in pull requests to detect spam content using AI.

## Features

- **Automated Analysis**: When a pull request modifies the README.md file, the workflow automatically analyzes the changes.
- **AI-Powered Detection**: Uses Vercel AI SDK with OpenAI to categorize changes as:
  - `spam`: Changes appear to be spam, promotional content, or malicious
  - `unknown`: Changes are unclear or suspicious but not definitively spam
  - `none`: Changes are legitimate and not spam
- **Automatic Labeling**: Applies the appropriate label to the pull request based on the analysis
- **PR Comments**: Adds a comment to the pull request with the analysis results

## Setup

To use this workflow in your repository:

1. Copy the `.github/workflows/readme-antispam.yml` file to your repository
2. Add an `OPENAI_API_KEY` secret to your repository settings:
   - Go to Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `OPENAI_API_KEY`
   - Value: Your OpenAI API key
3. Ensure the workflow has the necessary permissions (already configured in the workflow file)

## How It Works

1. The workflow triggers on pull requests that modify `README.md`
2. It checks out the code and gets the diff of README.md changes
3. The diff is analyzed using the Vercel AI SDK with OpenAI's GPT-4
4. Based on the AI analysis, the PR is labeled and a comment is added

## Requirements

- OpenAI API key (stored as a repository secret)
- GitHub Actions enabled on your repository