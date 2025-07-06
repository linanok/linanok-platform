<p align="center">
  <a href="https://linanok.com" target="_blank">
    <img src="https://raw.githubusercontent.com/linanok/linanok/main/logo.svg" width="300" alt="Linanok Logo">
  </a>
</p>

# Linanok Platform

This repository contains the prebuilt Docker images for Linanok Platform - a professional URL shortening application designed for organizations and companies.

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/linanok/linanok-platform.git
   cd linanok-platform
   ```

2. **Start with Docker:**
   ```bash
   # Edit the default .env file with your settings
   docker-compose up -d
   ```

3. **Create admin user:**
   ```bash
   docker-compose exec app php artisan make:super-admin
   ```

The application will be available at `http://localhost:8000`
