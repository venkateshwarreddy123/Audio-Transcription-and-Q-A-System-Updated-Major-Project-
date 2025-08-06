# Audio Transcription & Q&A System

A powerful web application that downloads YouTube videos, transcribes audio content, and provides intelligent question-answering capabilities using advanced AI models.

## 🚀 Features

- **YouTube Audio Download**: Download audio from any YouTube video URL
- **Multi-language Transcription**: Transcribe audio in original language or translate to English
- **AI-Powered Q&A**: Ask intelligent questions about the transcribed content
- **Text Summarization**: Generate concise summaries of long audio content
- **Vector Search**: Advanced semantic search using FAISS and sentence transformers
- **Modern Web Interface**: Beautiful, responsive UI with real-time progress tracking

## 🛠️ Technology Stack

- **Backend**: Flask (Python)
- **AI Models**: 
  - Faster Whisper (Audio Transcription)
  - Sentence Transformers (Text Embeddings)
  - Google Gemini (Q&A & Summarization)
- **Vector Database**: FAISS (Facebook AI Similarity Search)
- **Frontend**: HTML5, CSS3, JavaScript
- **Audio Processing**: yt-dlp, FFmpeg

## 📋 Prerequisites

- Python 3.8 or higher
- FFmpeg installed on your system
- Google API key for Gemini AI
- At least 4GB RAM (for model loading)

## 🔧 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd major_project
   ```

2. **Install FFmpeg**
   
   **Windows:**
   - Download from [FFmpeg official website](https://ffmpeg.org/download.html)
   - Extract to `C:\ffmpeg\` or add to PATH
   
   **macOS:**
   ```bash
   brew install ffmpeg
   ```
   
   **Linux:**
   ```bash
   sudo apt update
   sudo apt install ffmpeg
   ```

3. **Install Python dependencies**
   ```bash
   pip install -r "requirements (2).txt"
   ```

4. **Set up Google API Key**
   
   Create a `.env` file in the project root:
   ```env
   GOOGLE_API_KEY=your_google_api_key_here
   ```
   
   Or set it directly in the code (not recommended for production):
   ```python
   os.environ["GOOGLE_API_KEY"] = "your_api_key_here"
   ```

## 🚀 Usage

1. **Start the application**
   ```bash
   python app.py
   ```

2. **Open your browser**
   Navigate to `http://localhost:5000`

3. **Using the application**
   - Enter a YouTube URL
   - Choose transcription type (translate or transcribe)
   - Click "Download & Process"
   - Wait for audio download and transcription
   - Process the text for Q&A capabilities
   - Ask questions or generate summaries

## 📚 API Endpoints

### `/api/download-audio`
Downloads audio from YouTube URL
- **Method**: POST
- **Body**: `{"url": "youtube_url"}`
- **Returns**: Audio file info and video title

### `/api/transcribe`
Transcribes audio file using Whisper
- **Method**: POST
- **Body**: `{"audio_file": "filename", "task": "translate|transcribe"}`
- **Returns**: Transcribed text and output file path

### `/api/process-text`
Processes text for Q&A system
- **Method**: POST
- **Body**: `{"text_file": "filename"}`
- **Returns**: Number of chunks and index files

### `/api/ask-question`
Answers questions using AI
- **Method**: POST
- **Body**: `{"question": "text", "index_file": "path", "chunks_file": "path"}`
- **Returns**: Answer and relevant context chunks

### `/api/summarize`
Generates text summary
- **Method**: POST
- **Body**: `{"text_file": "filename"}`
- **Returns**: Generated summary

## 🔍 How It Works

1. **Audio Processing Pipeline**:
   - YouTube URL → Audio download (yt-dlp)
   - Audio file → Transcription (Faster Whisper)
   - Text → Chunking (LangChain)

2. **Q&A System**:
   - Text chunks → Embeddings (Sentence Transformers)
   - Embeddings → FAISS index
   - Question → Embedding → Similarity search
   - Relevant chunks → Gemini AI → Answer

3. **Summarization**:
   - Full text → Gemini AI → Summary

## 📁 Project Structure

```
major_project/
├── app.py                 # Main Flask application
├── index (5).html        # Web interface
├── requirements (2).txt  # Python dependencies
├── README.md            # This file
└── Generated files:
    ├── audio_*.mp3      # Downloaded audio files
    ├── transcribed_*.txt # Transcription output
    ├── faiss_index_*.idx # Vector search index
    └── chunks_*.pkl     # Text chunks data
```

## ⚙️ Configuration

### Model Settings
- **Whisper Model**: Base model (configurable: tiny, base, medium, large)
- **Embedding Model**: all-mpnet-base-v2
- **LLM**: Gemini 1.5 Flash Latest
- **Chunk Size**: 200 characters with 50 character overlap

### Performance Tuning
- Adjust chunk size in `app.py` line 218
- Modify FAISS search parameters (k=3 for top results)
- Change Whisper model size based on accuracy/speed needs

## 🐛 Troubleshooting

### Common Issues

1. **FFmpeg not found**
   - Ensure FFmpeg is installed and in PATH
   - Update paths in `app.py` lines 22-23

2. **Model loading errors**
   - Check internet connection for model downloads
   - Ensure sufficient RAM (4GB+ recommended)
   - Try smaller models if memory is limited

3. **Google API errors**
   - Verify API key is valid and has Gemini access
   - Check API quota limits

4. **Audio download failures**
   - Verify YouTube URL is valid and accessible
   - Check yt-dlp version compatibility

### Error Logs
Check the console output for detailed error messages. The application provides verbose logging for debugging.

## 🔒 Security Notes

- **API Keys**: Never commit API keys to version control
- **File Storage**: Generated files are stored locally
- **CORS**: Configured for development; adjust for production
- **Input Validation**: Implement additional validation for production use

## 🚀 Deployment

### Production Considerations
1. Use WSGI server (Gunicorn, uWSGI)
2. Set up reverse proxy (Nginx)
3. Configure environment variables
4. Implement proper error handling
5. Add rate limiting
6. Set up monitoring and logging

### Docker Deployment
```dockerfile
FROM python:3.9-slim
RUN apt-get update && apt-get install -y ffmpeg
COPY . /app
WORKDIR /app
RUN pip install -r "requirements (2).txt"
EXPOSE 5000
CMD ["python", "app.py"]
```

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📞 Support

For issues and questions:
- Check the troubleshooting section
- Review error logs
- Create an issue with detailed information

## 🔄 Updates

- **v1.0**: Initial release with basic transcription and Q&A
- Future versions will include:
  - Batch processing
  - More language support
  - Advanced analytics
  - Export capabilities

---

**Note**: This application requires significant computational resources for AI model inference. Ensure your system meets the minimum requirements for optimal performance. 