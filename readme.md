# DUSK Monitoring and Notification Script

This Python script automates the monitoring, and management of **DUSK blockchain staking**, balances, compounding and epochs. It efficiently handles claiming and restaking rewards, sends notifications via multiple services, and optionally (still in development) updates the TMUX status bar with real-time information.

---


Dusk wallet for Tips: `eox326D2m1ohpBUFVgiF885yV7aN4sg4caA6UkAg7UUhB6JWystDE7t2bdvstBHKTGYrF1oEhYZEd4Bqh4Uhoer`

## Features

### 🚀 Automated Actions

- **Staking Management**:
  - Monitors staking rewards, reclaimable slashed stakes, and eligible stakes.
  - Automatically claims and stakes rewards when profitable.
  - Unstakes and restakes reclaimable slashed amounts when optimal.

- **Notification Support**:
  - Sends alerts via:
    - **Discord**
    - **Pushbullet**
    - **Telegram**
    - **Pushover**
  - Configurable per service using environment variables or script settings.

- **Efficient Execution**:
  - Calculates sleep times based on epochs to minimize unnecessary processing.
  - Prevents redundant or runaway actions.

- **TMUX Integration (Optional)**:
  - Updates the TMUX status bar with real-time staking and balance data.

---

## Installation

### Prerequisites

- **Python**: Version 3.7 or higher

---

### Steps

1. **Clone the Repository**:

    ```bash
    git clone https://github.com/wolfrage76/dusk-compounder.git
    cd <your-repo-name>
    ```

2. **Install Dependencies**: Install the required Python libraries:

    ```bash
    pip install requests pyyaml
    ```

3. **Set Wallet Password**: Export your wallet password as an environment variable. For example:

    ```bash
    export MY_SUDO_PASSWORD="your_wallet_password"
    ```

4. **Configure Notifications**: Open the script and edit the config dictionary to enable and set up the notification services you want to use:

    ```python
    notification_config = {
        "discord_webhook": None, # Replace Nonewith your webhook URL: "https://discord.com/api/webhooks/..." in quotes
        "pushbullet_token": None,
        "telegram_bot_token": None,
        "telegram_chat_id": None
        "pushover_user_key": None,
        "pushover_app_token": None
    }
    ```

5. **Run the Script**: Start the monitoring script:

    ```bash
    python dusk_monitor.py
    ```

---

## Notification Configuration

To enable notifications for specific services, provide the required credentials in the `config` dictionary. Notifications will only be sent for properly configured services. Setting a value to `None` disables that notification.

| **Service**  | **Required Configuration Fields**                     |
|--------------|-------------------------------------------------------|
| Discord      | `discord_webhook`                                     |
| Pushbullet   | `pushbullet_token`                                    |
| Telegram     | `telegram_bot_token`, `telegram_chat_id`              |
| Pushover     | `pushover_user_key`, `pushover_app_token`             |

---

## Notes

- **Epoch Calculation**:  
  The script calculates sleep times based on the remaining blocks until the next epoch, ensuring efficient execution.

- **Minimum Rewards**:  
  The script only claims and stakes rewards if they exceed a configurable threshold (default: `1 DUSK`).

- **TMUX Integration**:  
  Displays real-time blockchain and balance data directly in the TMUX status bar if enabled.
