# Camel Up Simulator

> A Python implementation of the *Camel Up* board game with a built-in AI advisor that tells you the optimal bet at any point in the race.

Built as part of the Jane Street AMP program. Models the full game — camel movement, stacking mechanics, leg betting, and race outcomes — and includes both enumerative and Monte Carlo probability engines to calculate expected value on every available bet.

---

## What It Does

- **Full game simulation** — camels move across a 16-tile track, stacking on each other according to the official rules; the camel on top of a stack carries the others
- **Leg betting** — players take betting tickets for which camel they think will lead the leg; payouts depend on correct 1st/2nd place predictions
- **AI advisor** — before each move, type `A` to get real-time win probabilities and expected values for every available bet ticket
- **Dual probability engines** — the AI runs both an enumerative analysis (exact, full state-space enumeration) and an experimental analysis (Monte Carlo simulation) and compares their outputs

---

## AI Advisor Output

```
  Enumerative    Experimental
   1st   2nd      1st   2nd
r  0.42  0.28     0.41  0.27
b  0.18  0.31     0.19  0.30
...

Available bets: (r) 5 EV:1.84  (b) 3 EV:0.62 ...
AI Advice: Bet on r with an expected value of 1.84
```

If no bet has EV > 1, the AI tells you to roll instead.

---

## Tech

- **Python** — no external dependencies beyond `colorama` for terminal colors
- **Enumerative analysis** — exhaustive enumeration of all possible dice sequences using `itertools.product`
- **Monte Carlo simulation** — random dice shaking over N trials to estimate probabilities
- **Expected value calculation** — EV = `P(1st) × ticket_value + P(2nd) × 1 + P(other) × -1`

---

## Getting Started

```bash
git clone https://github.com/coscoo/camel-up-simulator.git
cd camel-up-simulator
pip install colorama
python CamelUp.py
```

During a leg, each player picks:
- `B` — take a betting ticket for a camel
- `R` — roll the dice (move a random camel, earn 1 coin)
- `A` — ask the AI advisor for optimal strategy

---

## Project Structure

```
camel-up-simulator/
├── CamelUp.py        # Main game loop, player turns, leg payouts
├── Board.py          # Track state, camel positions, stacking logic
├── Pyramid.py        # Dice pyramid — tracks which dice remain
├── Player.py         # Player state — money, bets, moves
├── AI.py             # Probability engines and EV calculator
└── test_*.py         # Unit tests for board, pyramid, player, and AI
```

---

## License

MIT
