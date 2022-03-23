---
layout: post
title: Απλά GUI στην Python με tkinter
feature: 1
---

Παρακάτω ακολουθούν κάποια απλά παραδείγματα γραφικού περιβάλλοντος στην Python με τη χρήση της βιβλιοθήκης [tkinter](https://docs.python.org/3/library/tkinter.html).

<br><br>
## Παράδειγμα 1
Στο πρώτο παράδειγμα θα φτιάξουμε ένα παράθυρο που έχει ένα μικρό κείμενο κι ένα κουμπί. Προς το παρόν το κουμπί δεν θα κάνει κάτι!<br>
Προσέξτε την εντολή window.mainloop(). Αυτή εμφανίζει το παράθυρό μας και το κρατάει ανοικτό, μέχρι να το κλείσουμε με κάποιον τρόπο εμείς!
```python
from tkinter import *

window = Tk()
window.title("Ο τίτλος μου")
window.geometry('300x100')

name = "Μαρίνα"

lbl = Label(window, text="Γεια σου " + name)
lbl.grid(column=0, row=0)

btn = Button(window, text="Ένα κουμπί")
btn.grid(column=1, row=0)

window.mainloop()
```

<br><br>
## Παράδειγμα 2
Σε αυτό το παράδειγμα προσθέσαμε κάποια λειτουργικότητα στο κουμπί. Όταν το πατάμε αλλάζει το κείμενο που έχουμε μέσα στο παράθυρό μας.
```python
from tkinter import *

window = Tk()
window.title("Ο τίτλος μου")
window.geometry('400x100')

name = "Μαρίνα"

lbl = Label(window, text="Γεια σου " + name)
lbl.grid(column=0, row=0)

def clicked():
    lbl.configure(text="Η " + name + " πάτησε το κουμπί.")

btn = Button(window, text="Πάτησε αυτό το κουμπί", bg="orange", fg="red", command=clicked)
btn.grid(column=1, row=0)

window.mainloop()
```

Παράδειγμα 3
```python
from tkinter import *
from tkinter import messagebox

window = Tk()
window.title("¨ο τίτλος μου")
window.geometry('300x100')

name = "Μαρίνα"

lbl = Label(window, text="Γεια σου " + name)
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = Entry(window, width=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    messagebox.showinfo('Τίτλος μηνύματος', 'Πάτησες το κουμπί.')

btn = Button(window, text="Πάτησέ με", bg="white", fg="green", command=clicked)
btn.grid(column=2, row=0,sticky="nsew", padx=(5, 5), pady=(5, 5))

window.grid_columnconfigure(0, weight=1)
window.grid_columnconfigure(1, weight=12)
window.grid_columnconfigure(2, weight=1)

window.mainloop()
```

Παράδειγμα 4
```python
from tkinter import *
from tkinter import messagebox

window = Tk()
window.title("Ο τίτλος μου")
window.geometry('300x100')

name = "Μαρίνα"

lbl = Label(window, text="Γεια σου " + name)
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = Entry(window, width=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    name = txt.get()
    lbl.configure(text= "Γεια σου " + name)
    messagebox.showinfo('Τίτλος μηνύματος', 'Άλλαξες το όνομά σου.')

def clear():
    txt.delete(0,"end")

btn = Button(window, text="Αλλαγή ονόματος", bg="white", fg="green", command=clicked)
btn.grid(column=0, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

btn2 = Button(window, text="Καθάρισμα", bg="white", fg="red", command=clear)
btn2.grid(column=1, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

window.grid_columnconfigure(0, weight=1)
window.grid_columnconfigure(1, weight=2)
window.mainloop()
```

Παράδειγμα 5
```python
from tkinter import *
from tkinter import messagebox
from tkinter import scrolledtext

window = Tk()
window.title("Ο τίτλος μου")
window.geometry('500x300')

name = "Μαρίνα"

lbl = Label(window, text="Γεια σου " + name, bg="yellow")
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = scrolledtext.ScrolledText(window,width=40,height=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    name = txt.get(0.0,END)
    lbl.configure(text= "Γεια σου " + name)
    messagebox.showinfo('Τίτλος μηνύματος', 'Το όνομά σου άλλαξε.')
    txt.insert(INSERT," πρόσθεσα_κείμενο_στη_γραμμή")
    txt.insert(INSERT,"\nπρόσθεσα_άλλη_μία_γραμμή")

def clear():
    txt.delete(0.0,END)

btn = Button(window, text="Αλλαγή ονόματος", bg="white", fg="green", command=clicked)
btn.grid(column=0, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

btn2 = Button(window, text="Καθαρισμός", bg="white", fg="red", command=clear)
btn2.grid(column=1, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

def radio():
    messagebox.showinfo('Μήνυμα', selected.get())

selected = IntVar()
rad1 = Radiobutton(window,text='Πρώτη επιλογή', value=1, variable=selected, command=radio, width=30)
rad2 = Radiobutton(window,text='Δεύτερη επιλογή', value=2, variable=selected, command=radio, width=30)
rad3 = Radiobutton(window,text='Τρίτη επιλογή', value=3, variable=selected, command=radio, width=30)
rad1.grid(column=0, row=2)
rad2.grid(column=0, row=3)
rad3.grid(column=0, row=4)

window.grid_columnconfigure(0, weight=1)
window.grid_columnconfigure(1, weight=2)
window.mainloop()
```
