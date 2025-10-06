Paradex Volume Bot
Automated volume generation bot for Paradex - a Starknet-based decentralized perpetual exchange with zero trading fees.

Features
Zero trading fees (0% maker/taker on Paradex)
Fully configurable via .env file
Ultra-tight spread market making strategy
Real-time volume tracking from API
Support for 250+ perpetual markets
Auto order refresh and placement
Rate limit protection (800 req/s)
Subkey support for enhanced security
Requirements
Python 3.8 or higher
pip package manager
Paradex account (testnet or mainnet)
Installation
1. Clone the repository
bash
git clone https://github.com/yourusername/paradex-volume-bot.git
cd paradex-volume-bot
2. Create virtual environment
bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
3. Install dependencies
bash
pip install -r requirements.txt
Configuration
Step 1: Get API Credentials
Option A: Using Subkey (Recommended)
Visit Paradex
Connect your wallet
Navigate to Settings → Key Management
Click Subkeys tab
Click + Add New Key
Enter a name (e.g., "Volume Bot")
Copy the L2 Private Key (shown only once!)
Benefits:

Cannot withdraw funds
Safer for automated trading
Can be revoked anytime
Option B: Using Main Private Key
Go to Wallet tab
Click Copy Private Key
Warning: This grants full account access including withdrawals. Not recommended for bots.

Step 2: Configure Environment Variables
bash
cp .env.example .env
nano .env  # or use your preferred editor
Edit the .env file:

bash
# ========================================
# Paradex API Configuration
# ========================================
L2_PRIVATE_KEY=0x...              # Your Paradex L2 private key
L1_ADDRESS=0x...                  # Your Ethereum wallet address
ENVIRONMENT=PROD                   # TESTNET or PROD

# ========================================
# Market & Trading Settings
# ========================================
MARKET=DOGE-USD-PERP              # Market to trade (see supported markets below)
LEVERAGE=10                        # Leverage multiplier (1-20x)
INVESTMENT_USDC=10                 # Investment amount in USDC

# ========================================
# Volume Target Settings
# ========================================
TARGET_VOLUME=100000               # Target volume in USD ($100k)
MAX_LOSS=10                        # Maximum acceptable loss in USD ($10)
TARGET_HOURS=24                    # Timeframe to achieve target (hours)

# ========================================
# Strategy Parameters
# ========================================
SPREAD_BPS=2                       # Spread in basis points (2 = 0.02%)
ORDERS_PER_SIDE=10                 # Number of orders per side (10 buy + 10 sell)
ORDER_SIZE_PERCENT=0.5             # Order size as % of capital (0.5 = 50%)
REFRESH_INTERVAL=2.0               # How often to refresh orders (seconds)

# ========================================
# Rate Limit Protection
# ========================================
DELAY_BETWEEN_ORDERS=0.05          # Delay between placing orders (seconds)
DELAY_AFTER_CANCEL=0.3             # Delay after canceling orders (seconds)
STATUS_INTERVAL=30                 # Status update interval (seconds)
MAX_ORDERS_TO_PLACE=10             # Max orders to place per side per cycle

# ========================================
# Advanced Settings
# ========================================
USE_POST_ONLY=true                 # Use POST_ONLY orders (true/false)
TRADING_FEE_PERCENT=0.0            # Trading fee percentage (0.0 for Paradex)
Supported Markets
Recommended Markets (with $10-50 investment)
DOGE-USD-PERP - Dogecoin (~$0.26, min size: 1 DOGE)
XRP-USD-PERP - Ripple (~$2.50, min size: 1 XRP)
ADA-USD-PERP - Cardano (~$0.80, min size: 1 ADA)
Popular Markets (require higher investment)
BTC-USD-PERP - Bitcoin (~$125k, min size: 0.001 BTC = $125)
ETH-USD-PERP - Ethereum (~$3.3k, min size: 0.01 ETH = $33)
SOL-USD-PERP - Solana (~$200, min size: 0.1 SOL = $20)
Note: Choose a market where minimum order size is less than your order capital.

Usage
Run the bot
bash
python3 bot.py
Expected Output
🚀 PARADEX VOLUME GENERATOR - FULLY CONFIGURABLE
===========================================================================
Environment: PROD
Market: DOGE-USD-PERP
Account: 0xb91b3DEc...3D96e5a1
Investment: $10.00 (Leverage: 10x)
Effective Capital: $100.00

🎯 TARGETS:
   Volume Goal: $100,000 in 24h
   Hourly Goal: $4,166
   Max Loss: $10.00

⚙️  STRATEGY CONFIG:
   Spread: 0.020% (2 bps)
   Orders: 20 total (10 each side)
   Order Size: 50.0% of capital
   Refresh: Every 2.0s

🔄 Starting order refresh (2.0s cycles)...

