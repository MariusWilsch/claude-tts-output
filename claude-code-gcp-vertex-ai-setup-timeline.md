# Complete Timeline: Claude Code + GCP Vertex AI Setup

## Day 0: Initial Setup (15 minutes)

### 1. GCP Project Setup
```bash
gcloud config set project YOUR-PROJECT-ID
gcloud services enable aiplatform.googleapis.com
```

### 2. Request Claude Model Access
- Go to: https://console.cloud.google.com/vertex-ai/model-garden
- Search "Claude"
- Click each Claude model → "Request Access"
- ⏰ **Wait 24-48 hours for approval**

### 3. While Waiting: Set Up Auth
```bash
gcloud auth login
gcloud auth application-default login
```

---

## Day 1-2: Approval Wait

*Nothing to do - Google reviews your model access request*

---

## Day 2-3: First Configuration (5 minutes)

### 4. Configure Claude Code Environment
```bash
# Add to ~/.bashrc or ~/.zshrc
export CLAUDE_CODE_USE_VERTEX=1
export CLOUD_ML_REGION=global
export ANTHROPIC_VERTEX_PROJECT_ID=your-project-id

# Reload shell
source ~/.bashrc  # or ~/.zshrc
```

### 5. Test It
```bash
claude
# Type: /status
```

You should see Vertex AI connection confirmed.

---

## Day 3: Hit Rate Limits (Immediate)

### 6. Default Quota: 60 requests/minute
- You'll likely hit this quickly during active development
- Error: `RESOURCE_EXHAUSTED`, code 429

### 7. Request Quota Increase
- Go to: https://console.cloud.google.com/iam-admin/quotas
- Filter: "online_prediction"
- Find: `aiplatform.googleapis.com/online_prediction_requests_per_base_model`
- Click "Edit Quota"
- Fill form:
  - New limit: 200-500 QPM (or your need)
  - Justification: "Software development with Claude Code, need higher throughput for interactive sessions"
- Submit
- ⏰ **Wait 2-5 business days for approval**

---

## Day 5-8: Quota Approval

*Google reviews and approves (usually approved)*

---

## Day 8+: Production Use

### 8. Monitor & Optimize
- Check GCP billing dashboard
- Use global endpoints (no +10% premium)
- Set up billing alerts

---

## Quick Reference Timeline

```
Day 0:  Enable API, request model access, set up auth
Day 1-2: Wait for model access approval
Day 2:  Configure Claude Code, test
Day 3:  Hit rate limits, request quota increase
Day 5-8: Wait for quota approval
Day 8+: Full production use
```

**Total Time to Full Operation:** ~8-10 days (mostly waiting)

---

## The "Do Everything Now" Approach

If you want to minimize calendar time:

### Do on Day 0 (all at once):
1. Enable Vertex AI API
2. Request model access (wait starts)
3. Set up authentication
4. Configure Claude Code environment variables
5. **Also request quota increase immediately** (even before testing)
   - You'll hit limits anyway
   - Start the 2-5 day wait clock early

**Result:** ~5-7 days total (overlapping waits) instead of ~10 days sequential.
