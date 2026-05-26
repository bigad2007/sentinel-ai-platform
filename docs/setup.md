# Sentinel AI Platform - Quick Start Guide

## Prerequisites

- Docker & Docker Compose
- Node.js 18+ (for local frontend development)
- Python 3.11+ (for local backend development)
- Git

## Quick Start with Docker Compose

### 1. Clone Repository
```bash
git clone https://github.com/bigad2007/sentinel-ai-platform.git
cd sentinel-ai-platform
```

### 2. Configure Environment
```bash
# Copy environment template
cp backend/.env.example backend/.env

# Edit configuration (add your API keys)
nano backend/.env
```

### 3. Start Services
```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f backend
docker-compose logs -f frontend
```

### 4. Access Application
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8000
- **API Docs**: http://localhost:8000/docs
- **Redis**: localhost:6379
- **PostgreSQL**: localhost:5432

### 5. Stop Services
```bash
docker-compose down

# Remove volumes
docker-compose down -v
```

## Local Development Setup

### Backend Development

```bash
# Navigate to backend
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run development server
python -m uvicorn app.main:app --reload
```

**Backend URL**: http://localhost:8000

### Frontend Development

```bash
# Navigate to frontend
cd frontend

# Install dependencies
npm install

# Run development server
npm run dev
```

**Frontend URL**: http://localhost:5173

### Start Redis (separate terminal)
```bash
# Using Docker
docker run -d -p 6379:6379 redis:7-alpine

# Or use local Redis installation
redis-server
```

### Start PostgreSQL (separate terminal)
```bash
# Using Docker
docker run -d \
  -p 5432:5432 \
  -e POSTGRES_USER=sentinel \
  -e POSTGRES_PASSWORD=sentinel_pass \
  -e POSTGRES_DB=sentinel_db \
  postgres:15-alpine
```

## API Endpoints

### Logs API
```bash
# List logs
curl http://localhost:8000/api/v1/logs

# Get statistics
curl http://localhost:8000/api/v1/logs/stats
```

### Threat Intelligence API
```bash
# Analyze IP
curl http://localhost:8000/api/v1/intelligence/ip/8.8.8.8

# Analyze URL
curl "http://localhost:8000/api/v1/intelligence/url?url=https://example.com"

# Analyze hash
curl http://localhost:8000/api/v1/intelligence/hash/abc123def456

# Analyze domain
curl http://localhost:8000/api/v1/intelligence/domain/example.com
```

### Analysis API
```bash
# Perform analysis
curl -X POST http://localhost:8000/api/v1/analysis/query \
  -H "Content-Type: application/json" \
  -d '{
    "query": "What are the suspicious activities?",
    "context": {}
  }'
```

### Alerts API
```bash
# List alerts
curl http://localhost:8000/api/v1/alerts

# Get alert stats
curl http://localhost:8000/api/v1/alerts/stats

# Acknowledge alert
curl -X POST http://localhost:8000/api/v1/alerts/{alert_id}/acknowledge

# Resolve alert
curl -X POST http://localhost:8000/api/v1/alerts/{alert_id}/resolve \
  -H "Content-Type: application/json" \
  -d '{"resolution_notes": "False positive"}'
```

## WebSocket Connections

### Using JavaScript/Browser
```javascript
// Log streaming
const logsWs = new WebSocket('ws://localhost:8000/ws/logs');

logsWs.onmessage = (event) => {
  console.log('Log:', JSON.parse(event.data));
};

// Event streaming
const eventsWs = new WebSocket('ws://localhost:8000/ws/events');

eventsWs.onmessage = (event) => {
  console.log('Event:', JSON.parse(event.data));
};

// Chat
const chatWs = new WebSocket('ws://localhost:8000/ws/chat');

chatWs.send(JSON.stringify({
  message_id: 'msg_123',
  content: 'What are the recent threats?'
}));

chatWs.onmessage = (event) => {
  console.log('Response:', JSON.parse(event.data));
};
```

### Using Python
```python
import asyncio
import websockets
import json

async def test_chat():
    uri = "ws://localhost:8000/ws/chat"
    async with websockets.connect(uri) as websocket:
        # Send message
        message = {
            "message_id": "msg_123",
            "content": "Analyze recent security events"
        }
        await websocket.send(json.dumps(message))
        
        # Receive response
        response = await websocket.recv()
        print(f"Response: {response}")

asyncio.run(test_chat())
```

## Common Tasks

### Adding API Keys
Edit `backend/.env`:
```env
VIRUSTOTAL_API_KEY=your_key_here
ABUSEIPDB_API_KEY=your_key_here
OPENAI_API_KEY=your_key_here
```

### Database Migrations (Future)
```bash
# Create migration
alembic revision --autogenerate -m "Add users table"

# Apply migrations
alembic upgrade head
```

### Running Tests
```bash
# Backend tests
cd backend
pytest

# Frontend tests
cd frontend
npm test
```

### Building for Production
```bash
# Backend
docker build -t sentinel-backend:latest backend/

# Frontend
docker build -t sentinel-frontend:latest frontend/

# Both via compose
docker-compose build
```

## Troubleshooting

### Port Already in Use
```bash
# Find and kill process using port
lsof -ti:8000 | xargs kill -9  # Backend
lsof -ti:5173 | xargs kill -9  # Frontend
```

### Redis Connection Error
```bash
# Verify Redis is running
redis-cli ping  # Should return PONG

# Check Redis connection
redis-cli -h localhost -p 6379
```

### PostgreSQL Connection Error
```bash
# Test connection
psql -h localhost -U sentinel -d sentinel_db

# Check if service is running
docker ps | grep postgres
```

### WebSocket Connection Failed
- Check backend is running
- Verify firewall rules
- Check browser console for errors
- Ensure correct WebSocket URL in frontend

### API Documentation Not Loading
- Backend must be running
- Visit http://localhost:8000/docs
- Check browser console for errors

## Performance Tips

1. **Frontend**
   - Use React DevTools to identify re-renders
   - Implement code splitting with lazy loading
   - Monitor WebSocket message frequency

2. **Backend**
   - Monitor async task queue
   - Check Redis memory usage
   - Profile endpoints with slow queries

3. **Database**
   - Create indexes on frequently queried fields
   - Monitor query performance
   - Regular maintenance and backups

## Next Steps

1. Review the [Architecture Guide](architecture.md)
2. Read the [API Documentation](api.md)
3. Configure threat intelligence API keys
4. Set up local LLM with Ollama (optional)
5. Start building custom detection rules
6. Create deployment configuration

## Support

- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions
- **Documentation**: Check docs/ folder
- **Community**: Open security research discussions

---

**Happy Hunting! 🛡️**
