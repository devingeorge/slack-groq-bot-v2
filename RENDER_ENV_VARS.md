# Render Environment Variables Setup

## 🔧 Required Environment Variables

Add these to your Render dashboard under **Environment Variables**:

### Core Slack Configuration
```
NODE_ENV=production
SLACK_CLIENT_ID=your-client-id-here
SLACK_CLIENT_SECRET=your-client-secret-here
SLACK_SIGNING_SECRET=your-signing-secret-here
SLACK_STATE_SECRET=your-state-secret-here
```

### AI Service (Choose ONE)
```
# For Grok (Recommended)
GROQ_API_KEY=your-groq-api-key-here
GROQ_MODEL=llama-3.1-8b-instant

# OR for OpenAI
OPENAI_API_KEY=your-openai-api-key-here

# OR for Google Gemini
GOOGLE_API_KEY=your-google-api-key-here
```

### Optional Configuration
```
# Redis (for caching and memory)
REDIS_URL=your-redis-url-here
MEMORY_TURNS=16
MEMORY_TTL_DAYS=14

# Assistant Settings
ASSISTANT_THREAD_TTL_SECONDS=86400
ASSISTANT_CONTEXT_TTL_SECONDS=1800

# RAG (if using PostgreSQL)
RAG_ENABLED=false
PG_CONN=your-postgres-connection-string

# Feature Flags
FEAT_CHANNEL_CONTEXT=true
FEAT_RECENT_MESSAGES=true
FEAT_DATA_ACCESS=false

# Limits
MAX_USER_CHARS=4000
MODEL_TEMPERATURE=0.3
```

## 🚀 Quick Setup Steps

1. **Go to your Render dashboard**
2. **Select your `slack-groq-bot-v2` service**
3. **Click "Environment" tab**
4. **Add each variable above** (copy-paste the key-value pairs)
5. **Save the configuration**

## 🔑 Getting Your Slack Credentials

After creating your new Slack app (next step), you'll get these from:
- **Basic Information** → Client ID, Client Secret, Signing Secret
- **OAuth & Permissions** → Bot User OAuth Token (if using single-tenant mode)

## ⚠️ Important Notes

- **SLACK_STATE_SECRET**: Generate a random string (32+ characters)
- **GROQ_API_KEY**: Get from [console.groq.com](https://console.groq.com)
- **REDIS_URL**: Optional but recommended for production
- **RAG_ENABLED**: Set to `false` unless you have PostgreSQL set up

## 🧪 Testing

After setting up environment variables:
1. **Deploy your service**
2. **Check logs** for any startup errors
3. **Test health endpoint**: `https://your-service-url.onrender.com/health`

