---
layout: post
title: Χρήσιμος κώδικας για το πείραμά μας με το astro-pi
---

###Τυχαίοι αριθμοί
Ο παρακάτω κώδικα παράγει τυχαίους αριθμούς:
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
