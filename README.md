# K-Wallet

## Table of Contents

1. [First-Time Tip Recipient Guide](#first-time-tip-recipient-guide)
2. [Creating a Wallet to Tip Others](#creating-a-wallet-to-tip-others)
3. [K-Wallet User Guide](#k-wallet-user-guide)
4. [Discord's Slash Command Interface](#discord-slash-command-interface)
5. [Developer Guide](#developer-guide)
   - [Run](#run)
   - [Settings](#settings)

## First-Time Tip Recipient Guide

When you receive your first tip, here's what you should do:

### 1. Remember Your Password

- Your password encrypts your mnemonic in storage
- Without the password, you cannot access your funds
- There's no recovery option for forgotten passwords
- Choose a strong, memorable password before creating your wallet

### 2. Create and Secure Your Wallet

Run `/kwallet unlock <password>` to create your wallet. You'll receive your 12-word mnemonic phrase via DM - save it
immediately as it's the only way to recover your wallet.

### 3. Back Up Your Recovery Phrase

- Store your mnemonic phrase offline and securely
- Never share it with anyone
- You can view it later with `/kwallet info show-secret:true` (requires unlocking)

### 4. Find Your Receiving Address

Your Kaspa receiving address is available in two ways:

- **Your address**: Run `/kwallet info` to see your public address with an explorer link
- **Others can find it**: Anyone can run `/kwallet address_of @yourname` to get your receiving address

### 5. Receiving External KAS

Yes, you can send KAS from any external wallet to your k-wallet address. The address works like any standard Kaspa
address - just copy it from `/kwallet info` and use it as the destination in any Kaspa wallet or exchange.

## Creating a Wallet to Tip Others

If you want to start tipping others without having received a tip first:

### 1. Remember Your Password

- Your password encrypts your mnemonic in storage
- Without the password, you cannot access your funds
- There's no recovery option for forgotten passwords
- Choose a strong, memorable password before creating your wallet

### 2. Create and Secure Your Wallet

Run `/kwallet unlock <password>` to create a new wallet. You'll receive your 12-word mnemonic phrase via DM - save it immediately as it's the only way to recover your wallet.

### 3. Back Up Your Recovery Phrase

- Store your mnemonic phrase offline and securely
- Never share it with anyone
- You can view it later with `/kwallet info show-secret:true` (requires unlocking)

### 4. Fund Your Wallet

- Send KAS from any exchange or external wallet to your address
- Your address works like any standard Kaspa address
- Use the explorer link from `/kwallet info` to verify deposits

### 5. Start Tipping

Once funded, you can tip others:
> `/kwallet tip @user 10 "Here's a tip!"`

Your wallet must be unlocked to send tips.

## Notes

- Your wallet automatically receives tips sent to you, even when locked
- Funds sent to users without wallets are held in custodial storage until they create a wallet
- The bot administrators cannot access your funds or recovery phrase
- Minimum 1 KAS per recipient for multiple tips

# K-Wallet User Guide

A comprehensive guide to using the K-Wallet Discord bot for Kaspa (KAS) tipping and wallet management.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Core Commands](#core-commands)
3. [Wallet Management](#wallet-management)
4. [Advanced Features](#advanced-features)
5. [How Tipping Works](#how-tipping-works)
6. [Security Best Practices](#security-best-practices)
7. [Troubleshooting](#troubleshooting)

## Getting Started

### Creating Your Wallet

To start using K-Wallet, create a personal wallet:

> `/kwallet unlock <password>`

- Creates a new wallet with a unique Kaspa address
- Your 12-word mnemonic phrase is sent via DM
- **Important**: Save your mnemonic phrase securely - it's the only way to recover your wallet

### Checking Your Wallet

View wallet information:

> `/kwallet info`

Shows balance, address, and wallet status. Use `show-secret:true` to view your mnemonic phrase.

## Core Commands

### 💸 Tip - Send KAS to Discord Users

Primary command for sending KAS:

> `/kwallet tip <who> <amount> [message] [options]`

**Parameters:**

- `who`: Discord mention (@user, @role, @everyone)
- `amount`: Amount of KAS to send
- `message`: Optional message to display with the tip

**Options:**

- `allow-hold`: Hold funds for users without wallets (default: true for single users, false for roles)
- `inclusive-fee`: Deduct fees from the amount (default: false)

**Examples:**
> `/kwallet tip @friend 10 "Thanks for helping!"`
>
> `/kwallet tip @role 5 allow-hold:false`
>
> `/kwallet tip @user 100 inclusive-fee:true`

**Short form:** `/ktip` also works

### 💰 Withdraw - Send KAS to External Addresses

Withdraw KAS to any Kaspa address:

> `/kwallet withdraw <amount> <address>`

Features:

- Autocomplete shows balance and saved withdraw address
- Set default withdraw address in settings

## Wallet Management

### 🔓 Unlock - Access Your Wallet

Unlock wallet for transactions:

> `/kwallet unlock <password>`

- Keeps wallet unlocked for 10 minutes by default
- Auto-locks after inactivity for security

### 🔒 Lock - Secure Your Wallet

Manually lock wallet:

> `/kwallet lock`

Immediately removes keys from memory.

### 🔧 Settings - Configure Your Wallet

Manage wallet preferences:

> `/kwallet settings [options]`

**Options:**

- `secret`: Change wallet password
- `withdraw-address`: Set default withdraw address
- `unlock-timeout`: Adjust auto-lock duration
- `auto-withdraw`: Forward all tips to withdraw address (if enabled)

### 🔄 Recover - Restore from Mnemonic

Restore wallet using 12-word phrase:

> `/kwallet recover <mnemonic> <new-password>`

- Must delete existing wallet first
- Mnemonic must be exactly 12 words

## Advanced Features

### 📊 Info - Detailed Wallet Information

View comprehensive wallet details:

> `/kwallet info [show-secret]`

**Displays:**

- Wallet status (locked/unlocked)
- Available and pending balance
- UTXO count
- Public and withdraw addresses
- Mnemonic phrase (if show-secret:true)

### 🔄 Compound - Merge UTXOs

Consolidate multiple UTXOs to reduce future fees:

> `/kwallet compound [max]`

- `max`: Maximum UTXOs to compound (default: 500)
- Useful after receiving many small tips

### ✂️ Split - Create Multiple UTXOs

Split balance for parallel spending:

> `/kwallet split <amount> <count>`

- `amount`: Total KAS to split
- `count`: Number of outputs to create (minimum: 2)

### 👤 Address_of - Look Up User Address

Find another user's public address:

> `/kwallet address_of <user>`

## How Tipping Works

### Custodial System

For users without wallets:

- Tips are held in custodial storage
- Funds are automatically transferred when they create a wallet
- No loss of tips for new users

### Transaction Monitoring

- Tips are monitored until finalized (100+ block confirmations)
- Status indicators: ⏳ pending, ☑️ finalized
- Real-time updates in Discord

### Fee Handling

- Default: Fees paid separately from tip amount
- Use `inclusive-fee:true` to deduct fees from the tip
- Not available for multiple recipients

## Security Best Practices

### 🔐 Protect Your Mnemonic

- Mnemonic phrase is the master key to your wallet
- Store it offline and securely
- Never share it with anyone
- View it with `/kwallet info show-secret:true`

### 🛡️ Wallet Security

- Use a strong, unique password
- Lock wallet when not in use
- Be cautious with auto-withdraw feature
- Verify addresses before withdrawing

### 🚨 Important Notes

- Bot administrators cannot access your funds
- Your wallet is controlled only by your mnemonic
- Tips are public messages on Discord
- Transaction details are on the blockchain

## Troubleshooting

### Common Issues

**"Wallet is locked"**

- Run `/kwallet unlock <password>`
- Check if password is correct

**"You do not have a wallet"**

- Create one with `/kwallet unlock <password>`
- Or recover with `/kwallet recover`

**"Failed submitting transaction"**

- Check balance (amount + fees)
- Verify recipient address
- Try again with `inclusive-fee:true`

**"Insufficient balance"**

- Need amount + network fees in wallet
- Use `inclusive-fee:true` to tip entire balance

### Getting Help

- Use Discord's built-in command help by typing `/kwallet`
- Check parameter descriptions while typing commands
- Error messages provide specific guidance

## Command Summary

| Command | Purpose | Wallet Required | Unlocked Required |  
|---------|---------|-----------------|-------------------|  
| `tip` | Send KAS to users | Yes | Yes |  
| `withdraw` | Send to external address | Yes | Yes |  
| `unlock` | Create/unlock wallet | No | N/A |  
| `lock` | Lock wallet | Yes | No |  
| `info` | View wallet info | Yes | No (degraded) |  
| `settings` | Configure wallet | Yes | Varies |  
| `compound` | Merge UTXOs | Yes | Yes |  
| `split` | Create UTXOs | Yes | Yes |
| `recover` | Restore wallet | No | N/A |  
| `address_of` | Look up address | No | No |  

## Notes

- Commands work in any Discord server where the bot is present
- Some commands may take up to an hour to appear in new servers
- Bot may be disabled during maintenance
- Minimum 1 KAS per recipient for multiple tips
- Bots cannot receive tips

## Discord Slash Command Interface

When you type `/kwallet` in any Discord server where the bot is present, Discord displays a built-in help interface that
shows all available commands with their descriptions.

### How It Works

The bot registers its command structure with Discord's API during deployment:

The main command is created with:

- Name: "kwallet"
- Description: "Kaspa tipper and wallet manager"

Each subcommand is added with its description:

- tip - "Sends some KAS"
- withdraw - "Withdraw KAS"
- unlock - "Unlocks the wallet, enabling spending"
- info - "Shows public address and balance of current user"
- And all other commands

### Discord's Native UI Features

When you type `/kwallet`, Discord automatically shows:

- Command list: All available subcommands in a dropdown menu
- Descriptions: Each command's description appears in the UI
- Parameter hints: As you select a command, required and optional parameters appear
- Autocomplete: Some fields show suggestions (like your balance for amount fields)

### Short Commands

Commands with `short: true` also work as standalone commands:

- `/ktip` - Same as `/kwallet tip`
- These also show their own help when typed

### Notes

- This help system is provided by Discord, not the bot
- Command descriptions come directly from the code in each command file
- The interface updates automatically when commands are redeployed
- Force refresh Discord (Ctrl+R) if commands don't appear after deployment

This Discord-native interface makes it easy to discover and learn all available commands without needing separate
documentation.

# Developer Guide

## Run

### Docker

Build the docker image

```shell 
docker build . --tag k-wallet
```

Create a `config.json` file as described in [#Settings], and run the docker
```shell
docker run -v ./config.json:/app/config.json -e CONFIG_PATH=/app/config.json k-wallet
```

In case of using firestore, map the firestore key file to the desired location configured in `config.json`:
```
docker run -v keyfile.json:/app/firestore.json -v ./config.json:/app/config.json -e CONFIG_PATH=/app/config.json k-wallet
```

### Locally

Clone the `multipe_targets` branch of [tmrlvi/kaspa-wallet](https://github.com/tmrlvi/kaspa-wallet/tree/multiple_targets)
into the parent directory of this repository. Then run,

```shell
npm install
npm run start
```

## Settings

The settings are in a json file, e.g. `config.json`. The path is determined by the environment variable `CONFIG_PATH`.
The file is of the following structure:
```json
{
    "kaspad_address": <kaspad address>,
    "explorer_tx": <explorer tx address>,
    "explorer_addr": <explorer wallet link>,
    "network": <"kaspa" | "kaspatest" | "kaspadev" - determines the key derivation and default port>
    "custodial": <mnemonics for the custodial wallet>,

    "storeType": <"firestore" or "keyv" (direct control)>,
    "storeConfig": {
        "projectId": <firestore project id>,
        "databaseId": <database id>,
	    "keyFilename": <path to service account key file>
    },
    "userStore": <connection string or collection name (for firestore) of the user store>,
    "custodyStore": <connection string or collection name (for firestore) or the custody store>,
  
    "offline": <use "no", "yes" or "admin" enables more debug logging directly in discord>,
    "admin": <user ids which are allowed to see the direct logging if opted to admin>,
    "discord_token": <bot token>,

    "enableAutoForward": false,
    "enableFaucet": false,
    "minAllowedMulticast": 1.0
}
```
