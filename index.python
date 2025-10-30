import tkinter as tk
from tkinter import messagebox, ttk

class GoaTripCalculator(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Goa Trip Cost Calculator")
        self.geometry("500x650")
        self.configure(bg="#f0f8ff")
        self.selected_items = []

        title = tk.Label(self, text="GOA TRIP COST CALCULATOR", font=("Arial", 20, "bold"), fg="#007acc", bg="#f0f8ff")
        title.pack(pady=15)

        self.category_frames = {}
        self.create_categories()
        self.selected_box()
        self.total_box()
        self.print_button()

    def create_categories(self):
        categories = {
            "Transportation": [("Bus", 500), ("Train", 700), ("Flight", 3000)],
            "Hotel": [("Hotel A", 2000), ("Hotel B", 2500)],
            "Sightseeing": [
                ("Fort Aguada", 500), ("Calangute Beach", 400), ("Baga Beach", 400),
                ("Palolem Beach", 600), ("Colva Beach", 500), ("Cabo De Rama Fort", 700)
            ],
            "Water Sports": [("Jet Ski", 1500), ("Parasailing", 2000)]
        }

        for name, items in categories.items():
            btn = tk.Button(self, text=name, bg="#007acc", fg="white", font=("Arial", 12),
                            command=lambda n=name: self.toggle_category(n))
            btn.pack(fill="x", padx=20, pady=5)

            frame = tk.Frame(self, bg="#e6f4ff")
            frame.pack(fill="x", padx=25, pady=2)
            frame.pack_forget()
            self.category_frames[name] = frame

            for title, cost in items:
                item_btn = tk.Button(frame, text=f"{title} – ₹{cost}", bg="#e6f4ff", anchor="w",
                                     command=lambda t=title, c=cost, b=frame: self.toggle_item(t, c))
                item_btn.pack(fill="x", pady=2)
    
    def toggle_category(self, name):
        for n, frame in self.category_frames.items():
            if n == name:
                if frame.winfo_viewable():
                    frame.pack_forget()
                else:
                    frame.pack(fill="x", padx=25, pady=2)
            else:
                frame.pack_forget()

    def toggle_item(self, name, cost):
        existing = next((item for item in self.selected_items if item['name'] == name), None)
        if existing:
            self.selected_items = [i for i in self.selected_items if i['name'] != name]
        else:
            self.selected_items.append({'name': name, 'cost': cost})
        self.update_selected_items()

    def selected_box(self):
        box_frame = tk.Frame(self, bg="white", bd=1, relief="solid")
        box_frame.pack(fill="x", padx=25, pady=10)
        label = tk.Label(box_frame, text="Selected Items:", fg="#007acc", bg="white", font=("Arial", 12, "bold"))
        label.pack(anchor="w", padx=5, pady=3)
        self.selected_list = tk.Listbox(box_frame, bg="white", fg="#007acc", font=("Arial", 11))
        self.selected_list.pack(fill="both", padx=10, pady=5)

    def update_selected_items(self):
        self.selected_list.delete(0, tk.END)
        total = 0
        for item in self.selected_items:
            total += item['cost']
            self.selected_list.insert(tk.END, f"{item['name']} – ₹{item['cost']}")
        self.total_label.config(text=f"Grand Total: ₹{total}")

    def total_box(self):
        total_frame = tk.Frame(self, bg="#e6f4ff")
        total_frame.pack(fill="x", padx=25, pady=5)
        self.total_label = tk.Label(total_frame, text="Grand Total: ₹0", fg="#007acc",
                                    bg="#e6f4ff", font=("Arial", 12, "bold"))
        self.total_label.pack(anchor="e", padx=10)
        
    def print_button(self):
        print_btn = tk.Button(self, text="🖨️ Show & Print Trip Details", bg="#28a745", fg="white",
                              font=("Arial", 12, "bold"), command=self.print_details)
        print_btn.pack(fill="x", padx=25, pady=10)

    def print_details(self):
        if not self.selected_items:
            messagebox.showwarning("Warning", "No items selected for the trip!")
            return

        total = sum(item['cost'] for item in self.selected_items)
        details = "\n".join([f"{i['name']} – ₹{i['cost']}" for i in self.selected_items])
        print_text = f"GOA TRIP DETAILS\n\n{details}\n\nGrand Total: ₹{total}"
        
        print_window = tk.Toplevel(self)
        print_window.title("Trip Summary")
        text = tk.Text(print_window, wrap="word", fg="#007acc", bg="#f0f8ff", font=("Arial", 12))
        text.insert(tk.END, print_text)
        text.config(state="disabled")
        text.pack(padx=20, pady=20, fill="both", expand=True)

if __name__ == "__main__":
    app = GoaTripCalculator()
    app.mainloop()
