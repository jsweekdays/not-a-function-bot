# Not-a-Function Spam Bot for JsWeekdays

A Telegram bot designed to help moderate and manage the JsWeekdays community by detecting and handling spam messages. This bot uses the [tg-spam](https://github.com/umputun/tg-spam) service for spam detection.

## Features

- Automated spam detection using [tg-spam](https://github.com/umputun/tg-spam)
- Automatic updates of spam detection samples
- Telegram group moderation
- Admin notifications for suspicious messages
- Real-time message processing
- Docker containerization for easy deployment

## Prerequisites

Before running the bot, make sure you have:

- Docker and Docker Compose installed
- A Telegram Bot Token (obtainable from [@BotFather](https://t.me/botfather))
- An OpenAI API key
- Admin access to your Telegram group

## Environment Variables

The following environment variables are required:

- `TELEGRAM_TOKEN`: Your Telegram bot token
- `TELEGRAM_GROUP`: ID of the Telegram group to moderate
- `OPENAI_TOKEN`: Your OpenAI API key
- `ADMIN_GROUP`: ID of the Telegram group for admin notifications

## Project Structure

The project uses Docker Compose with three services:

1. `tg-spam`: Main spam detection service
2. `tg-spam-updater`: Service that keeps spam samples up to date
3. `watchtower`: Automatic container updates (checks every 30 seconds)

### Volumes

The following directories are used for persistent storage:

- `./data`: General data directory
- `./log`: Log files
- `./tg-spam-samples`: Spam detection samples
- `./tg-spam-dynamic`: Dynamic spam detection data

## Installation and Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/not-a-function-bot.git
   cd not-a-function-bot
   ```

2. Create necessary directories:
   ```bash
   mkdir -p data log tg-spam-samples tg-spam-dynamic
   ```

3. Set up your environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your actual values
   ```

4. Start the services:
   ```bash
   docker-compose up -d
   ```

## Service Configuration

### tg-spam Service

- Logging enabled with JSON format
- Max log size: 10MB with 5 rotations
- Debug mode enabled
- No spam reply mode enabled

### tg-spam-updater Service

- Updates spam samples from the official repository
- Samples stored in `/samples` directory

### Watchtower Service
- Automatically updates containers
- Checks for updates every 30 seconds

## Logs

Logs are stored in the `./log` directory with a maximum size of 5MB per file. You can view the logs using:

```bash
docker-compose logs -f tg-spam
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For support, please join our [Telegram group](https://t.me/jsweekdays) or open an issue in this repository.

## Acknowledgments

- [tg-spam](https://github.com/umputun/tg-spam) for spam detection
- JsWeekdays community
- OpenAI for providing the AI capabilities
- Telegram Bot API
