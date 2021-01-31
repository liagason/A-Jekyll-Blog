---
layout: post
title: Παραδείγματα χρήσιμου κώδικα για να ενσωματώσουμε στο πείραμά μας με το Astro Pi - Ομάδες Makerlab
---

### 1. Τυχαίοι αριθμοί
Ο παρακάτω κώδικας παράγει τυχαίους αριθμούς και αναλόγως με το αποτέλεσμα δείχνει και ένα διαφορετικό μήνυμα στην οθόνη το SenseHat. Θα τον τροποποιήσουμε και θα τον ενσωματώσουμε για να μη δείχνουμε συνέχεια το ίδιο μήνυμα.
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

### 2. Συντεταγμένες στον ΔΔΣ
Με τον παρακάτω κώδικα μπορούμε να βρούμε τις συντεταγμένες του ΔΔΣ και να τις δείξουμε στην οθόνη. Θα τον τροποποιήσουμε και θα τον ενσωματώσουμε για να καταγράφουμε τις συντεταγμένες σε ένα αρχείο CSV.
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
  
  if latitude < 0:
    print("Southern hemisphere")
  else:
    print("Northern hemisphere")
```

### 3. Μετράμε εύκολα τον χρόνο
Με τον παρακάτω κώδικα θα τρέξουμε το κομμάτι που είναι μέσα το while για 178 λεπτά. Ο κώδικα δείχνει το μήνυμα test και περιμένει 2 δευτερόλεπτα.
```python
import datetime
from time import sleep

start_time = datetime.datetime.now()
now_time = datetime.datetime.now()

while (now_time < start_time + datetime.timedelta(minutes = 178)):
    print("test....")
    sleep(2)
    now_time = datetime.datetime.now()
```

### 4. Ένταση μαγνητικού πεδίου
Για να υπολογίσουμε την ένταση του μαγνητικού πεδίου θα χρησιμοποιήσουμε τους [σχετικούς μαθηματικούς τύπους από την Βρετανική Γεωλογική Υπηρεσία](https://geomag.bgs.ac.uk/education/earthmag.html). Ο παρακάτω κώδικας υπολογίζει την ένταση του μαγνητικού πεδίου και την αποθηκεύει στη μεταβλητή f:
```python
from sense_hat import SenseHat
from time import sleep
from math import *

sense = SenseHat()

while True:
  compass = sense.get_compass_raw()

  # Get raw data (values are swapped because Sense HAT on ISS is in different position)
  # x: northerly intensity
  # y: easterly intensity
  #  z: vertical intensity
  
  x = float(compass['z'])
  y = float(compass['y'])
  z = float(compass['x'])

  # h: horizontal intensity
  # f: total intensity
  # d: declination
  # i: inclination
  
  h = sqrt(x ** 2 + y ** 2)
  f = sqrt(h ** 2 + z ** 2)
  d = degrees(atan(y / x))
  i = degrees(atan(z / h))

  print('z: ' + str(z))
  print('h: ' + str(h))
  print('f: ' + str(f))

  sleep(1)
```
