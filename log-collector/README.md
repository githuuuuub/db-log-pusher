# DB Log Collector Service

This is a tiny log collector service that receives logs from the DB Log Pusher plugin and stores them in a MySQL database.

## Overview

The DB Log Collector service is a lightweight HTTP server that receives log entries from the Wasm plugin and stores them in a MySQL database. It supports batch insertion for performance and provides querying capabilities.

## Features

- Receives log entries via HTTP POST at `/ingest`
- Stores logs in MySQL database with complete access log fields, including request and response bodies
- Supports batch insertion for improved performance
- Provides querying capabilities via `/query` endpoint
- Includes health check endpoint at `/health`

## Configuration

The service can be configured using the following environment variables:

- `MYSQL_DSN`: MySQL Data Source Name (default: root:root@tcp(127.0.0.1:3306)/higress_poc?charset=utf8mb4&parseTime=True)
- `PORT`: Port to listen on (default: 8080)

## Endpoints

- `POST /ingest`: Receive log entries from the plugin
- `GET /query`: Query stored logs with various filters
- `GET /health`: Health check endpoint

## Database Schema

The service creates the `access_logs` table on startup if it does not exist, and ensures the expected indexes are present. The table stores basic request information, response details, traffic metrics, upstream information, connection details, routing information, AI logs, monitoring metadata, token usage statistics, and request/response bodies.
