# Password_Analyzer-Tool
import tkinter as tk
from tkinter import messagebox
import re

def analyze_password():
    password = entry.get()
    score = 0
    suggestions = []

    # Check length
    if len(password) >= 8:
        score += 1
    else:
        suggestions.append("Password should be at least 8 characters long.")

    # Check for uppercase letters
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Include at least one uppercase letter (A-Z).")

    # Check for lowercase letters
    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Include at least one lowercase letter (a-z).")

    # Check for numbers
    if re.search(r"[0-9]", password):
        score += 1
    else:
        suggestions.append("Include at least one number (0-9).")

    # Check for special characters
    if re.search(r"[!@#$%^&*()_+=<>?/{}|~`]", password):
        score += 1
    else:
        suggestions.append("Include at least one special character (!@#$...).")

    # Check common passwords
    common_passwords = ['123456', 'password', 'admin', 'qwerty', 'abc123']
    if password.lower() in common_passwords:
        suggestions.append("This is a very common password, please change it.")
        score = 0

    # Final rating
    if score >= 4:
        result = " Strong Password"
    elif score == 3:
        result = " Medium Password"
    else:
        result = "Weak Password"

    # Show result
    message = f"Password Strength: {result}\n\n"
    if suggestions:
        message += "Suggestions:\n" + "\n".join(f"- {s}" for s in suggestions)

    messagebox.showinfo("Password Result", message)

# GUI setup
root = tk.Tk()
root.title("Password Analyzer")
root.geometry("400x250")
root.resizable(False, False)
root.configure(bg="#eaf2ff")

title = tk.Label(root, text="🔍 Password Strength Analyzer", font=("Helvetica", 14, "bold"), bg="#eaf2ff")
title.pack(pady=10)

entry = tk.Entry(root, width=30, show="*", font=("Arial", 12))
entry.pack(pady=10)

btn = tk.Button(root, text="Analyze Password", command=analyze_password, bg="#4CAF50", fg="white", font=("Arial", 11))
btn.pack(pady=20)

root.mainloop()
