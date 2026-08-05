---
label: 6. Keep it Alive
order: 830
---

# Step 6: Keep it Alive (UptimeRobot)

Render's free tier spins down after inactivity. To keep your logger running 24/7:

1. Create a free account on [UptimeRobot](https://uptimerobot.com/).
2. Click **Add New Monitor**.
3. **Monitor Type**: HTTP(s)
4. **Friendly Name**: WhatsApp Logger
5. **URL (or IP)**: `https://your-app.onrender.com/ping` (make sure to include `/ping`)
6. **Monitoring Interval**: 5 minutes
7. Click **Create Monitor**.
