import tkinter as tk

def on_click(event):
    """Handles button click event"""
    text = event.widget.cget("text")
    if text == "=":
        try:
            result.set(eval(entry.get()))
        except Exception as e:
            result.set("Error")
    elif text == "C":
        entry.set("")
        result.set("")
    else:
        entry.set(entry.get() + text)

# Create the main window
root = tk.Tk()
root.title("Calculator")

# Input field
entry = tk.StringVar()
result = tk.StringVar()
entry_field = tk.Entry(root, textvariable=entry, font=("Arial", 20), justify="right")
entry_field.grid(row=0, column=0, columnspan=4)

# Button layout
buttons = [
    "7", "8", "9", "/", 
    "4", "5", "6", "*", 
    "1", "2", "3", "-", 
    "C", "0", "=", "+"
]

row_val = 1
col_val = 0
for button in buttons:
    btn = tk.Button(root, text=button, font=("Arial", 20), width=5, height=2)
    btn.grid(row=row_val, column=col_val)
    btn.bind("<Button-1>", on_click)
    col_val += 1
    if col_val > 3:
        col_val = 0
        row_val += 1

# Result display
result_label = tk.Label(root, textvariable=result, font=("Arial", 20), fg="blue")
result_label.grid(row=row_val, column=0, columnspan=4)

root.mainloop() 
