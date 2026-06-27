# Skill: VTT to JSON Transcript Converter

## Description
This skill enables the agent to take a standard WebVTT (`.vtt`) closed-caption/transcript file format and convert it into a structured, clean, and valid JSON object for downstream data processing.

## Input Format
The input will be a standard WebVTT string or file snippet, typically containing:
- A `WEBVTT` header block.
- Optional identifiers/cue IDs (e.g., `9ad24116-fae0-4709-a68c-4b916f43a0c0/7-0`).
- Timestamp markers in the format `HH:MM:SS.fff --> HH:MM:SS.fff`.
- Text dialogue lines (which may span single or multiple lines).

---

## Instructions & Behavior
1. **Parse Input**: Analyze the provided VTT text block line by line.
2. **Clean Text**: Remove any redundant or duplicated lines if the VTT text contains overlapping timestamps with identical dialogue strings.
3. **Map Properties**: Extract the following components into a JSON structure:
   - `id`: The cue identifier string (if present).
   - `start_time`: The beginning timestamp of the dialogue block.
   - `end_time`: The ending timestamp of the dialogue block.
   - `text`: The actual spoken dialogue text, joined into a single string if it spans multiple lines.
4. **Output Format**: Return **ONLY** a valid JSON array of objects inside standard markdown JSON blocks. Do not add conversational conversational text before or after the JSON output.

---

## Output Target Schema
```json
[
  {
    "id": "string (optional)",
    "start_time": "HH:MM:SS.fff",
    "end_time": "HH:MM:SS.fff",
    "text": "string"
  }
]