# Instapods Hub

Standalone cloud hub for Lab R&D Operating System mesh synchronization.

## Features

- Mesh sync coordination with B2
- Supabase mirroring
- Mobile note ingestion
- File upload/download via signed URLs
- Supabase keep-alive (prevents free tier pausing)

## Quick Start

### 1. Configure Environment

Copy `.env.example` to `.env` and configure your environment variables:

```bash
cp .env.example .env
# Edit .env with your actual credentials
```

Required environment variables:
- `B2_ACCOUNT2_ENDPOINT`, `B2_ACCOUNT2_KEY_ID`, `B2_ACCOUNT2_APPLICATION_KEY`, `B2_ACCOUNT2_BUCKET` - Backblaze B2 credentials
- `SUPABASE_URL`, `SUPABASE_SERVICE_KEY` - Supabase credentials
- `JWT_SECRET` - Secret for API authentication
- `INSTAPODS_HOST`, `INSTAPODS_PORT` - Server configuration

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Start the Server

**Linux/Mac:**
```bash
chmod +x start.sh
./start.sh
```

**Windows:**
```cmd
start.bat
```

**Or manually:**
```bash
python instapods_hub.py
```

The server will start on `http://0.0.0.0:8001` by default.

## Deployment

### Instapods Native Deployment

1. Push this repository to GitHub
2. Connect to Instapods dashboard
3. Configure build settings (Python 3.12)
4. Add environment variables from `.env.example`
5. Deploy

### Docker Deployment (Optional)

Create a `Dockerfile` for containerized deployment if needed.

## Endpoints

- `GET /health` - Health check (no authentication)
- `GET /signed-url?filename=` - Get B2 signed URL (JWT authentication required)
- `POST /upload` - Upload file to B2 (JWT authentication required)

## Architecture

```
Instapods Hub (Python/FastAPI)
    ↓
Mesh Sync Coordinator
    ↓
B2 (Backblaze B2) - Mesh transactions and files
    ↓
Supabase - Structured data mirror
    ↓
Mobile App (React Native)
```

## Dependencies

This deployment environment includes only the dependencies needed for the cloud sync coordinator:
- Web server: FastAPI, Uvicorn
- Database sync: Supabase client, Boto3
- Data processing: Pandas, NumPy, PyArrow
- AI: Google Generative AI (if used for server-side processing)

Audio processing dependencies (SpeechRecognition, pyttsx3) are excluded as they run client-side only.

## License

Part of Lab R&D Operating System
"# instapods-hub" 
