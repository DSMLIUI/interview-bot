# interview-bot

An AI-powered interview bot that conducts technical interviews for AI Engineering positions, specifically focused on RAG (Retrieval Augmented Generation) roles.

## Architecture

The bot uses three main components:

1. **Speech-to-Text**: Deepgram Nova model for accurate transcription of candidate responses
2. **Language Model**: Llama 3.2 running on Ollama for generating contextual interview questions and feedback
3. **Text-to-Speech**: Deepgram TTS for natural-sounding voice output

## Prerequisites

- Deepgram API key (for STT and TTS)
- Daily.co API key (for video/audio communication)
- Ollama installed with Llama 3.2 model pulled

## Environment Setup

1. Create a `.env` file with:

```bash
DEEPGRAM_API_KEY=your_key_here
DAILY_API_KEY=your_key_here
```

## Installation

1. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```
2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Running the Bot
Start the interview bot:

```bash
python interview_bot.py
```

The bot will conduct a technical interview, asking questions about Python experience, project examples, RAG understanding, evaluation metrics, and open-source contributions. At the end, it provides feedback on the candidate's performance and areas for improvement.

## Technical Documentation

### Components Overview

#### Daily Transport Layer (DailyTransport)
- Handles audio/video communication
- Configures VAD (Voice Activity Detection) using Silero
- Parameters include audio I/O, camera settings, and VAD configuration

#### Speech Services
##### STT (DeepgramSTTService)
- Uses Deepgram's Nova model
- Configured for English (en-US)

##### TTS (DeepgramTTSService)
- Uses a British male voice profile

#### LLM Service
- Uses Ollama with Llama 3.2 model
- Handles interview question generation and response processing
- Guided by system prompt defining interviewer persona and question flow

### System Prompt Structure
The bot follows a structured interview format with:
- Interviewer persona: Allysa from Meta
- Fixed question set covering:
  - Python experience
  - Project examples
  - RAG knowledge
  - Performance metrics
  - Open-source contributions
- Concludes with personalized feedback

### Configuration System
- Uses environment variables for API keys
- Daily.co room configuration handled by `configure()` function
- Supports both command-line arguments and environment variables
- Room tokens generated with 1-hour expiry

### Voice Activity Detection
- Uses Silero VAD with configurable parameters:
  - Stop threshold: 0.2 seconds
  - Start threshold: 0.2 seconds
  - Confidence threshold: 0.4

The bot conducts a technical interview, asking questions about Python experience, project examples, RAG understanding, evaluation metrics, and open-source contributions. At the end, it provides feedback on the candidate's performance and areas for improvement.
