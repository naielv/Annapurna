# Annapurna Docker Compose Example

This example demonstrates how to run Annapurna with Docker Compose.

## Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/naielv/Annapurna.git
   cd Annapurna
   ```

2. **Create data directories** (optional - Docker will create them automatically):
   ```bash
   mkdir -p data/L1
   mkdir -p data/License
   ```

3. **Start the application**:
   ```bash
   docker compose up -d
   ```

4. **Access the application**:
   Open your browser and navigate to: http://localhost:8080

5. **View logs**:
   ```bash
   docker compose logs -f
   ```

6. **Stop the application**:
   ```bash
   docker compose down
   ```

## Architecture

The `docker-compose.yml` file defines a single service:

- **annapurna**: Flask-based web application that serves both the backend API and frontend UI
  - **Port**: 8080 (mapped to host port 8080)
  - **Volumes**:
    - `./data/L1` → `/DATA/L1` (User data files)
    - `./data/License` → `/DATA/License` (License files)

## Customization

### Change Port

To run on a different port, edit the `ports` section in `docker-compose.yml`:

```yaml
ports:
  - "3000:8080"  # Access at http://localhost:3000
```

### Data Persistence

User data and licenses are stored in the `./data/` directory by default. These volumes ensure data persists even when the container is stopped or removed.

### Production Deployment

For production use, consider:
- Using environment variables for configuration
- Setting up HTTPS with a reverse proxy (nginx, Traefik, etc.)
- Configuring proper backup for the data volumes
- Reviewing security settings

## Troubleshooting

### Container won't start

Check the logs:
```bash
docker compose logs annapurna
```

### Port already in use

If port 8080 is already in use, change the port mapping in docker-compose.yml or stop the conflicting service.

### Permission issues with volumes

Ensure the user running Docker has permission to access the `./data/` directory.

## License

See the LICENSE file in the repository.
