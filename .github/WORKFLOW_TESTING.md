# Workflow Testing Guide

This document describes how to test the README Anti-Spam workflow.

## Prerequisites

Before testing, ensure:
1. The `OPENAI_API_KEY` secret is configured in the repository settings
2. The workflow file is committed to the `.github/workflows/` directory
3. Labels `spam`, `unknown`, and `none` exist in the repository (GitHub will create them automatically if they don't exist)

## Test Scenarios

### Test 1: Legitimate README Changes

**Action**: Create a PR that adds documentation or legitimate content to README.md

**Expected Result**:
- Workflow runs successfully
- PR is labeled with `none`
- Comment is added: "✅ The changes to README.md appear to be legitimate."

### Test 2: Spam/Promotional Content

**Action**: Create a PR that adds obvious spam content (e.g., "Buy our product at www.example.com!!!")

**Expected Result**:
- Workflow runs successfully
- PR is labeled with `spam`
- Comment is added: "⚠️ The changes to README.md appear to be spam or promotional content."

### Test 3: Unclear/Suspicious Changes

**Action**: Create a PR with unclear or suspicious changes

**Expected Result**:
- Workflow runs successfully
- PR is labeled with `unknown`
- Comment is added: "⚠️ The changes to README.md are unclear or suspicious. Please review manually."

### Test 4: No README Changes

**Action**: Create a PR that doesn't modify README.md

**Expected Result**:
- Workflow doesn't run (due to path filter)

## Manual Testing Steps

1. Create a test branch:
   ```bash
   git checkout -b test/readme-spam-check
   ```

2. Modify README.md with test content:
   ```bash
   echo "Test content for spam detection" >> README.md
   ```

3. Commit and push:
   ```bash
   git add README.md
   git commit -m "Test: Add content to README"
   git push origin test/readme-spam-check
   ```

4. Create a pull request on GitHub

5. Monitor the workflow execution in the "Actions" tab

6. Verify the label and comment are added correctly

## Troubleshooting

If the workflow fails:

1. Check the workflow logs in the Actions tab
2. Verify the `OPENAI_API_KEY` secret is correctly configured
3. Ensure the API key has sufficient credits
4. Check network connectivity to OpenAI API
5. Verify the Vercel AI SDK and OpenAI SDK are compatible

## Notes

- The workflow only triggers when README.md is modified in a PR
- The workflow requires `OPENAI_API_KEY` to be set as a repository secret
- The AI analysis uses OpenAI's GPT-4 model via the Vercel AI SDK
- The workflow automatically handles multiline diffs
