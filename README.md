# MySQL Backup Script

This script is designed to perform MySQL backups using `mysqldump` and send email notifications using `ssmtp`. It supports configuration through a dedicated configuration file.

## Features

- Perform MySQL backups for specified databases.
- Email notifications on backup success and errors.
- Configurable backup directory and retention period.
- Ignore specified databases during the backup process.

## Installation

### Prerequisites

- **MySQL Client Tools**: Ensure that `mysql` and `mysqldump` binaries are installed on your system.
- **ssmtp**: Install `ssmtp` for sending email notifications.

    ```bash
    # On Debian/Ubuntu
    sudo apt-get install ssmtp

    # On Red Hat-based systems
    sudo yum install ssmtp
    ```

### Configuration

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/mysql-backup-script.git
    cd mysql-backup-script
    ```

2. Create a configuration file named `config.cfg`:

    ```ini
    # config.cfg

    # Email settings
    ADMIN_EMAIL="your_email@example.com"
    MAIL_SUBJECT_SUCCESS="MySQL Backup Success"
    MAIL_SUBJECT_ERRORS="MySQL Backup Errors"

    # SMTP settings
    SMTP_HOST="smtp.yourprovider.com"
    SMTP_PORT="587"
    SMTP_USERNAME="your_smtp_username"
    SMTP_PASSWORD="your_smtp_password"

    # Backup settings
    BACKUP_DIR="/opt/backup/sql/"
    BACKUP_RETENTION_DAYS=30
    ```

    Adjust the settings according to your environment.

3. Create a MySQL client configuration file named `client.cnf` with appropriate MySQL credentials:

    ```ini
    # client.cnf

    [client]
    user=your_mysql_user
    password=your_mysql_password
    host=your_mysql_host  # Add the MySQL host if it's not the local host

    # Additional MySQL configurations if needed
    ```

    Replace `your_mysql_user`, `your_mysql_password`, and `your_mysql_host` with your MySQL credentials.

### Set Executable Permissions

Make sure the script is executable by running the following command:

```bash
chmod +x backupSql
```

### Usage

Run the backup script:

```bash
./backupSql
```

### Schedule the Script with Cron

To run the script automatically at a specific time each day, you can use cron. Open the crontab file for editing:

```bash
crontab -e
```

Add the following line to run the script, for example, every day at midnight:

```bash
0 0 * * * /path/to/your/script/backupSql
```

This cron expression represents "every day at midnight." Adjust the timing as needed. Save and exit the editor.

For additional help with cron expressions, you can use online tools like [CronTab Guru](https://crontab.guru/) to generate the appropriate schedule.

Remember to replace /path/to/your/script/ with the actual path to your script.

Now, the backup script will be executed automatically according to the specified schedule.
