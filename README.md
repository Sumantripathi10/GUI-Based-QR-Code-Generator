import qrcode 
import tkinter as tk
from tkinter import filedialog, messagebox

def generate_qr():
   
    text = entry.get()
    if not text:
        messagebox.showerror("Error", "Please enter text to generate QR code.")
        return

    qr = qrcode.QRCode(version=1, box_size=10, border=5)
    qr.add_data(text)
    qr.make(fit=True)
    img = qr.make_image(fill='black', back_color='white')

    file_path = filedialog.asksaveasfilename(defaultextension=".png", filetypes=[("PNG files", "*.png")])
    if file_path:
        img.save(file_path)
        messagebox.showinfo("Success", f"QR code saved as {file_path}")

root = tk.Tk()

root.title("QR Code Generator")

label = tk.Label(root, text="Enter text to generate QR code:")
label.pack(pady=5)

entry = tk.Entry(root, width=40)
entry.pack(pady=5)

generate_button = tk.Button(root, text="Generate and Save QR Code", command=generate_qr)
generate_button.pack(pady=10)

root.mainloop()
