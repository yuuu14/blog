---
layout: post
title: deutschlernen-plan
date: 2025-10-14 19:18 +0800
---

Last post was already 2 years ago... SO MUCH has changed, Transformer to GPT, capacity of AI models keeps astonishing me. And now I would love to start improving my German, listening and speaking are my nightmare, at the moment I plan to listen to daily 20:00 Tagesschau, dictate and compare with transcription. And there is no available transcript so I have to find a suitable ASR model to run locally. And apparently Whisper is a perfect answer. 

[Whisper-brief-intro]

Just write down current workflow as a reference:
- based on Whisper GitHub [1]
  `uv add openai-whisper setuptools-rust && brew install ffmpeg`

- run `transcribe.py`
    ```Python
    import whisper

    audio_file = "./asr/data/date.mp3"
    output_file = "./asr/data/tagesschau-date.txt"

    model = whisper.load_model("turbo")
    result = model.transcribe(audio_file)
    transcription_text = result["text"]

    with open(output_file, "w", encoding='utf-8') as f:
        f.write(transcription_text) # type: ignore
    ```
- prompt to correct and reformulate transcription
    ```Python
    prompt_template = """
    You are given the transcript of today’s Tagesschau broadcast.

    # Your tasks:
    Correct grammatical errors (e.g., missing articles, verb agreement, punctuation).
    Insert any clearly missing words that are necessary for grammatical completeness.
    Break the text into logical paragraphs to improve readability in Markdown.
    Important: Do not rephrase, summarize, embellish, or alter the original meaning, tone, or factual content in any way. Changes must be minimal and strictly limited to the above.

    # Original transcript:
    {transcript}

    # Return only the refined transcript—no additional commentary, headings, or formatting beyond basic Markdown paragraphs. 
    """
    ```



# Useful Tools I cannot live without

- **Readlang**
  the extension is so convenient, could import so many things. Considering upgrade at the upgrade...






# References
[1] https://github.com/openai/whisper