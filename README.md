🏆 SportyBet Automated Value Betting Bot (with Kelly Criterion)

This project automates value betting and bankroll management on SportyBet using Python and Pyppeteer.
It automatically finds profitable bets, calculates the ideal stake using the Kelly Criterion, and places bets directly on the SportyBet website — all hands-free.

⚙️ Key Features

✅ Automatic Login to SportyBet using Pyppeteer

✅ Automatic Game Detection from SportyBet’s website or local data

✅ Value Betting System (identifies profitable opportunities)

✅ Kelly Criterion Bet Sizing (smart bankroll management)

✅ Automatic Bet Placement (enters stake and clicks “Place Bet”)

✅ Multi-Bet Capable — handles 100+ bets daily

✅ Human-like delays to reduce automation detection

✅ Bankroll Tracker (monitors growth over time)

🧠 How It Works (Step-by-Step)

Game Scraping
The bot fetches upcoming matches from SportyBet using Pyppeteer or preloaded data files.

Value Calculation
Each game’s expected value (EV) is calculated:

value = (probability * odds) - 1


Bets are only taken if the value > 0.

Kelly Criterion Calculation
The bot computes the stake to bet using the Kelly formula:

f* = (bp - q) / b


Where:

b = odds - 1

p = win probability

q = 1 - p

f* = fraction of bankroll to bet

Automatic Betting
Using Pyppeteer, the bot:

Logs into SportyBet

Finds the target match

Clicks the betting option

Inputs the stake (calculated using Kelly Criterion)

Clicks “Place Bet”

Bankroll Logging
After each bet, results are recorded in a CSV file or terminal output, showing bankroll performance.

🧮 Kelly Criterion Helper Function
def cal(odd, pba, amt):
    odd = float(odd)
    pba = float(pba)
    odd -= 1  # Subtract 1 to get net odds (b)
    proba = round(pba / 100, 4)  # Convert percentage to decimal
    loss = 1 - proba
    if odd == 0:
        return 0  # Avoid division by zero
    f = round((((odd * proba) - (loss)) / odd) * amt)
    return f

Example:

If the odds = 2.50, your estimated win probability = 55%, and bankroll = ₦1000
Then:

f = (((1.5 * 0.55) - 0.45) / 1.5) * 1000 = ₦100


So the bot automatically places a ₦100 bet.

🧠 Real-Life Explanation (Layman’s Terms)

Imagine you’re betting ₦1000.
The Kelly formula helps you avoid losing too much and maximize long-term growth.
If the bot finds a game that looks slightly profitable (say 60% chance to win at 2.00 odds), it’ll only risk a portion (say ₦200).
This protects your bankroll if you lose and compounds your profits if you win consistently.

📂 Example Project Structure
sportybet-bot/
│
├── bot.py                # Main entry point – runs the entire bot
├── sportybet.py          # Handles Pyppeteer browser automation
├── kelly.py              # Kelly Criterion calculation helper
├── value_bet.py          # Determines which games are value bets
├── config.py             # Contains user credentials, bankroll, and settings
├── data/
│   └── matches.csv       # Optional: Pre-fetched match data
├── logs/
│   └── results.csv       # Stores bankroll, results, and bet logs
├── requirements.txt      # List of Python dependencies
└── README.md             # Documentation (this file)

🧩 File Explanations
bot.py

Controls the full workflow

Loads bankroll and probability thresholds

Calls functions from other modules to calculate values, stakes, and execute bets

sportybet.py

Automates SportyBet using Pyppeteer

Handles:

Login

Scrolling and selecting odds

Inputting stake

Clicking “Place Bet” button

Error handling for slow network

kelly.py

Contains the Kelly Criterion function (cal())

Prevents division by zero and ensures safe stake sizing

value_bet.py

Compares predicted probabilities with SportyBet odds

Filters only bets with positive expected value (> 0)

config.py

Stores user preferences and credentials:

SPORTYBET_EMAIL = "your_email@example.com"
SPORTYBET_PASSWORD = "your_password"
BANKROLL = 1000
PROBABILITY_THRESHOLD = 60
BETTING_LIMIT = 10  # minimum Kelly output % to place a bet

data/matches.csv

Optional dataset containing:

Match,Odds,Probability
Arsenal vs Chelsea,2.10,58
Man City vs Liverpool,1.85,65
...

logs/results.csv

Records each bet’s:

Match,Odds,Probability,Stake,Result,Balance

🧮 Value Betting Example

Let’s say the bot finds these matches:

Match	Odds	Probability	EV	Bet?
Arsenal vs Chelsea	2.10	58%	0.218	✅ Yes
Barcelona vs Madrid	1.90	45%	-0.145	❌ No
Milan vs Inter	3.00	40%	0.200	✅ Yes

The bot automatically places bets only on Arsenal and Milan.

📈 Example Output Log
[INFO] Logging in to SportyBet...
[INFO] Found 2 value bets.
[BET] Arsenal vs Chelsea | Odds: 2.10 | WinProb: 58% | Kelly Stake: ₦130
[BET] Milan vs Inter | Odds: 3.00 | WinProb: 40% | Kelly Stake: ₦90
[INFO] Bets placed successfully.
[RESULT] Balance updated: ₦1120

🧠 Example Python Usage
from bot import start_bot

# Run bot with bankroll 1000 and 60% threshold
start_bot(bankroll=1000, probability_threshold=60)

🧰 Requirements

Install dependencies with:

pip install pyppeteer pandas numpy asyncio


Or from the included file:

pip install -r requirements.txt

🖥️ Run the Bot

To run in normal mode:

python bot.py


To run continuously (Linux/Termux/VPS):

nohup python bot.py &

🧠 Tips and Recommendations

Start testing with small bankrolls (₦1000).

Use await asyncio.sleep() to introduce random delays.

Review logs/results.csv weekly for performance.

Don’t exceed 10% of bankroll on a single bet.

Adjust the probability threshold (e.g., 60% → safer, 55% → more bets).

Can be modified to run on Android (Termux/Pydroid) or VPS.

🧩 Future Improvements

AI-powered match probability predictions

Telegram/Discord notifications for placed bets

Support for more bookmakers

Visual bankroll charts

Advanced error recovery and session handling

👨‍💻 Author

Ezee Kits (Peter)
🎓 Electrical & Electronics Engineer | Python Automation Developer
📺 YouTube: Ezee Kits

📧 Email: ezeekits@gmail.com

💬 Content: Python, Tech, DIY, Engineering, Automation

⚠️ Disclaimer

This bot is for educational and research purposes only.
Use responsibly and at your own risk.
The author is not responsible for financial losses or betting misuse.
