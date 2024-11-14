# Interview Bot

An AI-powered interview bot designed for conducting technical interviews for AI Engineering positions, with a focus on RAG (Retrieval Augmented Generation) roles. The bot evaluates candidates on Python experience, project examples, RAG understanding, evaluation metrics, and open-source contributions, providing feedback on performance and areas for improvement.

## Architecture

The bot comprises three main components:

1. **Speech-to-Text (STT)**: Utilizes Deepgram's Nova model for accurate transcription.
2. **Language Model (LLM)**: Employs Llama 3.2 on Ollama for generating contextual questions and feedback.
3. **Text-to-Speech (TTS)**: Uses Deepgram TTS for natural-sounding voice output.

## Prerequisites

- Deepgram API key (for STT and TTS)
- Daily.co API key (for video/audio communication)
- Ollama installed with Llama 3.2 model

## Environment Setup

Create a `.env` file with the following content:

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

The bot will conduct a technical interview and provide feedback on the candidate's performance.

## Technical Documentation

### Components Overview

- **Daily Transport Layer**: Manages audio/video communication with VAD (Voice Activity Detection) using Silero.

- **Speech Services**:
  - **STT**: Deepgram's Nova model for English (en-US).
  - **TTS**: British male voice profile.

- **LLM Service**: Llama 3.2 model for question generation and response processing.

### System Prompt Structure

The bot follows a structured interview format with:
- **Interviewer persona**: Allysa from Meta
- **Fixed question set** covering key topics
- Concludes with **personalized feedback**

### Configuration System

- **Environment variables** for API keys
- Daily.co room configuration via `configure()` function
- Supports command-line arguments and environment variables

### Voice Activity Detection

Silero VAD with configurable parameters:
- **Stop threshold**: 0.2 seconds
- **Start threshold**: 0.2 seconds
- **Confidence threshold**: 0.4

## Call Architecture Flow

### Communication Layer

- **WebRTC** for video call interface, hosted through Daily.co

### Signal Processing Flow

1. **Input**: User's voice captured via WebRTC
2. **VAD**: Silero VAD manages speech segmentation
3. **Processing Pipeline**:
   - User Speech → Deepgram STT → Text → Llama 3.2 → Generated Response → Deepgram TTS → Audio Output

This setup ensures a seamless, natural conversation flow, allowing the AI interviewer to engage in real-time dialogue and provide appropriate follow-up questions or feedback.