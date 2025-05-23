# Telegram Channel Scraper 📱

A powerful Python script that allows you to scrape messages & media from Telegram channels using the Telethon library. Features include real-time continuous scraping, media downloading, and data export capabilities!

```
___________________  _________
\__    ___/  _____/ /   _____/
  |    | /   \  ___ \_____  \ 
  |    | \    \_\  \/        \
  |____|  \______  /_______  /
                 \/        \/
```
## Features 🚀

- Scrape messages from multiple Telegram channels
- Download media files (photos, documents)
- Real-time continuous scraping
- Export data to JSON and CSV formats
- SQLite database storage
- Resume capability (saves progress)
- Media reprocessing for failed downloads
- Progress tracking
- Interactive menu interface

## Prerequisites 📋

Before running the script, you'll need:

- Python 3.7 or higher
- Telegram account
- API credentials from Telegram

### Required Python packages

```
pip install -r requirements.txt
```

Contents of `requirements.txt`:
```
telethon
aiohttp
asyncio
```

## Getting Telegram API Credentials 🔑

1. Visit https://my.telegram.org/auth
2. Log in with your phone number
3. Click on "API development tools"
4. Fill in the form:
   - App title: Your app name
   - Short name: Your app short name
   - Platform: Can be left as "Desktop"
   - Description: Brief description of your app
5. Click "Create application"
6. You'll receive:
   - `api_id`: A number
   - `api_hash`: A string of letters and numbers
   
Keep these credentials safe, you'll need them to run the script!.
## Setup and Running 🔧

1. Clone the repository:
```bash
git clone https://github.com/unnohwn/telegram-scraper.git
cd telegram-scraper
```

2. Install requirements:
```bash
pip install -r requirements.txt
```

3. Run the script:
```bash
python telegram-scraper.py
```

4. On first run, you'll be prompted to enter:
   - Your API ID
   - Your API Hash
   - Your phone number (with country code)
   - Your phone number (with country code) or bot, but use the phone number option when prompted second time.
   - Verification code (sent to your Telegram)

## Initial Scraping Behavior 🕒

When scraping a channel for the first time, please note:

- The script will attempt to retrieve the entire channel history, starting from the oldest messages
- Initial scraping can take several minutes or even hours, depending on:
  - The total number of messages in the channel
  - Whether media downloading is enabled
  - The size and number of media files
  - Your internet connection speed
  - Telegram's rate limiting
- The script uses pagination and maintains state, so if interrupted, it can resume from where it left off
- Progress percentage is displayed in real-time to track the scraping status
- Messages are stored in the database as they are scraped, so you can start analyzing available data even before the scraping is complete

## Usage 📝

The script provides an interactive menu with the following options:

- **[A]** Add new channel
  - Enter the channel ID or channelname
- **[R]** Remove channel
  - Remove a channel from scraping list
- **[S]** Scrape all channels
  - One-time scraping of all configured channels
- **[M]** Toggle media scraping
  - Enable/disable downloading of media files
- **[C]** Continuous scraping
  - Real-time monitoring of channels for new messages
- **[E]** Export data
  - Export to JSON and CSV formats
- **[V]** View saved channels
  - List all saved channels
- **[L]** List account channels
  - List all channels with ID:s for account
- **[Q]** Quit

### Channel IDs 📢

You can use either:
- Channel username (e.g., `channelname`)
- Channel ID (e.g., `-1001234567890`)

## Data Storage 💾

### Database Structure

Data is stored in SQLite databases, one per channel:
- Location: `./channelname/channelname.db`
- Table: `messages`
  - `id`: Primary key
  - `message_id`: Telegram message ID
  - `date`: Message timestamp
  - `sender_id`: Sender's Telegram ID
  - `first_name`: Sender's first name
  - `last_name`: Sender's last name
  - `username`: Sender's username
  - `message`: Message text
  - `media_type`: Type of media (if any)
  - `media_path`: Local path to downloaded media
  - `reply_to`: ID of replied message (if any)

### Media Storage 📁

Media files are stored in:
- Location: `./channelname/media/`
- Files are named using message ID or original filename

### Exported Data 📊

Data can be exported in two formats:
1. **CSV**: `./channelname/channelname.csv`
   - Human-readable spreadsheet format
   - Easy to import into Excel/Google Sheets

2. **JSON**: `./channelname/channelname.json`
   - Structured data format
   - Ideal for programmatic processing

## Features in Detail 🔍

### Continuous Scraping

The continuous scraping feature (`[C]` option) allows you to:
- Monitor channels in real-time
- Automatically download new messages
- Download media as it's posted
- Run indefinitely until interrupted (Ctrl+C)
- Maintains state between runs

### Media Handling

The script can download:
- Photos
- Documents
- Other media types supported by Telegram
- Automatically retries failed downloads
- Skips existing files to avoid duplicates

## Error Handling 🛠️

The script includes:
- Automatic retry mechanism for failed media downloads
- State preservation in case of interruption
- Flood control compliance
- Error logging for failed operations

## Limitations ⚠️

- Respects Telegram's rate limits
- Can only access public channels or channels you're a member of
- Media download size limits apply as per Telegram's restrictions

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request.

## License 📄

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer ⚖️

This tool is for educational purposes only. Make sure to:
- Respect Telegram's Terms of Service
- Obtain necessary permissions before scraping
- Use responsibly and ethically
- Comply with data protection regulations
