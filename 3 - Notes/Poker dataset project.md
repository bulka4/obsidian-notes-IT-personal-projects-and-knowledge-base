Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project, we create a dataset about poker games.

We use a text file describing a game:
```
Seat 1: MrWhite (10000 in chips)
Seat 2: Gogo (10000 in chips)
...
Dealt to MrWhite [3c 9s]
Dealt to Gogo [6d 5s]
...
Budd: folds
Eddie: folds
Bill: raises 125 to 225
```

and based on it we create a table with columns:
- `round`
- `player`
- `cards_hand`
- `bets_before_floop`
- `floop_cards`
- `floop_hands`
- `bets_floop`
- `_turn_cards`
- `turn_hands`
- `bets_turn`
- `ruver_cards`
- `river_hands`
- `bets_river`
- `win_or_loos`
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/poker_dataset_preparation).