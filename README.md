- The "Replays" directory contains Starcraft replay files to extract raw data.
  
- The "Human_observational_data" directory contains x and y coordinates data of humans observing the game.
  Each directory contains 5 files, where each directory represents a person, and each file represents a different game.
  Directories 1 to 5, 6 to 10, and 11 to 15 contain observational data from the same games.

- To create the preprocessed masked data, run 1_make_input.py, 2_make_label.py, and 3_make_paired.py sequentially with replay file numbers.

Example usage
###
```
python 1_make_input.py --replays 36 212 438 522 1660 6254

python 2_make_label.py --replays 36 212 438 522 1660 6254  --method all_correct

python 3_make_paired.py --replays 36 212 438 522 1660 6254 --method all_correct --output channel

```

For training observer, we designed the following structure:

- Input data (9,128,128): For both player 1 and player 2, it includes information on workers, ground units, air units, buildings x 2, and terrain data.
- Label: The human observational data from 5 spectators.

If you want to extract the other characteristics of units from replays, you can use BWAPI to generate raw data by extracting unit information for every frame.

Visualization:
```
import numpy as np
import matplotlib.pyplot as plt

a = np.load("../result/36/1550.npy", allow_pickle=True)
print(a[0][0])
print(a[0].shape)
print(a[1].shape)
print(a[1])

fig, axes = plt.subplots(2, 5, figsize=(15, 6))

for i in range(4):
    ax = axes[0, i]
    ax.imshow(a[0][i], cmap='gray')
    ax.axis('off')  # 축 숨기기
    ax.set_title(f"a[0][{i}]")

for i in range(4, 9):
    ax = axes[1, i-4]
    ax.imshow(a[0][i], cmap='gray')
    ax.axis('off')  # 축 숨기기
    ax.set_title(f"a[0][{i}]")

axes[1, 4].axis('off')

plt.tight_layout()
plt.savefig("subplot_output_custom_9_images.png")
```
