# Film Trailer and Summary Generator

This project is a Python-based tool that automatically generates a cinematic trailer and a concise summary video with voiceover for any input video file. It leverages advanced audio processing, speech-to-text transcription, and AI-driven content selection to create engaging video outputs. The project was originally developed in Google Colab and uses various libraries for video editing, transcription, and text-to-speech generation.

## Features
- **Audio Extraction**: Extracts audio from input videos and converts it to a standardized WAV format.
- **Transcription**: Uses OpenAI's Whisper model to transcribe audio with precise timestamps.
- **Trailer Generation**: Automatically selects dramatic, emotional, or action-packed segments to create a compelling trailer using Google Gemini AI.
- **Summary Video**: Generates a concise summary video with key narrative moments and a professional voiceover created via Kokoro-82M.
- **Google Drive Integration**: Supports input and output file handling via Google Drive.
- **JSON Output**: Saves transcriptions and selected segments as JSON for further analysis or reuse.

[![Original Video](https://img.youtube.com/vi/x9yuKmAdnn4&t=961s/0.jpg)](https://www.youtube.com/watch?v=x9yuKmAdnn4&t=961s)

## Requirements
To run this project, ensure you have the following dependencies installed:
```bash
pip install git+https://github.com/openai/whisper.git
pip install yt-dlp
pip install torchaudio librosa pydub ffmpeg-python panns-inference
pip install -q kokoro>=0.9.2 soundfile
pip install moviepy langchain-google-genai langchain-core
```
Additionally, install system-level dependencies:
```bash
apt-get -qq -y install espeak-ng
```

### Additional Setup
- **Google API Key**: Required for Google Gemini AI. Set it as an environment variable:
  ```bash
  export GOOGLE_API_KEY='your_api_key'
  ```
- **Google Drive**: Mount your Google Drive in Colab to access input videos and save outputs.
- **Input Video**: Place your video file (e.g., `panda.mp4`) in a Google Drive folder (e.g., `/My Drive/videos/`).

## Usage
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/film-trailer-and-summary.git
   cd film-trailer-and-summary
   ```

2. **Prepare Input**:
   - Update the `input_file_path` in the script to point to your video file in Google Drive (e.g., `/content/drive/My Drive/videos/panda.mp4`).
   - Ensure the output paths (e.g., `panda_trailer.mp4`, `panda_summary.mp4`) are correctly specified.

3. **Run the Script**:
   ```bash
   python film_trailer_and_summary.py
   ```
   The script will:
   - Extract audio from the input video.
   - Transcribe the audio using Whisper.
   - Generate a trailer video with selected dramatic segments.
   - Create a summary video with a text summary and voiceover.
   - Save outputs to JSON files (`film_analysis_output.json`, `trailer.json`, `summary.json`) and video files in Google Drive.

## Project Structure
- `film_trailer_and_summary.py`: Main script containing all functionality.
- `/content/drive/My Drive/videos/`: Default directory for input and output files (configurable).
- `film_analysis_output.json`: Stores the full transcript with timestamps.
- `trailer.json`: Contains selected segments for the trailer.
- `summary.json`: Contains selected segments for the summary video.
- `panda_summary_transcript.txt`: Text summary of the video.
- `panda_summary_audio.wav`: Generated voiceover audio for the summary.

## How It Works
1. **Audio Extraction**:
   - Uses `pydub` to extract audio from the input video and convert it to mono 16kHz WAV format.
2. **Transcription**:
   - Employs Whisper's `large` model to transcribe audio and generate segments with timestamps.
3. **Trailer Generation**:
   - Divides the transcript into four chunks and uses Google Gemini AI to select 1-5 dramatic segments per chunk.
   - Concatenates selected clips using `moviepy` to create the trailer.
4. **Summary Generation**:
   - Selects 1-3 key segments per chunk to cover the narrative arc.
   - Generates a 100-150 word text summary using Gemini AI.
   - Creates a voiceover with Kokoro-82M and synchronizes it with the summary video.
5. **Output**:
   - Saves the trailer and summary videos to Google Drive.
   - Exports transcriptions and segment data as JSON for further use.

## Limitations
- Requires a stable internet connection for Google Drive and API access.
- Kokoro-82M voice generation may not perfectly match video duration, requiring padding with silence.
- Google Gemini API usage may incur costs depending on your plan.
- Designed for Google Colab; local execution may require adjustments (e.g., file paths, dependency installation).

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request with your changes. Ensure your code follows PEP 8 style guidelines and includes appropriate documentation.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- [OpenAI Whisper](https://github.com/openai/whisper) for speech-to-text transcription.
- [Google Gemini AI](https://cloud.google.com/gemini) for intelligent segment selection and summarization.
- [Kokoro-82M](https://github.com/kokoro-82m) for text-to-speech voiceover generation.
- [MoviePy](https://zulko.github.io/moviepy/) for video editing.
