# AI Video Generation Agent using Agno Framework and Hugging Face Spaces

## Overview

This project implements an AI-powered video generation agent using the Agno framework. The agent accepts a natural language request from the user, converts it into a detailed video generation prompt, and invokes a free Hugging Face Space to generate a short AI video.

The current implementation uses the **Lightricks/LTX-Video-Distilled** Hugging Face Space as the video generation backend.

---

# Objective

Develop an AI agent capable of:

* Receiving natural language requests from users.
* Automatically generating high-quality video prompts.
* Calling a free Hugging Face video generation model.
* Saving the generated video locally.
* Returning the generated video's location to the user.
* Handling failures gracefully and reporting meaningful errors.

---

# Technology Stack

| Component             | Technology          |
| --------------------- | ------------------- |
| Programming Language  | Python 3.10+        |
| AI Agent Framework    | Agno                |
| LLM                   | Mistral Large       |
| Video Model           | LTX-Video-Distilled |
| Video Backend         | Hugging Face Spaces |
| API Client            | gradio_client       |
| Environment Variables | python-dotenv       |

---

# Project Architecture

```
                User
                  │
                  ▼
         Agno AI Agent
                  │
                  ▼
      Understand User Request
                  │
                  ▼
 Generate Detailed Video Prompt
                  │
                  ▼
      generate_video() Tool
                  │
                  ▼
 Hugging Face Space (LTX Video)
                  │
                  ▼
     AI Video Generation
                  │
                  ▼
 Download Generated MP4
                  │
                  ▼
 Store in tmp/ Folder
                  │
                  ▼
 Return Video Path
```

---

# Project Flow

## Step 1 – User Request

The user provides a natural language prompt.

Example:

```
Generate a five-second cinematic video of a tiger walking through a jungle.
```

---

## Step 2 – Agno Agent

The Agno Agent receives the request and processes it using the configured Mistral model.

Responsibilities:

* Understand user intent.
* Create a detailed video generation prompt.
* Determine the requested video duration.
* Automatically invoke the video generation tool.

---

## Step 3 – Prompt Enhancement

The model converts the simple request into a richer prompt.

Example:

Original Prompt

```
Tiger walking in jungle
```

Enhanced Prompt

```
A cinematic tiger slowly walking through a lush green jungle,
golden sunlight passing through the trees,
realistic fur movement,
natural camera tracking,
high quality,
smooth motion,
ultra detailed,
8K look.
```

A richer prompt generally results in higher-quality generated videos.

---

## Step 4 – Video Generation Tool

The `generate_video()` function performs the following tasks:

* Validates the requested duration.
* Applies minimum and maximum duration limits.
* Connects to the Hugging Face Space.
* Sends the enhanced prompt.
* Waits for video generation to complete.
* Receives the generated video.
* Saves the video locally.

---

# Hugging Face Space Configuration

Current Space:

```
Lightricks/ltx-video-distilled
```

Maximum Supported Duration:

```
8.5 seconds
```

If a longer duration is requested, the tool automatically limits the request to the supported maximum.

Example:

Requested:

```
15 seconds
```

Actual:

```
8.5 seconds
```

---

# API Request Parameters

The following parameters are sent to the Hugging Face Space:

| Parameter            | Purpose                     |
| -------------------- | --------------------------- |
| prompt               | Video description           |
| negative_prompt      | Prevent low-quality outputs |
| mode                 | Text-to-video               |
| width                | Video width                 |
| height               | Video height                |
| duration             | Video duration              |
| frames               | Number of frames            |
| guidance_scale       | Controls prompt adherence   |
| improve_texture_flag | Improves visual quality     |
| randomize_seed       | Generates unique outputs    |

---

# Video Generation Process

The Hugging Face Space performs the following:

1. Receives the prompt.
2. Generates video frames.
3. Produces a final MP4 file.
4. Returns the file location.

The agent then copies the file into:

```
tmp/generated_video_<timestamp>.mp4
```

Example:

```
tmp/generated_video_1754567821.mp4
```

---

# Error Handling

The tool includes robust error handling for common failure scenarios.

Handled cases include:

* Invalid duration input.
* Hugging Face API errors.
* GPU quota exhaustion.
* Network connectivity issues.
* Missing generated files.
* Unexpected API response formats.

If generation fails, the agent returns a descriptive error message instead of falsely indicating success.

---

# Agent Instructions

The Agno Agent is configured with instructions to:

* Detect requests related to video generation.
* Automatically call the `generate_video()` tool.
* Generate detailed prompts without requesting additional clarification.
* Respect requested video duration when possible.
* Report the tool's output exactly as returned.

---

# Example Execution Flow

### User

```
Generate a five-second video of a dragon flying over mountains.
```

↓

### Agno Agent

* Understands the request.
* Expands the prompt.
* Calls the video generation tool.

↓

### Tool

* Connects to the Hugging Face Space.
* Generates the video.
* Downloads the MP4.

↓

### Response

```
Video saved to:

tmp/generated_video_1754567821.mp4
```

---

# Current Limitations

The implementation relies on free Hugging Face Spaces, which have some limitations:

* Shared GPU resources may become unavailable.
* Generation speed depends on server load.
* Maximum supported duration is limited by the selected model.
* API parameters may change if the Space is updated.
* Output quality depends on the underlying model.

---

# Future Enhancements

The following improvements can make the solution more robust:

* Support multiple video generation models.
* Automatic fallback to alternative Hugging Face Spaces.
* Integration with commercial video APIs.
* Image-to-video generation.
* Video extension and continuation.
* Background music generation.
* Automatic voice-over creation.
* Subtitle generation.
* Multiple aspect ratio support (16:9, 9:16, 1:1).
* Progress tracking for long-running jobs.
* Cloud storage integration for generated videos.

---

# Conclusion

This implementation demonstrates how the Agno framework can orchestrate an end-to-end AI video generation workflow. The agent interprets user requests, enriches prompts using a language model, invokes a Hugging Face text-to-video model, manages video generation, stores the resulting MP4 locally, and provides clear success or failure feedback. The modular design allows future integration with additional video generation services while keeping the agent interface consistent.
