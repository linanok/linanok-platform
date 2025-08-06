<p align="center">
  <a href="https://linanok.com" target="_blank">
    <img src="https://raw.githubusercontent.com/linanok/linanok/main/logo.svg" width="300" alt="Linanok Logo">
  </a>
</p>

# Linanok Platform

Linanok is a professional URL shortening application designed for organizations and companies. This repository
provides prebuilt Docker images and an easy deployment process.

> **Note:** The prebuilt Docker images only support PostgreSQL as the database backend. If you need to use a different
> database, you'll need to build the images from [source](https://github.com/linanok/linanok).

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/linanok/linanok-platform.git
   cd linanok-platform
   ```

2. **Configure environment variables:**
    - Copy the provided `.env` file and adjust the values as needed for your environment. See
      the [Environment Variables](#environment-variables) section below for details on each variable.

3. **Start with Docker Compose:**
   ```bash
   docker-compose up -d
   ```

4. **Create an admin user:**
   ```bash
   docker-compose exec app php artisan make:super-admin
   ```

The application will be available at [http://localhost:8000](http://localhost:8000).

---

## Environment Variables

The application is configured using a `.env` file in the project root. Below is a list of all supported environment
variables and their purposes:

| Variable                     | Description                                                           | Example / Default |
|------------------------------|-----------------------------------------------------------------------|-------------------|
| `APP_ENV`                    | Application environment (`production`, `local`, etc.)                 | `production`      |
| `APP_KEY`                    | Application encryption key (generate with `php artisan key:generate`) | *(secret)*        |
| `APP_DEBUG`                  | Enable debug mode (`true` or `false`)                                 | `false`           |
| `APP_TIMEZONE`               | Default timezone                                                      | `UTC`             |
| `OCTANE_WORKERS`             | Number of Octane workers                                              | `8`               |
| `QUEUE_WORKER_MAX_PROCESSES` | Maximum number of concurrent queue worker processes                   | `4`               |
| `TRUSTED_PROXIES`            | Trusted proxy IPs/subnets for Docker network                          | `172.25.0.0/16`   |
| `APP_MAINTENANCE_DRIVER`     | Maintenance mode driver                                               | `file`            |
| `BCRYPT_ROUNDS`              | Bcrypt hashing rounds                                                 | `12`              |
| `LOG_CHANNEL`                | Log channel                                                           | `stack`           |
| `LOG_STACK`                  | Log stack channel                                                     | `single`          |
| `LOG_DEPRECATIONS_CHANNEL`   | Channel for deprecation logs                                          | `null`            |
| `LOG_LEVEL`                  | Log verbosity level                                                   | `debug`           |
| `DB_CONNECTION`              | Database connection type                                              | `pgsql`           |
| `DB_HOST`                    | Database host                                                         | `postgres`        |
| `DB_PORT`                    | Database port                                                         | `5432`            |
| `DB_DATABASE`                | Database name                                                         | `linanok`         |
| `DB_USERNAME`                | Database username                                                     | `postgres`        |
| `DB_PASSWORD`                | Database password                                                     | `postgres`        |
| `SESSION_DRIVER`             | Session driver                                                        | `redis`           |
| `SESSION_LIFETIME`           | Session lifetime (minutes)                                            | `120`             |
| `SESSION_ENCRYPT`            | Encrypt session data (`true` or `false`)                              | `false`           |
| `SESSION_PATH`               | Session cookie path                                                   | `/`               |
| `SESSION_DOMAIN`             | Session cookie domain                                                 | `null`            |
| `FILESYSTEM_DISK`            | Default filesystem disk                                               | `local`           |
| `QUEUE_CONNECTION`           | Queue connection type                                                 | `database`        |
| `CACHE_STORE`                | Cache store                                                           | `redis`           |
| `CACHE_PREFIX`               | Cache key prefix                                                      | *(empty)*         |
| `REDIS_CLIENT`               | Redis client                                                          | `predis`          |
| `REDIS_HOST`                 | Redis host                                                            | `redis`           |
| `REDIS_PASSWORD`             | Redis password                                                        | `null`            |
| `REDIS_PORT`                 | Redis port                                                            | `6379`            |
| `REDIS_DB`                   | Redis database index                                                  | `0`               |
| `REDIS_CACHE_DB`             | Redis cache database index                                            | `1`               |
| `REDIS_CACHE_CONNECTION`     | Redis cache connection name                                           | `cache`           |

> **Note:**
> - The queue worker is managed by [Laravel Horizon](https://laravel.com/docs/horizon), which requires
    `QUEUE_CONNECTION=redis` in your `.env` file. Horizon only supports Redis as the queue backend.
> - Some variables are required for the application to function correctly (e.g., `APP_KEY`, database credentials).
> - Adjust values as needed for your deployment and security requirements.

---

## Production Recommendations

To ensure a secure and reliable production deployment, consider the following best practices:

- **Set a strong, unique `APP_KEY`**: Never use the default or example key in production. Generate a new key with
  `php artisan key:generate`.
- **Disable debug mode**: Set `APP_DEBUG=false` to prevent sensitive information from being exposed.
- **Use secure passwords**: Change all default database and Redis passwords to strong, unique values.
- **Restrict trusted proxies**: Set `TRUSTED_PROXIES` to only include your actual proxy or Docker network range.
- **Configure backups**: Regularly back up your database and Redis data volumes.
- **Use HTTPS**: Deploy behind a reverse proxy or load balancer that provides SSL/TLS encryption.
- **Monitor logs and health**: Set up log monitoring and use the built-in health checks for all services.
- **Resource tuning**: Adjust worker counts and resource limits based on your expected load and available hardware.
- **Keep images up to date**: Regularly update Docker images to receive security and performance improvements.
