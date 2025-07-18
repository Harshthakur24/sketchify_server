# Sketchify Server

Real-time collaborative sketching application server built with Node.js, Express, Socket.IO, and Redis.

## Features

- Real-time collaboration using WebSocket
- Room-based sketching sessions with persistence
- Redis-backed data storage (optional)
- Automatic room data recovery
- CORS protection
- Health monitoring endpoints

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Redis (optional - falls back to memory storage)

## Setup

1. Clone the repository:
```bash
git clone <your-repo-url>
cd sketchify_server
```

2. Install dependencies:
```bash
npm install
```

3. (Optional) Install and start Redis:
   - **Windows**: Download from https://redis.io/download or use WSL
   - **macOS**: `brew install redis && brew services start redis`
   - **Ubuntu/Debian**: `sudo apt install redis-server && sudo systemctl start redis`

4. Create a `.env` file in the root directory (optional):
```env
PORT=8080
REDIS_URL=redis://localhost:6379
```

## Development

To run the server in development mode with hot reload:

```bash
npm run dev
```

## Production

To start the server in production:

```bash
npm start
```

## Redis Integration

The server automatically tries to connect to Redis at `redis://localhost:6379`. If Redis is not available, it falls back to in-memory storage.

### Benefits of Redis:
- Room data persistence across server restarts
- Scalability for multiple server instances
- 7-day data retention (configurable)

### Without Redis:
- Room data is stored in memory only
- Data is lost when server restarts
- Single server instance only

## API Endpoints

- `GET /`: Server status page
- `GET /api/health`: Health check endpoint

## WebSocket Events

### Client -> Server
- `join`: Join a room and receive existing elements
- `leave`: Leave a room
- `getElements`: Broadcast elements to room participants and save to Redis

### Server -> Client
- `setElements`: Receive elements from other participants or room history

## Deployment

### With Redis (Recommended for Production)

#### Heroku with Redis
```bash
heroku create your-app-name
heroku addons:create heroku-redis:mini
git push heroku main
```

#### Railway with Redis
1. Add Redis service in Railway dashboard
2. Connect your GitHub repository
3. Deploy from main branch

### Without Redis (Simple Deployment)
The server works without Redis and will use in-memory storage.

## Environment Variables

- `PORT`: Server port (default: 8080)
- `REDIS_URL`: Redis connection URL (optional)

## License

ISC
