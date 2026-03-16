# URL Shortener

A fast and simple URL shortener built with **FastAPI**, featuring a clean dark-themed web UI, custom aliases, and click tracking.

## Features

- Shorten any URL with a single click
- Custom aliases (e.g., `/my-link`)
- Click tracking with statistics
- Clean, responsive dark-themed UI
- RESTful API endpoints
- Async SQLite database

## Quick Start

```bash
# Clone the repository
git clone https://github.com/qorexdev/url-shortener.git
cd url-shortener

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Run the server
uvicorn app.main:app --reload
```

Open [http://localhost:8000](http://localhost:8000) in your browser.

## API

### Shorten a URL

```
POST /api/shorten
Content-Type: application/json

{
  "url": "https://example.com/very/long/url",
  "custom_alias": "my-link"    // optional
}
```

**Response:**

```json
{
  "original_url": "https://example.com/very/long/url",
  "short_url": "http://localhost:8000/my-link",
  "short_code": "my-link"
}
```

### Get Link Stats

```
GET /api/stats/{code}
```

**Response:**

```json
{
  "original_url": "https://example.com/very/long/url",
  "short_url": "http://localhost:8000/my-link",
  "short_code": "my-link",
  "clicks": 42,
  "created_at": "2025-01-01T00:00:00",
  "last_clicked": "2025-01-02T12:30:00"
}
```

### Redirect

```
GET /{code}  →  307 redirect to original URL
```

## Configuration

Set environment variables to customize:

| Variable | Default | Description |
|---|---|---|
| `BASE_URL` | `http://localhost:8000` | Base URL for generated short links |
| `DATABASE_URL` | `sqlite+aiosqlite:///./shortener.db` | Database connection string |

## Tech Stack

- **FastAPI** - async web framework
- **SQLAlchemy** - async ORM with aiosqlite
- **Jinja2** - server-side templates
- **Vanilla JS** - no frontend framework needed

## License

MIT
