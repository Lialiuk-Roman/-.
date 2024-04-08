import tkinter as tk

class CreditCardValidatorApp:
    def __init__(self, master):
        self.master = master
        master.title("Перевірка номера кредитної картки")
        master.geometry("700x100")

        self.entry = tk.Entry(master, width=20)
        self.entry.pack(pady=5)
        self.validate_button = tk.Button(master, text="Перевірити", command=self.validate_card)
        self.validate_button.pack(pady=5)
        self.result_label = tk.Label(master, text="")
        self.result_label.pack(pady=5)

    def is_valid_credit_card(self, card_number):
        card_number = ''.join(card_number.split())

        if not card_number.isdigit():
            return False

        if len(card_number) != 16:
            return False

        total = 0
        for i, digit in enumerate(card_number[::-1]):
            if i % 2 == 0:
                total += int(digit)
            else:
                doubled_digit = int(digit) * 2
                if doubled_digit > 9:
                    total += doubled_digit - 9
                else:
                    total += doubled_digit
        return total % 10 == 0

    def validate_card(self):
        card_number = self.entry.get()
        if self.is_valid_credit_card(card_number):
            self.result_label.config(text="Цей номер кредитної картки є дійсним.")
        else:
            self.result_label.config(text="Цей номер кредитної картки є недійсним.")

root = tk.Tk()
app = CreditCardValidatorApp(root)
root.mainloop()
