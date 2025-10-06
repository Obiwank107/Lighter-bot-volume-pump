# Volume Trading Bots

Automated volume generation bots for decentralized perpetual exchanges with zero trading fees.

## Supported Exchanges

- **Paradex** - Starknet-based DEX with 250+ perpetual markets
- **Lighter** - High-performance perps DEX

## Features

- Zero trading fees (0% maker/taker)
- Fully configurable via `.env` file
- Ultra-tight spread market making strategy
- Real-time volume tracking from API
- Auto order refresh and placement
- Rate limit protection
- Support for multiple markets and leverage

## Project Structure

```
.
├── paradex/
│   ├── bot.py              # Paradex volume bot
│   └── .env.example        # Configuration template
├── lighter/
│   ├── bot.py              # Lighter volume bot
│   └── .env.example        # Configuration template
├── requirements.txt        # Python dependencies
└── README.md
```

## Installation

### Prerequisites

- Python 3.8+
- pip
- Virtual environment (recommended)

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/volume-trading-bots.git
cd volume-trading-bots

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Configuration

### Paradex Bot

1. **Get API Credentials:**
   - Visit [Paradex](https://app.paradex.trade)
   - Connect your wallet
   - Go to Settings → Key Management → Subkeys
   - Create new subkey and save the L2 Private Key

2. **Configure `.env`:**

```bash
cd paradex
cp .env.example .env
nano .env
```

Edit the following:

```bash
# Required
L2_PRIVATE_KEY=0x...              # Your Paradex L2 private key
L1_ADDRESS=0x...                  # Your Ethereum address
ENVIRONMENT=PROD                   # PROD or TESTNET

# Market Settings
MARKET=DOGE-USD-PERP              # Market to trade
LEVERAGE=10                        # Leverage multiplier
INVESTMENT_USDC=10                 # Investment amount

# Volume Targets
TARGET_VOLUME=100000               # Target volume ($100k)
MAX_LOSS=10                        # Maximum loss ($10)
TARGET_HOURS=24                    # Time to achieve target

# Strategy
SPREAD_BPS=2                       # Spread in basis points (0.02%)
ORDERS_PER_SIDE=10                 # Orders per side
ORDER_SIZE_PERCENT=0.5             # Order size (50% of capital)
REFRESH_INTERVAL=2.0               # Refresh interval (seconds)

# Rate Limits
DELAY_BETWEEN_ORDERS=0.05
DELAY_AFTER_CANCEL=0.3
MAX_ORDERS_TO_PLACE=10
```

### Lighter Bot

1. **Get API Credentials:**
   - Follow Lighter documentation to obtain API credentials
   - Save private key and account details

2. **Configure `.env`:**

```bash
cd lighter
cp .env.example .env
