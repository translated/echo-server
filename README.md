# Node.js Echo Server with MySQL, PostgreSQL, and Redis

This project is a simple Echo server built with Node.js and Express that demonstrates connectivity to MySQL, PostgreSQL, and Redis databases. 
It's designed to be run in a Docker container and can be easily configured using environment variables.

# Context
Hiring purpose

## Features

- Express.js web server
- Connectivity checks for MySQL, PostgreSQL, and Redis
- Docker support for easy deployment
- Environment variable configuration
- Password redaction in connection information output

## Prerequisites

- Docker
- Docker Compose (optional, for using docker-compose.yml)
- Access to MySQL, PostgreSQL, and Redis databases

## Quick Start

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/nodejs-echo-server.git
   cd nodejs-echo-server
   ```
2. Copy `.env.txt` to `.env` and fill the `.env` file with the relevant informations. 
  - `PORT`: The port the server will listen on (default: 3000)
  - `MYSQL_HOST`: MySQL server hostname
  - `MYSQL_PORT`: MySQL server port
  - `MYSQL_USER`: MySQL username
  - `MYSQL_PASSWORD`: MySQL password
  - `MYSQL_DATABASE`: MySQL database name
  - `POSTGRES_HOST`: PostgreSQL server hostname
  - `POSTGRES_PORT`: PostgreSQL server port
  - `POSTGRES_USER`: PostgreSQL username
  - `POSTGRES_PASSWORD`: PostgreSQL password
  - `POSTGRES_DATABASE`: PostgreSQL database name
  - `REDIS_URL`: Redis connection URL

3. Build and run the Docker container:

   Using Docker Compose:
   ```
   docker-compose up --build
   ```

   Or using Docker run:
   inline env variables 
   
   ```
   docker build -t echo-server .
   docker run -p 3000:3000 \
     -e MYSQL_HOST=your_mysql_host \
     -e MYSQL_PORT=your_mysql_port \
     -e MYSQL_USER=your_mysql_user \
     -e MYSQL_PASSWORD=your_mysql_password \
     -e MYSQL_DATABASE=your_mysql_database \
     -e POSTGRES_HOST=your_postgres_host \
     -e POSTGRES_PORT=your_postgres_port \
     -e POSTGRES_USER=your_postgres_user \
     -e POSTGRES_PASSWORD=your_postgres_password \
     -e POSTGRES_DATABASE=your_postgres_database \
     -e REDIS_URL=your_redis_url \
     --network existing_network \
     echo-server
   ```
   using .env file
   ```
   docker build -t echo-server .
   docker run -p 3000:3000 \
     --env-file .env \
     --network existing_network \
     echo-server
   ```

4. Access the server at `http://localhost:3000`

## API Endpoints

- `GET /`: Returns a JSON object with the server status and connection information for MySQL, PostgreSQL, and Redis.

Example response:

```json
{
  "message": "Echo server is running!",
  "mysql": {
    "connected": true,
    "connectionInfo": "mysql://user:****@mysql-host:3306/mydatabase"
  },
  "postgres": {
    "connected": true,
    "connectionInfo": "postgresql://user:****@postgres-host:5432/mydatabase"
  },
  "redis": {
    "connected": true,
    "connectionInfo": "redis://user:****@redis-host:6379"
  }
}
```

## Development

To run the server locally for development:

1. Install dependencies:
   ```
   npm install
   ```

2. Start the server:
   ```
   npm run dev
   ```

This will start the server with nodemon, which will automatically restart the server when you make changes to the code.

## License

This project is licensed under the ISC License.
