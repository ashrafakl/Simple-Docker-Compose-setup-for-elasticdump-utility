# Elasticdump Docker Setup

Simple Docker Compose setup for elasticdump utility.

## Quick Start

1. Start the container:
```bash
docker-compose up -d
```

2. Use elasticdump commands:
```bash
docker-compose exec elasticdump elasticdump --help
```

## Basic Usage

### Copy an index
```bash
docker-compose exec elasticdump elasticdump \
  --input=http://your-source-host:9200/index-name \
  --output=http://your-target-host:9200/index-name \
  --type=data
```

### Backup to file
```bash
docker-compose exec elasticdump elasticdump \
  --input=http://your-host:9200/index-name \
  --output=/backups/backup.json \
  --type=data
```

### Restore from file
```bash
docker-compose exec elasticdump elasticdump \
  --input=/backups/backup.json \
  --output=http://your-host:9200/index-name \
  --type=data
```

## Additional Examples

### Copy with mapping and data
```bash
# Copy mapping first
docker-compose exec elasticdump elasticdump \
  --input=http://source:9200/index-name \
  --output=http://target:9200/index-name \
  --type=mapping

# Then copy data
docker-compose exec elasticdump elasticdump \
  --input=http://source:9200/index-name \
  --output=http://target:9200/index-name \
  --type=data
```

### Restore from file
```bash
docker-compose exec elasticdump elasticdump \
  --input=/backups/backup.json \
  --output=http://your-host:9200/index-name \
  --type=data
```

## File Storage

The `./backups` directory is mounted to the container for file operations. All backup files will be saved here.

## Cleanup

Stop the container:
```bash
docker-compose down
```
