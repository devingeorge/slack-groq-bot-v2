# Slack Groq Bot v2 Deployment Guide

This guide will help you deploy the new slack-groq-bot-v2 as a completely separate instance from your original deployment.

## ✅ Completed Steps

### 1. Updated Configuration Files
- ✅ Updated `package.json` to version 2.0.0 with name "slack-groq-bot-v2"
- ✅ Updated `slack-app-manifest.json` with new URLs pointing to `slack-groq-bot-v2.onrender.com`
- ✅ Updated `render.yaml` with new service name "slack-groq-bot-v2"
- ✅ Committed all changes to git

## 🔄 Next Steps

### 2. ✅ GitHub Repository Created

The GitHub repository has been successfully created and your code has been pushed!

- **Repository URL**: https://github.com/devingeorge/slack-groq-bot-v2
- **Status**: Public repository with all code pushed
- **Remote**: Origin set up and tracking main branch

### 3. Set Up New Render Project

**Note**: The Render CLI is installed and authenticated, but it's designed for managing existing services rather than creating new ones. You'll need to create the project via the dashboard.

1. Go to [Render.com](https://render.com) and sign in
2. Click "New +" → "Web Service"
3. Connect your GitHub account and select the `slack-groq-bot-v2` repository
4. Configure the service:
   - **Name**: `slack-groq-bot-v2`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: Choose based on your needs (Free tier available)

**Render CLI Status**: ✅ Installed and authenticated as Devin George (devingeorge@gmail.com)

### 4. Configure Environment Variables

In your Render dashboard, add these environment variables:

#### Required Environment Variables:
```
NODE_ENV=production
SLACK_BOT_TOKEN=xoxb-your-bot-token-here
SLACK_SIGNING_SECRET=your-signing-secret-here
SLACK_CLIENT_ID=your-client-id-here
SLACK_CLIENT_SECRET=your-client-secret-here
SLACK_STATE_SECRET=your-state-secret-here
```

#### AI Service Variables (choose one):
```
# For Grok (recommended)
GROQ_API_KEY=your-groq-api-key-here

# OR for OpenAI
OPENAI_API_KEY=your-openai-api-key-here

# OR for Google Gemini
GOOGLE_API_KEY=your-google-api-key-here
```

#### Optional Variables:
```
# Database (if using PostgreSQL)
PG_CONN=your-postgres-connection-string

# Redis (if using Redis for caching)
REDIS_URL=your-redis-url

# Jira Integration (if using)
JIRA_BASE_URL=your-jira-url
JIRA_USERNAME=your-jira-username
JIRA_API_TOKEN=your-jira-token
```

### 5. Create New Slack App

1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Click "Create New App"
3. Choose "From an app manifest"
4. Select your workspace
5. Copy and paste the contents of `slack-app-manifest.json` from this repository
6. Click "Create"
7. Note down the following from your app's "Basic Information":
   - **Client ID**
   - **Client Secret**
   - **Signing Secret**
   - **Bot User OAuth Token** (from OAuth & Permissions)

### 6. Update Environment Variables with Slack Credentials

Go back to your Render dashboard and update the environment variables with the actual values from your new Slack app:

```
SLACK_BOT_TOKEN=xoxb-your-actual-bot-token
SLACK_SIGNING_SECRET=your-actual-signing-secret
SLACK_CLIENT_ID=your-actual-client-id
SLACK_CLIENT_SECRET=your-actual-client-secret
SLACK_STATE_SECRET=your-actual-state-secret
```

### 7. Deploy to Render

1. In your Render dashboard, click "Deploy latest commit"
2. Wait for the deployment to complete
3. Note the URL provided by Render (should be `https://slack-groq-bot-v2.onrender.com`)

### 8. Update Slack App URLs (if needed)

If Render assigned a different URL, update your Slack app:

1. Go to your Slack app's "Basic Information"
2. Update the following URLs to match your Render deployment:
   - **Request URL** (Event Subscriptions): `https://your-actual-url.onrender.com/slack/events`
   - **Interactivity Request URL**: `https://your-actual-url.onrender.com/slack/interactive`
   - **OAuth Redirect URLs**: `https://your-actual-url.onrender.com/slack/oauth_redirect`
   - **Slash Commands URLs**: `https://your-actual-url.onrender.com/slack/commands`

### 9. Install App to Workspace

1. In your Slack app dashboard, go to "Install App"
2. Click "Install to Workspace"
3. Authorize the permissions
4. Test the bot in your workspace

## 🎉 Deployment Complete!

You now have two independent deployments:

- **Original**: `slack-groq-bot` (your current working version)
- **New**: `slack-groq-bot-v2` (fresh deployment with Dynamic Action Triggers)

## 🔧 Testing Your v2 Deployment

Test these features in your workspace:

1. **Slash Commands**: `/ask` and `/ticket`
2. **Mentions**: @Grok AI v2
3. **Direct Messages**: Send a DM to the bot
4. **App Home**: Click on the bot in your sidebar

## 📝 Notes

- The v2 deployment uses completely separate environment variables and Slack app credentials
- Both deployments can run simultaneously without conflicts
- The v2 app has enhanced capabilities and Dynamic Action Triggers
- All URLs in the manifest point to the new v2 deployment

## 🆘 Troubleshooting

If you encounter issues:

1. Check Render logs for deployment errors
2. Verify all environment variables are set correctly
3. Ensure Slack app URLs match your Render deployment URL
4. Test the health endpoint: `https://your-url.onrender.com/health`

## 🔄 Future Updates

To update the v2 deployment:

1. Make changes to your local code
2. Commit and push to GitHub
3. Render will automatically redeploy

```bash
git add .
git commit -m "Your update message"
git push origin main
```

## 🛠️ Using Render CLI for Management

Once your service is created, you can use the Render CLI for management:

```bash
# View services
render services -o text

# View logs
render logs <service-name> -o text

# Restart service
render restart <service-name> --confirm

# View deploys
render deploys -o text

# Trigger a new deploy
render deploys create <service-name> --confirm
```

**Note**: The CLI requires a workspace to be set. You can set it interactively or use the dashboard to manage services.
