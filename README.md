<img width="1230" alt="image" src="https://github.com/sezaras85/Sentient-ai/blob/main/sentient%20resim.png" />


# Sentient AI Dobby Discord Bot s

This is a simple Discord chatbot using Fireworks AI's **Dobby-70B** model.

## Features

- Uses Sentient's Dobby model (`dobby-unhinged-llama-3-3-70b-new`)
- Friendly, filtered replies
- Basic profanity filter
- Async Discord client

 


1. Get an API Key from Firework AI
   
 ```bash
1. Go to the [Firework AI](https://firework.ai) website.
2. Log in to your account or create a new account.
3. Go to the **API Keys** section and create a new API key.
4. Save the generated API key in a safe place.

   ```

2. Creating a Discord Bot (Developer Portal)

```bash
Go to Discord Developer Portal.
https://discord.com/developers

“New Application” → name your bot.

From the left menu “Bot” → “Add Bot” → Yes, do it!

You will see the Bot Token here → copy it (keep it private).
*Don't forget to save your Discor_Bot_Token

```

3. Install dependencieses:
  
```bash
  pip install discord.py requests

```

4. Generate Python Code
   
```bash
   nano bot.py
```
5. enter your own keys FIREWORKS_API_KEY = "YOUR_FIREWORKS_API_KEY" and DISCORD_BOT_TOKEN = "YOUR_DISCORD_BOT_TOKEN"

write code save it with ctrl+O.

```bash
import discord
import requests
import re

# Fireworks AI API credentials
FIREWORKS_API_KEY = "YOUR_FIREWORKS_API_KEY"
FIREWORKS_API_URL = "https://api.fireworks.ai/inference/v1/completions"

# Discord bot token
DISCORD_BOT_TOKEN = "YOUR_DISCORD_BOT_TOKEN"

# Discord client permissions
intents = discord.Intents.default()
intents.message_content = True  # Needed to read user messages

# Initialize bot
client = discord.Client(intents=intents)

# List of profane and toxic words (can be expanded)
BAD_WORDS = [
    "fuck", "shit", "bitch", "asshole", "damn", "dick", "piss", "fucking", "motherfucker",
    "cunt", "fag", "retard", "nigger", "dyke", "slut", "whore", "bollocks", "arsehole"
]

def clean_toxic_language(text):
    """Censors profane and toxic language, reduces repeated characters, and softens excessive shouting."""
    
    # Censor bad words
    for word in BAD_WORDS:
        pattern = re.compile(rf"\b{word}\b", re.IGNORECASE)
        text = pattern.sub("[censored]", text)

    # Reduce excessively repeated characters (e.g. aaaa -> aaa)
    text = re.sub(r'(.)\1{3,}', r'\1\1\1', text)

    # Soften ALL-CAPS words (yelling)
    def fix_caps(m):
        word = m.group()
        return word.capitalize() if len(word) > 2 else word
    text = re.sub(r'\b[A-Z]{3,}\b', fix_caps, text)

    # Replace specific aggressive phrases
    aggressive_replacements = {
        r"fuck off": "[censored]",
        r"shut up": "[please be kind]",
        r"bitch": "[censored]",
        r"dogshit": "bad",
        r"idiot": "a bit careless",
    }
    for pattern, replacement in aggressive_replacements.items():
        text = re.sub(pattern, replacement, text, flags=re.IGNORECASE)

    return text.strip()

def generate_reply(message_text):
    """Generates a reply using Fireworks AI"""
    headers = {
        "Authorization": f"Bearer {FIREWORKS_API_KEY}",
        "Content-Type": "application/json"
    }

    prompt = f'Reply to this Discord message in a helpful, friendly tone: "{message_text}"'

    payload = {
        "model": "accounts/sentientfoundation/models/dobby-unhinged-llama-3-3-70b-new",
        "prompt": prompt,
        "max_tokens": 240,
        "temperature": 0.7,
        "top_p": 0.9
    }

    try:
        response = requests.post(FIREWORKS_API_URL, json=payload, headers=headers)
        response.raise_for_status()
        reply = response.json().get("choices", [{}])[0].get("text", "").strip()
        cleaned_reply = clean_toxic_language(reply)
        return cleaned_reply if cleaned_reply else "Sorry, I didn't understand that."
    except Exception as e:
        print(f"❌ Fireworks API Error: {e}")
        return "Something went wrong 😞"

@client.event
async def on_ready():
    print(f"✅ Logged in as: {client.user}")

@client.event
async def on_message(message):
    if message.author == client.user:
        return  # Don't respond to own messages

    if message.content.startswith("!"):
        return  # Skip bot commands

    reply = generate_reply(message.content)
    await message.channel.send(reply)

# Run the bot
client.run(DISCORD_BOT_TOKEN)

```
6. Run the bot

```bash
 python3 bot.py

```


8. Discord enable required permissions
   
```bash
Go to discord developer page
 https://discord.com/developers/applications

Activate the following 3 settings in the “Privileged Gateway Intents” section on the bottom left:

-Message Content Intent (can read user messages)

-Presence Intent (optional, for online status)

-Server Members Intent (optional, if member information is required)
```

8.Invite Bot to Your Server (OAuth2)

```bash
Go to the “OAuth2 → URL Generator” tab on the left menu.

Select the following boxes:

Scopes: ✅ bot

Bot Permissions:

✅ Send Messagess

✅ Read Message History

✅ View Channels

✅ Read Messages/View Channels

✅ Mention Everyone (if you want)

Copy the generated URL at the bottom of the page and paste it into your browser.

Invite the bot to your server.

```



 
