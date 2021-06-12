---
layout: post
title: Απλό GUI στην Python με tkinter
---

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

```python
from tkinter import *

window = Tk()
window.title("GUI example 1")
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
