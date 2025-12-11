# LiveKit AI Interview Agent

A real-time AI interview agent powered by Azure OpenAI and LiveKit, designed to conduct interactive technical interviews with natural voice conversations.

## Features

- 🎙️ Real-time voice conversations using Azure OpenAI Realtime API
- 🔊 Multiple voice options (alloy, echo, fable, onyx, nova, shimmer)
- 📝 Live transcription of both user and AI speech
- 🎯 Customizable interview contexts (position, skills, difficulty)
- 🔄 Automatic reconnection and error handling

## Architecture

- **LiveKit**: Real-time communication platform for audio streaming
- **Azure OpenAI**: GPT-4o Realtime API for natural voice interactions
- **Node.js**: Runtime environment with TypeScript
- **Docker**: Containerized deployment

## Deployment on Railway

### Prerequisites

1. **LiveKit Account**: Sign up at [LiveKit Cloud](https://cloud.livekit.io/)
2. **Azure OpenAI**: Access to Azure OpenAI with GPT-4o Realtime API
3. **Railway Account**: Sign up at [Railway.app](https://railway.app/)

### Step 1: Prepare Your Repository

Ensure your code is pushed to a Git repository (GitHub, GitLab, or Bitbucket).

### Step 2: Create a New Railway Project

1. Go to [Railway Dashboard](https://railway.app/dashboard)
2. Click **"New Project"**
3. Select **"Deploy from GitHub repo"**
4. Choose your repository
5. Railway will automatically detect the `railway.json` and `Dockerfile`

### Step 3: Configure Environment Variables

In the Railway dashboard, add the following environment variables:

| Variable | Description | Example |
|----------|-------------|---------|
| `LIVEKIT_URL` | Your LiveKit server WebSocket URL | `wss://your-project.livekit.cloud` |
| `LIVEKIT_API_KEY` | LiveKit API key from dashboard | `APIxxxxxxxxxx` |
| `LIVEKIT_API_SECRET` | LiveKit API secret from dashboard | `xxxxxxxxxxxxxxxx` |
| `AZURE_ENDPOINT` | Azure OpenAI endpoint URL | `https://your-resource.openai.azure.com` |
| `AZURE_OPENAI_DEPLOYMENT` | Your GPT-4o Realtime deployment name | `gpt-4o-realtime` |
| `AZURE_API_KEY` | Azure OpenAI API key | `xxxxxxxxxxxxxxxx` |

**To add environment variables in Railway:**
1. Select your deployed service
2. Go to the **"Variables"** tab
3. Click **"New Variable"**
4. Add each variable with its value
5. Click **"Deploy"** to restart with new variables

### Step 4: Deploy

Railway will automatically:
1. Build the Docker image using your `Dockerfile`
2. Install dependencies
3. Compile TypeScript to JavaScript
4. Start the agent with `npm start`

### Step 5: Monitor Deployment

1. Check the **"Deployments"** tab for build status
2. View logs in the **"Logs"** tab
3. Look for: `✓ Cleanup complete` and connection messages

### Step 6: Verify Agent is Running

Your agent should now be running and connected to LiveKit. You can verify by:
1. Checking Railway logs for successful connection messages
2. Testing an interview session from your frontend application
3. Monitoring LiveKit dashboard for active agents

## Local Development

### Prerequisites

- Node.js 20 or higher
- npm or yarn

### Setup

1. Clone the repository:
```bash
git clone <your-repo-url>
cd agents
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file (see `.env.example`):
```bash
cp .env.example .env
```

4. Configure your environment variables in `.env`

5. Run in development mode:
```bash
npm run dev
```

### Development Scripts

- `npm run dev` - Run with hot reload using tsx
- `npm run build` - Compile TypeScript to JavaScript
- `npm start` - Run compiled JavaScript (production)

## Docker Deployment (Alternative)

If you prefer to deploy using Docker directly:

```bash
# Build the image
docker build -t livekit-agent .

# Run the container
docker run -d \
  --name livekit-agent \
  --env-file .env \
  -p 8080:8080 \
  livekit-agent
```

## Troubleshooting

### Agent Not Connecting to LiveKit

- Verify `LIVEKIT_URL`, `LIVEKIT_API_KEY`, and `LIVEKIT_API_SECRET` are correct
- Check Railway logs for connection errors
- Ensure LiveKit project is active and not suspended

### Azure OpenAI Connection Issues

- Verify `AZURE_ENDPOINT` includes `https://` and correct resource name
- Confirm `AZURE_OPENAI_DEPLOYMENT` matches your deployment name exactly
- Check `AZURE_API_KEY` is valid and not expired
- Ensure GPT-4o Realtime API is enabled in your Azure subscription

### Build Failures

- Check Railway logs for specific error messages
- Verify `package.json` dependencies are correct
- Ensure TypeScript compiles locally with `npm run build`

### Audio Quality Issues

- Check network connectivity between Railway and LiveKit
- Monitor Railway logs for buffer underrun warnings
- Verify sample rate settings (24kHz) match on both ends

### Missing Native Modules

If you see errors about `@livekit/rtc-node-linux-x64-musl`:
- The Dockerfile copies `node_modules` from builder to preserve native bindings
- Ensure you're using the multi-stage Dockerfile provided

## Environment Variables Reference

See `.env.example` for a complete list of required environment variables with descriptions.

## Support

For issues related to:
- **LiveKit**: [LiveKit Documentation](https://docs.livekit.io/)
- **Azure OpenAI**: [Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/)
- **Railway**: [Railway Documentation](https://docs.railway.app/)

## License

[Your License Here]
