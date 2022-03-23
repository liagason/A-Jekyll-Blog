---
layout: post
title: Εντοπισμός ημισφαιρίου και ανίχνευση ημέρας και νύχτας στον Διεθνή Διαστημικό Σταθμό
feature: 1
---

Ο παρακάτω κώδικας χρησιμοποιεί τη βιβλιοθήκη [ephem](https://projects.raspberrypi.org/en/projects/code-for-your-astro-pi-mission-space-lab-experiment/4) για να εντοπίσει αν είναι ημέρα ή νύχτα στο σημείο πάνω από το οποίο βρίσκεται ο ΔΔΣ. Ο κώδικας εντοπίζει, επίσης, το ημισφαίριο πάνω από το οποίο βρίσκεται ο ΔΔΣ:
```python
import ephem
from ephem import readtle, degree
import time

name = "ISS (ZARYA)"
line1 = "1 25544U 98067A   21030.23684081  .00003078  00000-0  64152-4 0  9998"
line2 = "2 25544  51.6460 305.0424 0002363 316.2883 179.5775 15.48926800267219"
iss = readtle(name, line1, line2)

def get_latlon():
    iss.compute()
    return (iss.sublat / degree, iss.sublong / degree)

sun = None
place = None

while True:

  latitude, longitude = get_latlon()

  home = ephem.Observer()
  home.lat = str(latitude)
  home.lon = str(longitude)
  
  sunrise = home.next_rising(ephem.Sun()).datetime()
  sunset = home.next_setting(ephem.Sun()).datetime()
  
  if sunset < sunrise:
      sun = "Day"
      print(sun)
  else:
      sun = "Night"
      print(sun)

  if latitude > 0:
      place = "North"
      print(place)
  else:
      place = "South"
      print(place)

  time.sleep(2)
  ```
Στον ακόλουθο σύνδεσμο μπορείτε να δείτε [το ακριβές σημείο που βρίσκεται ο ΔΔΣ αυτή τη στιγμή σύμφωνα με τα στοιχεία της NASA](https://spotthestation.nasa.gov/tracking_map.cfm).
