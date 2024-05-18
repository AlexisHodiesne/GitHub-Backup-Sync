# GitHub Backup Sync

This script automates the backup of your development projects to a local directory every time you push changes to GitHub.

## Usage

1. Clone the project locally.
2. Navigate to the `.git/hooks` directory.
3. Make the file executable:
    ```sh
    chmod +x post-push
    ```
4. Modify the variables in the script according to your setup:
    - `BACKUP_DIR`: Set the path for the local backup directory.
    - `ENABLE_LOG`: Set to `true` to enable logging, or `false` to disable it.
    - `LOG_FILE`: Specify the path for the log file if logging is enabled (default is '/logs').
5. Push changes to your GitHub repository. The script will automatically create a backup of your project in the specified directory.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
