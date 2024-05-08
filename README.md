# GithubDownloadCount
see your project download count


so it's a python based file convert in exe

Python:
```
import tkinter as tk
from tkinter import messagebox
import requests

def get_download_count(repo_url):
    try:
        response = requests.get(repo_url)
        if response.status_code == 200:
            data = response.json()
            total_download_count = 0
            for release in data:
                for asset in release['assets']:
                    total_download_count += asset['download_count']
            return total_download_count
        else:
            messagebox.showerror("Error", f"Error: {response.status_code}")
            return None
    except Exception as e:
        messagebox.showerror("Error", f"Error fetching data: {str(e)}")
        return None

def get_download_count_and_display():
    NME = account_entry.get()
    PROGRAMM = repo_entry.get()
    repo_url = f"https://api.github.com/repos/{NME}/{PROGRAMM}/releases"
    download_count = get_download_count(repo_url)
    if download_count is not None:
        result_label.config(text=f"Nombre total de téléchargements : {download_count}")

window = tk.Tk()
window.title("GitHub Download Counter")

account_label = tk.Label(window, text="Enter Account Pseudo/Name:")
account_label.grid(row=0, column=0, padx=5, pady=5)
account_entry = tk.Entry(window)
account_entry.grid(row=0, column=1, padx=5, pady=5)

repo_label = tk.Label(window, text="Enter Repo Name:")
repo_label.grid(row=1, column=0, padx=5, pady=5)
repo_entry = tk.Entry(window)
repo_entry.grid(row=1, column=1, padx=5, pady=5)

fetch_button = tk.Button(window, text="Get Download Count", command=get_download_count_and_display)
fetch_button.grid(row=2, column=0, columnspan=2, padx=5, pady=5)

result_label = tk.Label(window, text="")
result_label.grid(row=3, column=0, columnspan=2, padx=5, pady=5)

window.mainloop()
```

just download exe and use it
