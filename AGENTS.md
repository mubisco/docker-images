# AGENTS.md

## Project Overview
This repository contains Docker image configurations for development environments, primarily focused on Node.js and PHP development containers.

## Directory Structure

### `/node`
Contains Node.js development environment Docker images based on Alpine Linux.

#### `/node/22.21.0` (LTS - Jod)
**Key Features:**
- Base: `node:22.21.0-alpine`
- Includes development tools: neovim, git, curl, zsh
- Pre-configured with oh-my-zsh
- Vite pre-installed globally
- Default port: 3000 (configurable via ARG)
- Runs as non-root `node` user

#### `/node/23.7.0`
**Key Features:**
- Base: `node:23.7.0-alpine`
- Includes development tools: neovim, git, curl, zsh
- Pre-configured with oh-my-zsh
- Vite pre-installed globally
- Default port: 3000 (configurable via ARG)
- Runs as non-root `node` user

### `/php84`
Contains a PHP 8.4 development environment Docker image based on Alpine Linux.

**Key Features:**
- Base: `alpine:3.21`
- PHP 8.4 with FPM
- Extensive PHP extensions (bcmath, curl, dom, gd, intl, mbstring, mysqlnd, opcache, pdo, etc.)
- Custom PHP configuration files:
  - `php.ini` - Main PHP configuration
  - `xdebug-custom.ini` - Xdebug configuration
  - `zz-docker.conf` - PHP-FPM Docker-specific configuration
- Development tools: neovim, git, curl, zsh

## Usage

### Building Images

**Node.js images:**
```bash
# LTS version (recommended)
cd node/22.21.0
docker build -t your-node-image:22.21.0-lts .

# Latest version
cd node/23.7.0
docker build -t your-node-image:23.7.0 .
```

**PHP 8.4 image:**
```bash
cd php84
docker build -t your-php84-image:latest .
```

### Customization

Both images support build arguments for customization:
- Node image: `USER_ID`, `PORT`
- Refer to individual Dockerfiles for specific configuration options

## Purpose
These Docker images are designed for:
- Local development environments
- Consistent development setups across team members
- CI/CD pipeline integration
- Testing and debugging applications

## Notes
- All images are based on Alpine Linux for minimal footprint
- Development tools are pre-installed for convenience
- Images are configured to run as non-root users when possible for security
