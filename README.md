# WhatsApp Reminder Action

This repository contains a GitHub Action that sends a daily WhatsApp message to the "Team D" group at a random time between 2 PM and 4 PM IST. The message follows the format "Day n of reminding Kairav I am taller", where `n` increments every day.

## How it works

1. **Scheduling**: A cron job triggers the action daily at 2:00 PM IST (8:30 AM UTC).
2. **Calculation**: The script calculates how many days have passed since the base date (September 17, 2026), making September 22, 2026 "Day 5".
3. **Random Delay**: To randomize the send time, the workflow sleeps for a random duration between 0 and 120 minutes before executing the final step.
4. **Sending**: It pulls your `mark816p/WhatsGo-forGithubActions` repository, reconstructs your WhatsApp session from secrets, and sends the message using Go.

## Setup Instructions

To get this working, you must add the following Secrets to this repository. Go to **Settings > Secrets and variables > Actions** and click **New repository secret**.

1. `WHATSAPP_SESSION_PART1`: Follow the instructions in your WhatsGo repo to generate and prune the `whatsapp_session.db`, then paste Part 1 here.
2. `WHATSAPP_SESSION_PART2`: Paste Part 2 of your generated session here.
3. `TEAM_D_JID`: The JID of the "Team D" group. (You can find it by logging into WhatsApp Web, pressing F12, and running `window.Store.Chat.models.filter(c => c.isGroup).map(c => ({name: c.name, id: c.id._serialized}))`).

## Manual Testing

You can trigger the workflow manually using `workflow_dispatch`. Go to the **Actions** tab in your repository, select **Daily WhatsApp Reminder**, and click **Run workflow**. By default, manual runs will skip the random sleep timer so you can verify it immediately.
