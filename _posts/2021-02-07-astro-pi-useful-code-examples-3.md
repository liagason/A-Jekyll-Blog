---
layout: post
title: Εντοπισμός ποσοστού ξηράς σε εικόνες που ελήφθησαν από τον ΔΔΣ - Ομάδες Makerlab
---

### Ποσοστό ξηράς
Ο παρακάτω κώδικας αναλύει τα pixels μιας εικόνας και βρίσκει το ποσοστό αυτών που αντιζτοιχούν στο χρώμα της ξηράς. 
Το ποσοστό δεν είναι ακριβές καθώς μέρος των φωτογραφιών της Γης από τον ΔΔΣ είναι και το "παράθυρο" του ΔΔΣ.
```python
import cv2 
import numpy as np

# ISS images: https://www.flickr.com/photos/raspberrypi/with/31257493207/

img_name = input("Picture name (with extension)? ")

img = cv2.imread(img_name)

# Get negative from picture
imagem = cv2.bitwise_not(img)
cv2.imwrite("neg_"+img_name, imagem)

# Set negative picture as default
img = cv2.imread("neg_"+img_name)

# boundaries for LAND color
boundaries = [
    ([60, 60, 60], [170, 170, 170])
    ]

for(lower, upper) in boundaries:
    lower = np.array(lower, dtype = "uint8")
    upper = np.array(upper, dtype = "uint8")

    # finds colors in boundaries and applies a mask
    mask = cv2.inRange(img, lower, upper)
    output = cv2.bitwise_and(img, img, mask = mask)

    # saves the image
    cv2.imwrite("edit_"+img_name, output)

tot_pixel = output.size
land_pixel = np.count_nonzero(output)
percentage = round(land_pixel * 100 / tot_pixel, 2)

print("LAND pixels: " + str(land_pixel))
print("Total pixels: " + str(tot_pixel))
print("Percentage of LAND pixels: " + str(percentage) + "%")
```
Μπορείτε να [τρέξετε τον παραπάνω κώδικα στο Repl.it](https://repl.it/@liagason/Detect-Land#main.py)
