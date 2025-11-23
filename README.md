# 🎙️ DailyAI Voice - Automated AI News Podcaster

DailyAI Voice is an automated AI podcaster that gathers the latest tech and AI news from trusted sources, summarizes them, and delivers a clean, easy-to-listen audio briefing straight to your WhatsApp inbox.

![Workflow Overview](public/Screenshot%202025-11-23%20220104.png)

## ✨ Features

- **Automated News Aggregation**: Fetches latest AI and tech news from multiple RSS feeds
- **AI-Powered Scriptwriting**: Uses Google Gemini to create natural, conversational podcast scripts
- **Text-to-Speech**: Converts scripts to high-quality audio using Murf AI
- **WhatsApp Delivery**: Automatically sends audio briefings to your WhatsApp
- **Smart Filtering**: Only includes news from the last 24 hours
- **RAG Integration**: Stores and retrieves context using Supabase vector database
- **Scheduled Updates**: Runs automatically on a schedule or via WhatsApp trigger

## 🏗️ Architecture

![Workflow Details](public/Screenshot%202025-11-23%20221015.png)

The workflow is built using **n8n** and consists of the following components:

### Data Sources
- **RSS Feeds**: Aggregates news from:
  - TechCrunch AI
  - Wired AI
  - Artificial Intelligence Blog
  - And more trusted sources

### Processing Pipeline
1. **RSS Feed Readers**: Fetch articles from multiple sources
2. **Merge Node**: Combines all articles into a single stream
3. **Filter**: Keeps only articles from the last 24 hours
4. **Aggregate**: Prepares data for AI processing
5. **AI Agent**: Google Gemini writes a natural podcast script
6. **Text-to-Speech**: Murf converts script to audio (MP3)
7. **WhatsApp Delivery**: Twilio sends audio to your WhatsApp

### AI Components
- **Language Model**: Google Gemini 2.5 Pro
- **Embeddings**: Cohere for vector embeddings
- **Vector Store**: Supabase for document storage and retrieval
- **Memory**: PostgreSQL for conversation context

## 🚀 Getting Started

### Prerequisites

- n8n instance (cloud or self-hosted)
- API keys for:
  - Google Gemini API
  - Murf AI
  - Twilio (for WhatsApp)
  - Cohere API
  - Supabase
  - PostgreSQL

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/shresthaPandit/AI_PODCAST_VOICE_AGENT.git
   cd AI_PODCAST_VOICE_AGENT
   ```

2. **Import the workflow**
   - Open your n8n instance
   - Go to Workflows → Import from File
   - Select `RAG (1).json`

3. **Configure Credentials**
   - Set up the following credentials in n8n:
     - Google Gemini API (for scriptwriting)
     - Murf API (for text-to-speech)
     - Twilio API (for WhatsApp delivery)
     - Cohere API (for embeddings)
     - Supabase API (for vector storage)
     - PostgreSQL (for chat memory)

4. **Update Configuration**
   - Replace placeholder values in the workflow:
     - `YOUR_ACCOUNT_SID` → Your Twilio Account SID
     - `YOUR_AUTH_TOKEN` → Your Twilio Auth Token
     - `YOUR_PHONE_NUMBER` → Your WhatsApp number
     - `YOUR_TWILIO_NUMBER` → Your Twilio WhatsApp number

5. **Activate the Workflow**
   - Enable the workflow in n8n
   - The schedule trigger will run automatically, or
   - Send a message to your Twilio WhatsApp number to trigger manually

## 📋 Workflow Components

### Triggers
- **Schedule Trigger**: Runs automatically on a set interval
- **Twilio Trigger**: Responds to incoming WhatsApp messages

### RSS Feed Sources
- TechCrunch AI News
- Wired AI Latest
- Artificial Intelligence Blog
- Additional customizable feeds

### AI Scriptwriter
The AI agent is configured to:
- Write in a friendly, conversational tone
- Summarize 5-10 most important articles
- Keep scripts under 900 words
- Create natural, podcast-ready content

### Audio Generation
- Voice: Alina (Female, English US)
- Style: Conversational
- Format: MP3
- Powered by Murf AI

## 🔧 Configuration

### Customizing RSS Feeds
Edit the RSS Read nodes to add or modify news sources:
```json
{
  "url": "https://your-rss-feed-url.com/feed/",
  "options": {}
}
```

### Adjusting Filter Timeframe
Modify the Filter node to change the time window:
```javascript
$now.minus({ days: 1 }) // Change 1 to desired number of days
```

### Customizing AI Prompt
Edit the AI Agent node's system message to change the scriptwriting style and tone.

## 📱 Usage

### Automatic Mode
The workflow runs automatically based on the schedule trigger. You'll receive daily audio briefings on WhatsApp.

### Manual Mode
Send any message to your configured Twilio WhatsApp number to trigger the workflow manually.

## 🛠️ Tech Stack

- **Workflow Engine**: n8n
- **AI Language Model**: Google Gemini 2.5 Pro
- **Text-to-Speech**: Murf AI
- **Messaging**: Twilio WhatsApp API
- **Vector Database**: Supabase
- **Embeddings**: Cohere
- **Database**: PostgreSQL

## 📝 Environment Variables

Create a `.env` file (not included in repo) with:
```
GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here
```

## 🔒 Security

⚠️ **Important**: This repository has been sanitized. All API keys, credentials, and sensitive information have been removed. Before using this workflow:

1. Never commit API keys or credentials
2. Use n8n's credential management system
3. Set up environment variables for sensitive data
4. Review and update all placeholder values

## 📄 License

This project is open source and available under the MIT License.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

For questions or support, please open an issue on GitHub.

---

**Built with ❤️ using n8n, Google Gemini, and Murf AI**

