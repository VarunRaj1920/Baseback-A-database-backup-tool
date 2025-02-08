# Baseback: A CLI Tool for database backup

A robust command-line interface tool for managing database backups and restorations across multiple database management systems. This utility supports various backup types, cloud storage integration, and automated notifications.

## Features

### Database Support
- Multiple DBMS support (MySQL, PostgreSQL, MongoDB)
- Secure connection handling with configurable parameters
- Connection testing and validation
- Comprehensive error handling

### Backup Capabilities
- Multiple backup types:
  - Full backup
  - Incremental backup
  - Differential backup
- Built-in compression to optimize storage
- Progress monitoring during operations

### Storage Management
- Local storage with customizable paths
- Cloud storage integration:
  - Amazon S3
  - Google Cloud Storage
  - Azure Blob Storage
- Automatic backup rotation and cleanup

### Monitoring & Notifications
- Detailed operation logging
- Slack notifications for operation status
- Operation metrics (duration, size, status)

### Recovery Options
- Full database restoration
- Selective table/collection recovery
- Point-in-time recovery options

## Installation

1. Clone the repository:
```bash
git clone https://github.com/your-username/db-backup-tool.git
cd db-backup-tool
```

2. Create and activate virtual environment:
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Unix/MacOS
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Configuration

1. Copy the example configuration file:
```bash
cp config/db_config.example.json config/db_config.json
```

2. Edit `config/db_config.json` with your settings:
```json
{
    "databases": {
        "mysql": {
            "host": "localhost",
            "port": 3306,
            "username": "your_username",
            "password": "your_password",
            "database": "your_database"
        }
    },
    "storage": {
        "cloud": {
            "provider": "s3",
            "aws_access_key": "your_access_key",
            "aws_secret_key": "your_secret_key",
            "bucket": "your-backup-bucket"
        }
    },
    "notification": {
        "slack": {
            "webhook_url": "your_slack_webhook_url"
        }
    }
}
```

## Usage

### Basic Commands

1. Create a full backup:
```bash
python src/cli.py backup --type full --db mysql
```

2. Create an incremental backup:
```bash
python src/cli.py backup --type incremental --db mysql
```

3. Restore from backup:
```bash
python src/cli.py restore --backup-file backups/backup_2024_02_08.sql.gz --db mysql
```

### Advanced Usage

1. Backup with cloud storage:
```bash
python src/cli.py backup --type full --db postgresql --storage s3 --bucket my-backups
```

2. Selective table restore:
```bash
python src/cli.py restore --backup-file backup.sql.gz --db mysql --tables users,orders
```

3. Backup with compression and notification:
```bash
python src/cli.py backup --type full --db mongodb --compress --notify
```

## Logging

- All operations are logged to `logs/backup.log`
- Log format includes:
  - Timestamp
  - Operation type
  - Status
  - Duration
  - Error details (if any)

## Best Practices

1. Regular Testing
   - Test restore operations periodically
   - Verify backup integrity
   - Monitor backup sizes and timing

2. Security
   - Use strong database credentials
   - Encrypt backup files when possible
   - Regularly rotate access keys

3. Performance
   - Schedule backups during off-peak hours
   - Monitor system resources during operations
   - Use incremental backups when possible

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Built using Python 3.x
- Supports cross-platform operation
- Inspired by industry backup best practices
