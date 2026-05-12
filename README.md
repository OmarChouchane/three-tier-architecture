# AWS Three-Tier Architecture

Production-style three-tier web application on AWS with separated presentation, application, and data layers.

## Architecture Diagram

![alt text](aws-three-tier-architecture.png)

## Project Scope

- Frontend tier: Static UI (HTML/CSS/JavaScript) served by NGINX
- Application tier: PHP API endpoints for message read/write operations
- Data tier: MySQL database for persistent storage

## AWS Design

- Public-facing Web ALB routes traffic to NGINX instances
- Frontend EC2 instances run in an Auto Scaling Group
- Internal/App ALB routes API traffic to PHP instances
- Backend EC2 instances run in an Auto Scaling Group
- Amazon RDS MySQL hosts application data

## Repository Structure

```text
three-tier-architecture/
├── frontend/
│   ├── index.html
│   └── styles.css
├── backend/
│   └── api/
│       ├── db_connection.php
│       ├── get_messages.php
│       └── save_message.php
├── database/
│   └── database_setup.sql
└── infrastructure/
    ├── backend_server.md
    ├── frontend_server.md
    └── nginx_config
```

## Core Functionality

- Submit a message through the frontend
- Persist messages in MySQL
- Retrieve and display stored messages

## Local Validation

### Prerequisites

- PHP-enabled web server (Apache or NGINX + PHP-FPM)
- MySQL Server

### Setup

1. Create a MySQL database and run `database/database_setup.sql`.
2. Update backend database credentials in `backend/api/db_connection.php`.
3. Serve the `frontend/` directory from a local web server.
4. Serve the PHP API from the `backend/api/` path.
5. Verify read/write flow using the frontend UI.

## Infrastructure Notes

- Server setup references are documented in `infrastructure/frontend_server.md` and `infrastructure/backend_server.md`.
- NGINX configuration reference is available in `infrastructure/nginx_config`.

## Security and Hardening

Current implementation is focused on architecture and functional flow. For production use, add:

- HTTPS termination and certificate management
- Authentication and authorization
- Strict input validation and sanitization
- Secrets management (no plaintext credentials)
- Monitoring, alerting, and centralized logging

## License

MIT