📊 Cycle 1 - Orderbook:
   Best Bid: $0.26005
   Best Ask: $0.26024
   Mid Price: $0.26015
   Spread: 0.073%
   Order size: 192.000000 DOGE
   Rounded size: 192
   Placing 10 buy + 10 sell orders...
   ✅ BUY @ $0.26004
   ✅ BUY @ $0.26003
   ✅ SELL @ $0.26026
   ✅ SELL @ $0.26027
   Summary: 10 buy + 10 sell orders placed

===========================================================================
⏱️  0:00:31 elapsed | 23.9h left | Price: $0.26
📊 Orders: 10 BUY + 10 SELL | Spread: 0.073%

💰 VOLUME (REAL from API):
   Current: $156 / $100,000 (0.2%)
   Trades: 6
   Current Rate: $300/hour

💸 COSTS:
   🎉 ZERO FEES - Free trading!
   Loss (spread): $0.00
===========================================================================
Stop the bot
Press Ctrl+C to stop gracefully.

Strategy Presets
Conservative (Safe, 24h runtime)
bash
SPREAD_BPS=5
ORDERS_PER_SIDE=8
ORDER_SIZE_PERCENT=0.2
REFRESH_INTERVAL=3.0
DELAY_BETWEEN_ORDERS=0.1
Balanced (Recommended)
bash
SPREAD_BPS=2
ORDERS_PER_SIDE=10
ORDER_SIZE_PERCENT=0.5
REFRESH_INTERVAL=2.0
DELAY_BETWEEN_ORDERS=0.05
Aggressive (High volume, faster loss)
bash
SPREAD_BPS=1
ORDERS_PER_SIDE=15
ORDER_SIZE_PERCENT=0.7
REFRESH_INTERVAL=1.0
DELAY_BETWEEN_ORDERS=0.03
Tips for Maximizing Volume
Choose the right market
Use low-priced assets (DOGE, XRP, ADA)
Ensure minimum order size < your order capital
Optimize spread
Wider spread = more fills but slower
Tighter spread = fewer fills but better price
Adjust order size
Larger orders = more volume per fill
Smaller orders = more frequent fills
Increase investment
More capital = larger orders = more volume
Use high liquidity markets
BTC, ETH, SOL have best liquidity
But require more capital
Troubleshooting
Orders not filling
Causes:

Spread too tight (orders sit in orderbook)
POST_ONLY mode (won't cross spread)
Low market liquidity
Solutions:

Increase SPREAD_BPS to 3-5
Change to USE_POST_ONLY=false (but you'll pay fees)
Try a more liquid market
"Size must be a multiple of 1" error
Cause: Your order size rounds to 0 or doesn't meet minimum

Solutions:

Increase INVESTMENT_USDC
Increase ORDER_SIZE_PERCENT
Use a lower-priced market (DOGE instead of BTC)
"Price must be a multiple of X" error
Cause: Price precision doesn't match market tick size

Solution: This should be fixed automatically. If persists, report as bug.

Rate limit errors
Cause: Too many API requests

Solutions:

Increase REFRESH_INTERVAL to 3.0
Increase DELAY_BETWEEN_ORDERS to 0.1
Reduce MAX_ORDERS_TO_PLACE to 8
Insufficient balance
Cause: Not enough USDC in account

Solution: Deposit USDC to your Paradex account

Safety & Risk Management
Important Warnings
You can lose your entire investment
This bot is for volume generation, not profit
Test on testnet first before using real funds
Never share your private keys
Use subkeys instead of main private key
Risk Mitigation
Start small - Test with $10-20 first
Use testnet - Practice on testnet.paradex.trade
Monitor closely - Watch the first hour carefully
Set stop-loss - Use MAX_LOSS parameter
Use subkeys - Protect your main account
Rate Limits
Paradex allows:

800 requests/second for order endpoints
17,250 requests/minute for order endpoints
1,500 requests/minute for GET endpoints
The bot stays well within these limits with default settings.

Advanced Configuration
Multi-market setup
Run multiple bots on different markets:

bash
# Terminal 1
MARKET=DOGE-USD-PERP python3 bot.py

# Terminal 2
MARKET=XRP-USD-PERP python3 bot.py
Custom logging
Redirect output to file:

bash
python3 bot.py > bot.log 2>&1 &
tail -f bot.log
Contributing
Contributions are welcome! Please:

Fork the repository
Create a feature branch
Make your changes
Submit a pull request
Support
Issues: GitHub Issues
Paradex Docs: docs.paradex.trade
Paradex Discord: discord.gg/paradex
License
MIT License - see LICENSE file for details

Disclaimer
This software is provided "as is" without warranty of any kind. Trading cryptocurrencies involves substantial risk of loss. Use at your own risk. The authors are not responsible for any financial losses incurred through the use of this bot.

This bot is designed for volume generation and market making, not profit generation. You will likely lose money using this bot. Only use funds you can afford to lose.

Built for Paradex - Zero-fee perpetual trading on Starknet

