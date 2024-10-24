- The "Replays" directory contains Starcraft replay files to extract raw data.
  
- The "Human_observational_data" directory contains x and y coordinates data of humans observing the game.
  Each directory contains 5 files, where each directory represents a person, and each file represents a different game.
  Directories 1 to 5, 6 to 10, and 11 to 15 contain observational data from the same games.



Example usage
###
```
python 1_make_input.py --replays 36 212 438 522 1660 6254 #write the numbers of replays you want to extract data

python 2_make_label.py --replays 36 212 438 522 1660 6254  --method all_correct

python 3_make_paired.py --replays 36 212 438 522 1660 6254 --method all_correct --output channel
