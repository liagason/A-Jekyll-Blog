---
layout: post
title: Χρήσιμος κώδικας για το πείραμά μας με το astro-pi
---

### Τυχαίοι αριθμοί
Ο παρακάτω κώδικα παράγει τυχαίους αριθμούς και αναλόγως με το αποτέλεσμα δείχνει και ένα διαφορετικό μήνυμα στην οθόνη το SenseHat:
```python
import random
temp = random.randint(1,4)
if temp == 1:
    sense.show_message("=> Doing stuff.")
if temp == 2:
    sense.show_message("=> Still working.")
if temp == 3:
    sense.show_message("=> Everything's OK.")
```

### Συντεταγμένες στον ΔΔΣ
Με τον παρακάτω κώδικα μπορούμε να βρούμε τις συντεταγμένες του ΔΔΣ και να τις δείξουμε στην οθόνη:
```python
from ephem import readtle, degree
name = "ISS (ZARYA)"
line1 = "1 25544U 98067A   21030.23684081  .00003078  00000-0  64152-4 0  9998"
line2 = "2 25544  51.6460 305.0424 0002363 316.2883 179.5775 15.48926800267219"
iss = readtle(name, line1, line2)

def get_latlon():
    iss.compute()
    return (iss.sublat / degree, iss.sublong / degree)
    
while True:
  latitude, longitude = get_latlon()
  print(latitude, longitude)
```
