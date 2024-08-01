# codsoft_internship
task1 password generator

from tkinter import *
from tkinter import ttk
import string
import random

def generator():
    small_alphabets = string.ascii_lowercase
    capital_alphabets = string.ascii_uppercase
    numbers = string.digits
    special_characters = string.punctuation

    all_characters = small_alphabets + capital_alphabets + numbers + special_characters
    try:
        password_length = int(length_Box.get())
        if password_length < 1:
            raise ValueError
    except ValueError:
        passwordField.delete(0, 'end')
        passwordField.insert(0, "Invalid length")
        return

    passwordField.delete(0, 'end')  # Clear the entry field before inserting the generated password

    if choice.get() == 1:
        generated_password = ''.join(random.choices(small_alphabets, k=password_length))
    elif choice.get() == 2:
        generated_password = ''.join(random.choices(small_alphabets + capital_alphabets, k=password_length))
    elif choice.get() == 3:
        generated_password = ''.join(random.choices(all_characters, k=password_length))
    
    passwordField.insert(0, generated_password)

def copy():
    root.clipboard_clear()
    root.clipboard_append(passwordField.get())
    root.update()

root = Tk()
root.title("Password Generator")
root.geometry("400x300")
root.config(bg='lightsteelblue')

Font = ('Arial', 12, 'bold')

# Create frames for better layout management
header_frame = Frame(root, bg='lightcoral', pady=10)
header_frame.pack(fill=X)

content_frame = Frame(root, bg='lightsteelblue', pady=10)
content_frame.pack(fill=BOTH, expand=True)

footer_frame = Frame(root, bg='lightsteelblue', pady=10)
footer_frame.pack(fill=X, side=BOTTOM)

passwordLabel = Label(header_frame, text='Password Generator', font=('Arial', 18, 'bold'), bg='lightcoral', fg='white')
passwordLabel.pack(pady=10)

choice = IntVar()

weakRadioButton = Radiobutton(content_frame, text='Weak', value=1, variable=choice, font=Font, bg='lightsteelblue')
weakRadioButton.grid(row=0, column=0, padx=10, pady=5)

mediumRadioButton = Radiobutton(content_frame, text='Medium', value=2, variable=choice, font=Font, bg='lightsteelblue')
mediumRadioButton.grid(row=0, column=1, padx=10, pady=5)

strongRadioButton = Radiobutton(content_frame, text='Strong', value=3, variable=choice, font=Font, bg='lightsteelblue')
strongRadioButton.grid(row=0, column=2, padx=10, pady=5)

lengthLabel = Label(content_frame, text='Password Length:', font=Font, bg='lightsteelblue')
lengthLabel.grid(row=1, column=0, padx=10, pady=5, sticky=W)

length_Box = Spinbox(content_frame, from_=1, to_=30, width=5, font=Font)
length_Box.grid(row=1, column=1, padx=10, pady=5)

generateButton = Button(content_frame, text='Generate', font=Font, command=generator, bg='forestgreen', fg='white')
generateButton.grid(row=1, column=2, padx=10, pady=5)

passwordField = Entry(content_frame, width=40, bd=2, font=Font)
passwordField.grid(row=2, column=0, columnspan=3, pady=10)

copyButton = Button(footer_frame, text='Copy', font=Font, bg='royalblue', fg='white', command=copy)
copyButton.pack()

root.mainloop()

