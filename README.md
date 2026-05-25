# Rails Base

A Docker-based template for quickly bootstrapping new Rails applications with best practices and modern tooling.

## Overview

This project provides a ready-to-use foundation for creating Rails applications in a containerized environment. It includes pre-configured Docker setup, helper scripts, and sensible defaults for both development and production.

## Features

- **Ruby** (latest stable version detected automatically at project creation)
- **Docker & Docker Compose** for consistent development environment
- **PostgreSQL** as the default database (with PostGIS support)
- **Redis** for caching and background jobs
- **Interactive project generator** with options for:
  - Database (PostgreSQL, MySQL, SQLite)
  - CSS framework (Tailwind, Bootstrap, Bulma, etc.)
  - JavaScript approach (Import maps, ESBuild, Webpack, Bun)
  - API-only mode
  - Test framework configuration
- **Development helper script** (`run`) for common tasks
- **Production-ready Dockerfile** generated from Rails and optimized with multi-stage builds

## Requirements

- Docker
- Docker Compose

## Quick Start

1. **Fork or clone this repository**

2. **Run the Rails generator:**
   ```bash
   ./rails-new
   ```

3. **The script will automatically detect** the latest stable Ruby version from Docker Hub

4. **Follow the interactive prompts** to configure your new Rails app

4. **Navigate to your new app and start developing:**
   ```bash
   cd your-app-name
   ./run build    # Build Docker images
   ./run up       # Start development server
   ```

5. **Open your browser:** http://localhost:3000

## Available Commands

The `./run` script provides convenient shortcuts for common tasks:

### Docker Operations
- `./run build` - Build Docker images
- `./run up` - Start all containers
- `./run down` - Stop containers
- `./run logs` - View container logs
- `./run cli` - Enter CLI container

### Rails Commands
- `./run rails <command>` - Run any Rails command
- `./run console` - Start Rails console
- `./run routes` - Show routes
- `./run g <generator>` - Run generators

### Database
- `./run db:migrate` - Run migrations
- `./run db:rollback` - Rollback migrations
- `./run db:reset` - Reset database
- `./run psql` - Connect to PostgreSQL

### Testing
- `./run test` - Run test suite

### Cleanup
- `./run clean` - Remove stopped containers and volumes
- `./run clean:all` - Remove everything including images

## Project Structure

```
.
├── rails-new              # Interactive Rails project generator
├── run                    # Development helper script
├── Dockerfile.development # Development Docker image
├── docker-compose.yml     # Services configuration
├── .env                   # Environment variables template
└── .dockerignore          # Docker build exclusions
```

## Configuration

### Environment Variables

The `.env` file contains default configuration:

- `UID` / `GID` - User/group IDs (match host user on Linux)
- `POSTGRES_USER` / `POSTGRES_PASSWORD` - Database credentials
- `DATABASE_URL` - PostgreSQL connection string
- `REDIS_URL` - Redis connection string

### Customization

When you run `./rails-new`, the script will:
1. **Detect the latest stable Ruby version** from Docker Hub automatically
2. Update Dockerfiles with the detected Ruby version
3. Build the base Docker image
4. Generate a new Rails application with your chosen options
5. Copy Docker configuration files into the project
6. Update all configurations with your app name and Ruby version
7. Configure the database to use environment variables

### Ruby Version

The project automatically detects and uses the latest stable Ruby version available on Docker Hub at the moment of project creation. This means:
- If Ruby 3.5 is released tomorrow, new projects will use it automatically
- No need to manually update version numbers in the template
- The detected version is pinned in the generated Dockerfiles for reproducibility

## Production Deployment

The `Dockerfile.production` is automatically generated from Rails' default Dockerfile and optimized for production use:
- Multi-stage build for smaller image size
- Jemalloc for reduced memory usage
- Non-root user for security
- Precompiled assets
- Thruster server by default

Build for production:
```bash
docker build -f Dockerfile.production -t your-app .
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is open source and available under the MIT License.

## Resources

- [Ruby on Rails Guides](https://guides.rubyonrails.org/)
- [Docker Documentation](https://docs.docker.com/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
