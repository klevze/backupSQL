# MySQL Backup Script

This script is designed to perform MySQL backups using `mysqldump` and send notifications through  Telegram. It supports configuration through dedicated configuration files.

## New Features

- **Telegram Integration:** Receive backup status messages on Telegram.
- **Colorized Output:** The script now provides color-coded output for better readability.
- **Improved Configuration:** Additional options and improved organization in the configuration files.

## Installation and Upgrade

### Prerequisites

Ensure that the required dependencies are installed:

- **MySQL Client Tools:** `mysql` and `mysqldump` binaries.
- **cURL:** Used for Telegram integration.

### Installation

1. **Clone the Repository:**

    Clone the repository to your local machine:

    ```bash
    git clone https://github.com/klevze/backupSQL.git
    cd backupSQL
    ```

2. **Create Configuration Files:**

    Create a configuration file named `backup.cnf` with the following content:

    ```bash
    # Backup settings
    BACKUP_DIR="/opt/backup/sql/"
    BACKUP_RETENTION_DAYS=30

    # Telegram
    TELEGRAM_TOKEN=
    TELEGRAM_CHATID=
    TELEGRAM_SERVERID=ServerName
    TELEGRAM_ENABLE=false
    ```

### Backup settings

The options `BACKUP_DIR` and `BACKUP_RETENTION_DAYS` in the configuration file play a crucial role in the MySQL backup script. Here's a description of each:

1. **`BACKUP_DIR="/opt/backup/sql/"`**

- This option specifies the directory where the MySQL backups will be stored.
- In the provided example, the backups will be saved in the `/opt/backup/sql/` directory.
- It's important to ensure that the specified directory exists and that the script has the necessary permissions to write to it.
- Customize this option based on your server's file system structure and storage preferences.

2. **`BACKUP_RETENTION_DAYS=30`**

- This option determines the retention period for the backups, specifically how many days the backups will be retained before being considered for deletion.
- In the provided example, backups older than 30 days will be removed from the backup directory.
- Adjust this value based on your backup retention policy and available storage capacity.
- A longer retention period provides a historical backup archive, while a shorter period might be necessary for systems with limited storage.

These configuration options allow you to tailor the backup script to your specific storage and retention requirements. It's important to regularly monitor the available disk space and adjust the retention period accordingly to avoid unnecessary storage consumption.

### Telegram

```bash
TELEGRAM_TOKEN=
TELEGRAM_CHATID=
TELEGRAM_SERVERID=ServerName
TELEGRAM_ENABLE=false
```

Create a MySQL client configuration file named `client.cnf` with appropriate MySQL credentials:

```bash
[client]
user=your_mysql_user
password=your_mysql_password
host=localhost
```

### Set Executable Permissions

Make sure the script is executable by running the following command:

`chmod +x backupSql`

### Usage

Run the backup script:

`./backupSql`

### Schedule the Script with Cron

To run the script automatically at a specific time each day, you can use cron. Open the crontab file for editing:

`crontab -e`

Add the following line to run the script, for example, every day at midnight:

`0 0 * * * /path/to/your/script/backupSql`

This cron expression represents "every day at midnight." Adjust the timing as needed. Save and exit the editor.

For additional help with cron expressions, you can use online tools like [CronTab Guru](https://crontab.guru/) to generate the appropriate schedule.

Remember to replace `/path/to/your/script/` with the actual path to your script.

Now, the backup script will be executed automatically according to the specified schedule.

# Setting Up a Telegram Bot

Telegram bots are special accounts designed to perform specific tasks. In this tutorial, we'll walk through the process of creating a Telegram bot and obtaining the necessary credentials to integrate it with your MySQL backup script.

## Step 1: Create a Telegram Account

If you don't have a Telegram account, download the Telegram app from [official website](https://telegram.org/) or your app store and create an account.

## Step 2: Create a New Telegram Bot

1. Open Telegram and search for the "BotFather" bot. This bot is responsible for creating and managing other bots.

2. Start a chat with the BotFather and use the `/newbot` command to create a new bot.

3. Follow the instructions to choose a name and username for your bot. Once completed, the BotFather will provide you with a unique API token for your bot.

## Step 3: Obtain Your Telegram Chat ID

To receive messages from your bot, you need to know your Telegram chat ID.

1. Start a chat with your newly created bot.

2. Send any message to the bot.

3. Open a web browser and go to the following URL, replacing `YOUR_BOT_TOKEN` with the actual token obtained from the BotFather:

`https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates`

4. Look for the `"chat"` object in the response. The value of `"id"` inside the `"chat"` object is your Telegram chat ID.

## Step 4: Update Your Backup Configuration

Now that you have the Telegram bot token and chat ID, update your `backup.cnf` configuration file:

```ini
# Backup settings
BACKUP_DIR="/opt/backup/sql/"
BACKUP_RETENTION_DAYS=30

# Telegram
TELEGRAM_TOKEN=YOUR_BOT_TOKEN
TELEGRAM_CHATID=YOUR_CHAT_ID
TELEGRAM_SERVERID=ServerName
TELEGRAM_ENABLE=true
```

Replace `YOUR_BOT_TOKEN` and `YOUR_CHAT_ID` with the values obtained from the BotFather and your chat with the bot, respectively.

## Step 5: Enable Telegram Integration

Set `TELEGRAM_ENABLE=true` in your `backup.cnf` to enable Telegram integration.

```ini
# Telegram
TELEGRAM_ENABLE=true
```

## Step 6: Save and Run the Backup Script

Save your `backup.cnf` file and run the MySQL backup script. If everything is configured correctly, you should receive Telegram messages about the backup status.

----------

That's it! You've successfully set up a Telegram bot and integrated it with your MySQL backup script. Now, you'll receive status messages directly on Telegram.
