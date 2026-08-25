---
icon: question
order: 100
---

# Frequently Asked Questions

## General

**Is this really free?**  
Yes. Render, Firebase, and UptimeRobot all have generous free tiers that are sufficient for personal use. You will typically never pay anything.

**Is my data safe?**  
Absolutely. The entire system is self-hosted. You own the database (Firebase) and the server (Render). The developers of this tool have zero access to your data.

**Does the developer see my chats?**  
No. The code connects directly from your Render server to your Firebase database using your personal API keys. There is no middleman server.

**Is this legal?**  
The tool uses standard WhatsApp Web protocols to function as a linked device. It is intended for personal archiving of your own conversations.

## Features & Limitations

**Does it save photos/videos?**  
No. To keep the project free (Firebase offers limited storage), the logger only saves text content. Media files would fill up your free tier storage very quickly.

**Does it save View Once messages?**  
No. WhatsApp does not send the content of "View Once" media to linked devices/web clients, so the logger cannot see them.

**Does it save WhatsApp Status?**  
No, it cannot save WhatsApp statuses at this time. If you would like to add this feature to this project, please submit a pull request by uploading the updated code to [Github](https://github.com/notamitgamer/WhatsApp-Logger-Self-Hosted-/pulls).

**Can I reply from the dashboard?**  
No. This tool is designed strictly as a read-only archive to ensure maximum safety and simplicity.

**Does it work with Group Chats?**  
Yes! It automatically archives messages from any group you are part of, including messages sent by other participants.

**Can I export my chats?**  
Yes. Inside any chat on the dashboard, open the menu (three dots) and select "Download" to get a `.txt` file of the conversation.

## Technical Setup

**What is Render?**  
Render is a cloud hosting platform. It provides the computer (server) that runs your logger 24/7 so your phone doesn't have to.

**What is Firebase?**  
Firebase is Google's database service. While Render processes the messages, Firebase acts as the permanent hard drive where logs are stored.

**Do I need my phone on 24/7?**  
No. Once you scan the QR code, the logger works independently via WhatsApp's Multi-Device feature. Your phone does not need to stay online continuously after linking.

**What if Render sleeps?**  
If the server sleeps, you will miss messages sent during that time. This is why setting up UptimeRobot (Step 5) is critical—it keeps the server awake.

**How do I update the logger?**  
In your Render dashboard, go to your service and click "Manual Deploy" -> "Deploy latest commit" to pull the newest code from GitHub.

**Can I host this on a Raspberry Pi?**  
Yes. The backend is standard Node.js. You can clone the repo and run `npm install && npm start`. You still need Firebase for the database.

**How much storage do I have?**  
The Firebase Free Tier (Spark Plan) gives you 1 GiB of storage. Since we only store text, this is enough for millions of messages.

## Troubleshooting

**Why is the QR code not loading?**  
Your Render server might be starting up or deploying. Wait 30 seconds and refresh the page. Check Render logs if the issue persists.

**Why does it say "No chats found"?**  
The logger starts empty. It only records messages that arrive *after* you have linked it. Send a message to your phone to see it appear.

**I forgot my App PIN/Password**  
On the lock screen, click "Forgot PIN". You can reset your local security using the server credentials (`AUTH_USER` and `AUTH_PASS`) you set in Render.
