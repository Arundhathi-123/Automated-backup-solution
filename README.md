#!/bin/bash

# Configuration
SOURCE_DIR="/path/to/source/directory"  # Directory to back up
REMOTE_USER="username"                    # Remote server username
REMOTE_HOST="remote.server.com"           # Remote server address
REMOTE_DIR="/path/to/remote/backup"       # Remote backup directory
LOG_FILE="/var/log/backup.log"             # Log file for backup reports
DATE=$(date '+%Y-%m-%d %H:%M:%S')

# Function to log messages
log_message() {
    echo "$DATE - $1" >> "$LOG_FILE"
}

# Start backup
log_message "Starting backup of $SOURCE_DIR to $REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR"

# Perform the backup using rsync
rsync -avz --delete "$SOURCE_DIR/" "$REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR" > /dev/null 2>&1

# Check the exit status of rsync
if [ $? -eq 0 ]; then
    log_message "Backup completed successfully."
else
    log_message "ERROR: Backup failed."
fi

# End of script# Automated-backup-solution
