# 🛠️ Technical Documentation

## Architecture Overview

### Components
1. **Web Interface (Flask)**
   - Routes handling
   - Template rendering
   - API endpoints
   - Error handling

2. **Article Scraper**
   - Content extraction
   - Text cleaning
   - Format conversion
   - Error handling

3. **Notion Integration**
   - API communication
   - Block conversion
   - Page creation
   - Error handling

## API Endpoints

### 1. Save Article
```http
POST /save
Content-Type: application/json

{
    "url": "https://example.com/article",
    "format": "md"  // Options: txt, md, notion
}
```

Response:
```json
{
    "success": true,
    "data": {
        "title": "Article Title",
        "content": "Article content...",
        "domain": "example.com",
        "link": "https://example.com/article"
    },
    "format": "md"
}
```

### 2. Preview Article
```http
POST /preview
Content-Type: application/json

{
    "url": "https://example.com/article"
}
```

Response:
```json
{
    "success": true,
    "preview": {
        "title": "Article Title",
        "content": "First 500 characters...",
        "domain": "example.com"
    }
}
```

## Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| SECRET_KEY | Flask secret key | Yes | None |
| NOTION_API_KEY | Notion integration token | For Notion | None |
| NOTION_DEFAULT_PAGE | Default Notion page ID | For Notion | None |
| FLASK_ENV | Environment (development/production) | No | production |
| MAX_CONTENT_LENGTH | Max request size | No | 16MB |

## Dependencies

### Core
- Flask==3.0.2
- notion-client==2.2.1
- requests==2.32.3
- beautifulsoup4==4.12.3
- python-dotenv==1.0.1

### Development
- pytest
- black
- flake8
- mypy

## Development Setup

1. **Create Virtual Environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate     # Windows
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   pip install -r requirements-dev.txt  # For development
   ```

3. **Set Environment Variables**
   ```bash
   cp .env.example .env
   # Edit .env with your values
   ```

4. **Run Development Server**
   ```bash
   flask run --debug
   ```

## Testing

### Unit Tests
```bash
pytest tests/unit/
```

### Integration Tests
```bash
pytest tests/integration/
```

### Load Tests
```bash
locust -f tests/load/locustfile.py
```

## Deployment

### Docker
```bash
docker-compose up -d
```

### Manual
```bash
gunicorn -w 4 -b 0.0.0.0:8000 run:app
```

## Security Considerations

1. **API Security**
   - HTTPS required
   - CSRF protection
   - Rate limiting
   - Input validation

2. **Data Security**
   - No content storage
   - Secure key handling
   - Session management

3. **Infrastructure**
   - Regular updates
   - Dependency scanning
   - Access control

## Performance Optimization

1. **Caching**
   - Response caching
   - Static file caching
   - Browser caching

2. **Resource Optimization**
   - Minified assets
   - Compressed responses
   - Lazy loading

3. **Database (Future)**
   - Connection pooling
   - Query optimization
   - Index management

## Monitoring

### Metrics
- Response time
- Error rate
- CPU usage
- Memory usage
- Request count

### Logging
```python
# Log format
{
    "timestamp": "2024-01-08T22:00:00Z",
    "level": "INFO",
    "event": "article_saved",
    "data": {
        "url": "https://example.com",
        "format": "md",
        "status": "success"
    }
}
```

## Error Handling

### HTTP Status Codes
- 200: Success
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Server Error

### Custom Error Pages
- 404.html
- 500.html
- error.html

## Contributing

1. **Code Style**
   - Follow PEP 8
   - Use type hints
   - Write docstrings

2. **Pull Requests**
   - Create feature branch
   - Add tests
   - Update docs
   - Request review

3. **Documentation**
   - Update README
   - Add inline comments
   - Update API docs

## Future Improvements

1. **Features**
   - User accounts
   - More formats
   - Batch processing
   - API keys

2. **Technical**
   - GraphQL API
   - WebSocket support
   - Service workers
   - PWA support

3. **Infrastructure**
   - CDN integration
   - Load balancing
   - Auto-scaling
   - Backup system 