# Slack App Setup Guide

## 🚀 Create New Slack App

### Step 1: Create the App
1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Click **"Create New App"**
3. Select **"From an app manifest"**
4. Choose your workspace
5. Click **"Next"**

### Step 2: Paste the Manifest
Copy the entire contents of `slack-app-manifest.json` and paste it into the manifest editor, then click **"Create"**.

### Step 3: Get Your Credentials
After creating the app, note down these values from your app dashboard:

#### From "Basic Information":
- **Client ID** → Use for `SLACK_CLIENT_ID`
- **Client Secret** → Use for `SLACK_CLIENT_SECRET`  
- **Signing Secret** → Use for `SLACK_SIGNING_SECRET`

#### Generate State Secret:
```bash
# Run this command to generate a secure state secret
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```
Use this output for `SLACK_STATE_SECRET`

### Step 4: Install to Workspace
1. Go to **"Install App"** in your app dashboard
2. Click **"Install to Workspace"**
3. Authorize the permissions
4. **Note the Bot User OAuth Token** (starts with `xoxb-`)

## 🔧 Update Render Environment Variables

Add these to your Render dashboard:

```
SLACK_CLIENT_ID=your-client-id-from-step-3
SLACK_CLIENT_SECRET=your-client-secret-from-step-3
SLACK_SIGNING_SECRET=your-signing-secret-from-step-3
SLACK_STATE_SECRET=your-generated-state-secret
GROQ_API_KEY=your-groq-api-key
NODE_ENV=production
```

## 🌐 Update URLs (if needed)

If Render assigned a different URL than `slack-groq-bot-v2.onrender.com`, update your Slack app:

1. Go to **"Basic Information"**
2. Update these URLs to match your actual Render URL:
   - **Request URL** (Event Subscriptions)
   - **Interactivity Request URL**
   - **OAuth Redirect URLs**
   - **Slash Commands URLs**

## ✅ Test Your Setup

1. **Deploy your Render service**
2. **Check Render logs** for startup success
3. **Test in Slack**:
   - Try `/ask hello` in a channel
   - Mention the bot: `@Grok AI v2 hello`
   - Send a DM to the bot

## 🎉 You're Done!

Your v2 Slack app should now be running independently from your original bot!

