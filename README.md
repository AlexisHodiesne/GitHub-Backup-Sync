# GitHub Backup Sync

GitHub Backup Sync is a script to automate the backup of your development projects to a local backup directory every time you push to GitHub.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Installation

1. Clone your project locally.
2. Navigate to the `.git/hooks` directory of your project (could be a hidden folder).
3. Create the `post-push` file and make it executable:
```sh
echo '
#!/bin/bash

# Variables
PROJECT_DIR="$(git rev-parse --show-toplevel)"
BACKUP_DIR="/path/to/backup/location"
LOG_FILE="/path/to/backup/logs/post-push.log"
ENABLE_LOG=true

# Copy function
copy_project() {
    if [ "$ENABLE_LOG" = true ]; then
        echo "$(date '+%Y-%m-%d %H:%M:%S') - Starting project copy" >> "$LOG_FILE"
        rsync -av --delete "$PROJECT_DIR/" "$BACKUP_DIR/" >> "$LOG_FILE" 2>&1
        if [ $? -eq 0 ]; then
            echo "$(date '+%Y-%m-%d %H:%M:%S') - Project copy completed successfully" >> "$LOG_FILE"
        else
            echo "$(date '+%Y-%m-%d %H:%M:%S') - Project copy failed" >> "$LOG_FILE"
        fi
    else
        rsync -av --delete "$PROJECT_DIR/" "$BACKUP_DIR/"
    fi
}

# Execute the copy function
copy_project
' > post-push && chmod +x post-push
```

## Configuration
Before using the script, make sure to configure the following variables according to your setup:

BACKUP_DIR: Set the path for the backup directory.

ENABLE_LOG: Set to true to enable logging, or false to disable it.

LOG_FILE: Specify the path for the log file if logging is enabled.
