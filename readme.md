# 🤖 WhatsApp AI Personal Bot

This is a **personal chatbot project integrated with WhatsApp**, designed to automatically reply to messages in your own communication style: direct, informal, practical, and without sounding like a generic AI.

The bot uses the **OpenAI API** + **TextMeBot API** to send and receive messages on WhatsApp, and keeps a conversation history to answer in a personalized and contextualized way.

---

## 🚀 Features

✅ Receives messages via **TextMeBot Webhook**  
✅ Uses **GPT-4o-mini** to reply naturally, simulating your way of talking  
✅ Maintains a **history of the last 5 interactions** to keep context  
✅ Provides a simple web panel to:
- Enable/Disable automatic responses
- Manage allowed contacts list (up to 10 contacts)
- View message logs
✅ Uses **Web Search Tool** to answer about weather, sports, news, and real-time information  
✅ Replies only to authorized contacts

---

## 🌐 How it works

### 📥 Message Flow

```
User sends message -> Webhook (/webhook) receives it ->
Verifies if contact is authorized ->
If authorized -> Calls OpenAI API with historical context ->
Generates a "human-like" reply ->
Sends reply via TextMeBot API ->
Logs the conversation
```

---

## 🗂️ Project Structure

```
📂 Project Root
├── allowed_contacts.txt     # Authorized contacts
├── config.txt               # Global settings
├── messages.log             # Conversation log
├── .env                     # Environment variables (API Keys)
├── app.py                   # Main application code
├── templates/
│   └── index.html           # Web configuration panel
└── README.md                # This file
```

---

## ⚙️ How to Use

### 1) Configure your `.env` file

Create a `.env` file with:

```
API_KEY_TEXTMEBOT=YOUR_TEXTMEBOT_API_KEY
```

### 2) Install dependencies

```bash
pip install flask openai python-dotenv requests
```

### 3) Run the server

```bash
python app.py
```

Access the configuration panel at:

```
http://localhost:3838
```

### 4) Configure Webhook on TextMeBot

Set the webhook URL in your TextMeBot account:

```
http://YOUR_IP:3838/webhook
```

---

## 📝 How to Configure Allowed Contacts

In the web panel, you can:
- Add up to 10 authorized contacts
- Enable/Disable automatic responses per contact
- Delete contacts
- Globally enable/disable the bot

You can also manually edit the `allowed_contacts.txt` file:

```
5519112345678,John,true
5519987654321,Mary,false
```

---

## 💬 Reply Style

The bot replies just like you would on WhatsApp:

- **Direct and informal**
- No exaggerated greetings
- No long texts
- No robotic phrases
- Uses web search for news, sports, and weather updates

Example:

**Question:** "What's the score of the Corinthians game today?"  
**Reply:** "Corinthians won 2-1 just now"

---

## 📄 Conversation Log

The `messages.log` file stores everything in JSON format, line by line, containing:

- Message received
- Response generated
- Timestamp
- Sender name

Example:

```json
{
  "from": "5519112345678",
  "from_name": "John",
  "user_message": "Hey, is it working?",
  "assistant_response": "Yeah, all good",
  "timestamp": "2025-03-31 12:34:56"
}
```

---

## 🔒 Security

✅ Replies only to authorized contacts  
✅ You can pause responses via the web panel  
✅ Limit of 10 contacts to avoid misuse

---

## ⭐️ Next Steps (Suggestions)

- Add authentication to the web panel
- Add keyword filters for special responses
- Allow custom quick commands

---

## 🔧 TextMeBot API Configuration (your responsability, I am just a user sharing my use case, I am not afiliate with textmebot )

**TextMeBot** is a simple and low-cost API that allows you to send WhatsApp messages using your own number.  
This bot uses the **paid plan** to allow your number to send messages to any number.

### 1) Get your API Key

1. Access the official website: [https://textmebot.com/](https://textmebot.com/)
2. Click on **Request API Key** and follow the instructions.
3. You will receive an email with your API Key and instructions to link your WhatsApp number.

### 2) Link your WhatsApp number

1. Use the link provided in the email to connect your WhatsApp number to the API.
2. Follow the instructions to confirm your number is correctly associated.

### 3) Send Text Messages

To send a message, use the following URL format:

```
http://api.textmebot.com/send.php?recipient=[phone_number]&apikey=[your_apikey]&text=[message_to_send]
```

**Example:**

```
http://api.textmebot.com/send.php?recipient=+5511999999999&apikey=YOURAPIKEY&text=Hello%20world!
```

To receive the response in JSON format, add `&json=yes` to the URL.

⚠️ **Warning:** Sending messages to people who don't expect them may result in your WhatsApp number being blocked.  
Use the API responsibly and implement a minimum delay of 5 seconds between messages to reduce this risk.

---

### 4) Receive Incoming Messages (Webhook)

To receive incoming messages to your WhatsApp number, configure a webhook:

1. Access: [https://api.textmebot.com/webhook.php?apikey=YOURAPIKEY](https://api.textmebot.com/webhook.php?apikey=YOURAPIKEY)
2. Set the endpoint URL that will receive incoming messages in JSON format.

Incoming messages will follow this structure:

```json
{
  "type": "text",
  "from": "5511999999999",
  "from_name": "Sender Name",
  "to": "5511888888888",
  "file": null,
  "message": "Message received on WhatsApp"
}
```

For more details, visit: [TextMeBot Webhook Documentation](https://api.textmebot.com/web_receive.php)

---

### 5) Send Images and Documents

You can send files hosted on public services like Google Drive.  
Make sure the file is **publicly shared** and use the URL in the `file` or `document` parameter.

**Example to send an image:**

```
http://api.textmebot.com/send.php?recipient=+5511999999999&apikey=YOURAPIKEY&text=Here's%20the%20image&file=[FILE_URL]
```

**Note:** When using Google Drive, make sure the file is set to "Anyone with the link can view."

---

### 6) Send Messages from Google Sheets

You can integrate TextMeBot with Google Sheets to send messages to multiple recipients:

1. Create a sheet with phone numbers and messages.
2. Use **Google Apps Script** to automate message sending using the TextMeBot API.

For a detailed guide, visit: [https://textmebot.com/send-whatsapp-google-sheet-script/](https://textmebot.com/send-whatsapp-google-sheet-script/)

---

### 7) Important Recommendations

- **Avoid Spam:** Never send unsolicited messages to unknown contacts. It may lead to your WhatsApp number being blocked.
- **Message Delay:** Always include a minimum delay of 5 seconds between message sends.
- **Dedicated Number:** Use a dedicated number for the API, separate from your personal number.

For more information and best practices, visit:  
[https://textmebot.com/](https://textmebot.com/)
