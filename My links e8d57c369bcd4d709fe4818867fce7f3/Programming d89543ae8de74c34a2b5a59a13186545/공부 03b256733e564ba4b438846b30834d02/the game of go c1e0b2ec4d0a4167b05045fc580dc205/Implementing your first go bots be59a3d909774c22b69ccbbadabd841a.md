# Implementing your first go bots

- implement a Go board by using Python
- Placing sequences of stones and simulating a game
- Encoding Go rules for this board to ensure legal moves are played
- Building a simple bot that can play aginst a copy of itself
- Playing a full game against your bot

### data models

- track the progress of a game you’re playing against a human opponent
- Track the progress of a game between two bots.this might seem to be exactly the same as the proceeding points but as it turns out a few subtle differences exist, most notably, naïve votes have a hard time recognizing when the game is over playing Two simple bots against each other is an important technique using later chapters so it’s worth calling out here.
- Compare prospective sequences from the same board position
- Import records and generate training data from them

### checking for availability

for example, after placing a black stone, you have to check all neighboring white stones to see whether black captured any stones that you have to remove.

1. You see whether there any neighbors have any liberties left
2. Check whether any of the neighbors’ neighbors have any liberties left
3. You examine the neighbors’ neighbors’s neighbors and so forth

viewing stones in isolation can lead to an increased computational complexity. instead, You keep track of groups of connected stones of the same color and their liberties at the same time. You call a group of connective stones of the same color, a string of stones or simply a string, and you can build this structure efficiently with the python set type.

### placing and capturing stones on a Go board

1. Marge, any adjacent strings of the same color
2. Reduce liberties of any adjacent strings of the opposite color
3. If any opposite color string now have zero liberties, remove them

also, if the newly created string has zero liberties, you reject the move.