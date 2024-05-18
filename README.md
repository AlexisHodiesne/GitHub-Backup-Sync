# GitHub Backup Sync

GitHub Backup Sync is a script to automate the backup of your development projects to a local backup directory every time you push to GitHub.

## Installation

1. Clone your project locally.
2. Navigate to the `.git/hooks` directory of your project.
3. Create the `post-push` file and make it executable:
    ```sh
    touch post-push
    chmod +x post-push
    ```
4. Add the copy script to `post-push` (see below).

## Script `post-push`

```sh
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
```

## Configuration

- **Logs**:
  - You can enable or disable logging with the `ENABLE_LOG` variable. Set it to `true` to enable logging and `false` to disable it.
  - The path for the log file should be set in `LOG_FILE`.

- **Backup**:
  - Set the backup path in `BACKUP_DIR`.
