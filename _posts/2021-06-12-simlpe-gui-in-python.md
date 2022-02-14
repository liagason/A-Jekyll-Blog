---
layout: post
title: Απλό GUI στην Python με tkinter
feature: 1
---

Μερικά απλά παραδείγματα για να ξεκινήσουμε να φτιάχνουμε γραφικά περιβάλλοντα με την Python.

Παράδειγμα 1
```python
from tkinter import *

window = Tk()
window.title("GUI example 1")
window.geometry('300x100')

name = "John"

lbl = Label(window, text="Hello " + name)
lbl.grid(column=0, row=0)

btn = Button(window, text="Click this button")
btn.grid(column=1, row=0)

window.mainloop()
```

Παράδειγμα 2
```python
from tkinter import *

window = Tk()
window.title("GUI example 2")
window.geometry('300x100')

name = "John"

lbl = Label(window, text="Hello " + name)
lbl.grid(column=0, row=0)

def clicked():
    lbl.configure(text= name + " clicked the button.")

btn = Button(window, text="Click this button", bg="orange", fg="red", command=clicked)
btn.grid(column=1, row=0)

window.mainloop()
```

Παράδειγμα 3
```python
from tkinter import *
from tkinter import messagebox

window = Tk()
window.title("GUI example 3")
window.geometry('300x100')

name = "John"

lbl = Label(window, text="Hello " + name)
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = Entry(window, width=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    lbl.configure(text= "Hello " + name)
    messagebox.showinfo('Message', 'Your name has changed.')

btn = Button(window, text="Change name", bg="white", fg="green", command=clicked)
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
window.title("GUI example 4")
window.geometry('300x100')

name = "John"

lbl = Label(window, text="Hello " + name)
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = Entry(window, width=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    name = txt.get()
    lbl.configure(text= "Hello " + name)
    messagebox.showinfo('Message', 'Your name has changed.')

def clear():
    txt.delete(0,"end")

btn = Button(window, text="Change name", bg="white", fg="green", command=clicked)
btn.grid(column=0, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

btn2 = Button(window, text="Clear text", bg="white", fg="red", command=clear)
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
window.title("GUI example 5")
window.geometry('500x300')

name = "John"

lbl = Label(window, text="Hello " + name, bg="yellow")
lbl.grid(column=0, row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

txt = scrolledtext.ScrolledText(window,width=40,height=10)
txt.grid(column=1,row=0,sticky="nsew",padx=(5, 5), pady=(5, 5))

def clicked():
    name = txt.get(0.0,END)
    lbl.configure(text= "Hello " + name)
    messagebox.showinfo('Message', 'Your name has changed.')
    txt.insert(INSERT," line_1")
    txt.insert(INSERT,"\nline_2")

def clear():
    txt.delete(0.0,END)

btn = Button(window, text="Change name", bg="white", fg="green", command=clicked)
btn.grid(column=0, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

btn2 = Button(window, text="Clear text", bg="white", fg="red", command=clear)
btn2.grid(column=1, row=1,sticky="nsew", padx=(5, 5), pady=(5, 5))

def radio():
    messagebox.showinfo('Message', selected.get())

selected = IntVar()
rad1 = Radiobutton(window,text='First', value=1, variable=selected, command=radio, width=30)
rad2 = Radiobutton(window,text='Second', value=2, variable=selected, command=radio, width=30)
rad3 = Radiobutton(window,text='Third', value=3, variable=selected, command=radio, width=30)
rad1.grid(column=0, row=2)
rad2.grid(column=0, row=3)
rad3.grid(column=0, row=4)

window.grid_columnconfigure(0, weight=1)
window.grid_columnconfigure(1, weight=2)
window.mainloop()
```
