
Task 3

### 1. Dataset size

**Command used**: 'ls -lh clean_dialog.csv' and 'wc -l clean_dialog.csv'
**Result**: 4.6M and 36860 lines

### Data structure

**Command used**: 'head -n 1 clean_dialog.csv' and 'csvtool readable clean_dialog.csv | head -n 10'
**Result**: Fields are: title, writer, pony and dialog. The content inside Friendship is Magic, part 1         Lauren Faust                                                                                           Narrator and Twilight Sparkle                                       ...sun and moon...

### How many episodes

**Command used**: 'csvtool col 1 clean_dialog.csv | tail -n +2 | uniq | wc -l'
**Result**: 197 lines

### Exploration phase anomalies

**Command used**: 'grep -i ",," clean_dialog.csv | head -n 10', 'csvtool height clean_dialog.csv', csvtool width clean_dialog.csv
**Result**: Checked for NaN values, checked for the inconsistenct column counts across rows, 



Task 4

### How often each main character speaks:

**Command used**: 'csvtool col 3 clean_dialog.csv | grep -i -xc "Twilight Sparkle"', and with all the other names
**Result**: 4745, 2660, 2833, 3072, 2109

### %

**Command used**: 
TOTAL_LINE=$(csvtool col 3 clean_dialog.csv | tail -n +2 | wc -l)
TWILIGHT_COUNT=$(csvtool col 3 clean_dialog.csv | grep -xc "Twilight Sparkle")
RARITY_COUNT=$(csvtool col 3 clean_dialog.csv | grep -xc "Rarity")
PINKIE_COUNT=$(csvtool col 3 clean_dialog.csv | grep -xc "Pinkie Pie")
RAINBOW_COUNT=$(csvtool col 3 clean_dialog.csv | grep -xc "Rainbow Dash")
FLUTTERSHY_COUNT=$(csvtool col 3 clean_dialog.csv | grep -xc "Fluttershy")

awk -v count=$TWILIGHT_COUNT -v total=$TOTAL_LINES 'BEGIN { printf "Twilight Sparkle: %.2f%%\n", (count/total)*100 }'
awk -v count=$RARITY_COUNT -v total=$TOTAL_LINES 'BEGIN { printf "Rarity: %.2f%%\n", (count/total)*100 }'
awk -v count=$PINKIE_COUNT -v total=$TOTAL_LINES 'BEGIN { printf "Pinkie Pie: %.2f%%\n", (count/total)*100 }'
awk -v count=$RAINBOW_COUNT -v total=$TOTAL_LINES 'BEGIN { printf "Rainbow Dash: %.2f%%\n", (count/total)*100 }'
awk -v count=$FLUTTERSHY_COUNT -v total=$TOTAL_LINES 'BEGIN { printf "Fluttershy: %.2f%%\n", (count/total)*100 }'

**Result**: 
Twilight Sparkle: 12.87%
Rarity: 7.22%
Pinkie Pie: 7.69%
Rainbow Dash: 8.33%
Fluttershy: 5.72%