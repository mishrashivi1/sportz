🏟️ Live Sports Event Streaming API

A real-time backend service for live sports coverage using REST APIs and WebSockets.
Built with Node.js, Express, PostgreSQL, and Drizzle ORM to deliver instant score updates and play-by-play commentary.

🚀 Overview

This project is a scalable backend system designed to:

Manage live sports matches

Handle structured commentary updates

Broadcast real-time data to subscribed clients via WebSockets

Enforce strict validation and performance limits

It demonstrates real-time architecture design, WebSocket protocol handling, database modeling, and production-grade backend practices.

⚙️ Tech Stack

Node.js – Backend runtime

Express.js – REST API framework

PostgreSQL – Relational database

Drizzle ORM – Type-safe database queries

Drizzle Kit – Schema migrations

WebSockets (ws) – Real-time communication

Zod – Runtime validation & schema enforcement

Arcjet – Rate limiting & security

Dotenv – Environment configuration

🔥 Key Features
🏆 Match Management

Create and list matches

Automatic status calculation (scheduled / live / finished)

📝 Commentary System

Add structured play-by-play commentary

Query commentary by match

Metadata & tagging support

⚡ Real-Time WebSocket Streaming

Subscribe/unsubscribe per match

Multi-match subscription support

Auto heartbeat & ping/pong

Structured messaging protocol

🛡️ Production-Grade Safeguards

Rate limiting (10 messages/sec)

Burst control

Backpressure protection

Max payload enforcement

Subscription caps

✅ Strict Validation

Zod schemas for REST & WS inputs

Type-safe queries via Drizzle ORM

🌱 Seed Tooling

Script to simulate live match activity

Quick development testing environment

🏗️ System Architecture

Client connects via HTTP (REST) or WebSocket

REST manages match & commentary data

WebSocket server maintains subscription maps

When commentary is created:

Server broadcasts update to subscribed clients

Heartbeat + rate limiting ensure stability

🛠️ Installation
1️⃣ Clone Repository
git clone https://github.com/yourusername/live-sports-ws.git
cd live-sports-ws
2️⃣ Install Dependencies
npm install
3️⃣ Environment Variables

Create a .env file:

# Database
DATABASE_URL=

# Server
PORT=8000
HOST=0.0.0.0

# Security
ARCJET_KEY=
ARCJET_ENV=development

# API URL
API_URL=http://localhost:8000

# Simulation Controls
BROADCAST=1
DELAY_MS=250
MATCH_COUNT=0
4️⃣ Run Development Server
npm run dev

Server Endpoints:

REST API → http://localhost:8000

WebSocket → ws://localhost:8000/ws

📡 REST API Endpoints
Get Matches
GET /matches?limit=50
Create Match
POST /matches

Example body:

{
  "sport": "football",
  "homeTeam": "FC Neon",
  "awayTeam": "Drizzle United",
  "startTime": "2025-02-01T12:00:00.000Z",
  "endTime": "2025-02-01T13:45:00.000Z"
}
Get Commentary
GET /matches/:id/commentary?limit=100
Add Commentary
POST /matches/:id/commentary
🔌 WebSocket Protocol
Connect
ws://localhost:8000/ws

Optional auto-subscribe:

ws://localhost:8000/ws?matchId=123
Client → Server
{ "type": "subscribe", "matchId": 123 }
{ "type": "unsubscribe", "matchId": 123 }
{ "type": "setSubscriptions", "matchIds": [1,2,3] }
{ "type": "ping" }
Server → Client
{ "type": "welcome" }
{ "type": "subscribed", "matchId": 123 }
{ "type": "commentary", "data": { ... } }
{ "type": "pong" }
{ "type": "error", "code": "match_not_found" }
⚙️ System Limits

Max subscriptions per socket: 50

Rate limit: 10 messages/sec (20 burst)

Max payload: 1MB

Backpressure auto-close if buffer exceeds 1MB

🧠 What This Project Demonstrates

Real-time system design

WebSocket subscription architecture

Backpressure handling

Rate limiting strategies

Type-safe database access

Production-ready API structuring

📈 Future Improvements

Authentication & role-based access

Redis pub/sub for multi-instance scaling

Kafka/NATS event streaming

Admin dashboard

Docker containerization


