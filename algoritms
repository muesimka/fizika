"""программа   логические элементы"""


import tkinter as tk
from tkinter import ttk, messagebox, scrolledtext


def invert(a: bool) -> bool:
    return not a

def conjunction(a: bool, b: bool) -> bool:
    return a and b

def disjunction(a: bool, b: bool) -> bool:
    return a or b

def implication(a: bool, b: bool) -> bool:
    return (not a) or b

def equivalence(a: bool, b: bool) -> bool:
    return a == b

OPERATIONS = {
    "1": {
        "ru": "Инверсия (Отрицание)",
        "en": "Inversion (Negation)",
        "symbol": "¬A  /  ~A",
        "func": invert,
        "needs_b": False
    },
    "2": {
        "ru": "Конъюнкция (Логическое умножение)",
        "en": "Conjunction (Logical AND)",
        "symbol": "A ∧ B",
        "func": conjunction,
        "needs_b": True
    },
    "3": {
        "ru": "Дизъюнкция (Логическое сложение)",
        "en": "Disjunction (Logical OR)",
        "symbol": "A ∨ B",
        "func": disjunction,
        "needs_b": True
    },
    "4": {
        "ru": "Импликация (Логическое следование)",
        "en": "Implication",
        "symbol": "A → B",
        "func": implication,
        "needs_b": True
    },
    "5": {
        "ru": "Эквивалентность (Логическое равенство)",
        "en": "Equivalence",
        "symbol": "A ↔ B",
        "func": equivalence,
        "needs_b": True
    },
}



class TruthTableApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Таблицы истинности / Truth Tables")
        self.root.geometry("620x580")
        self.root.resizable(False, False)
        self.root.configure(bg="#f0f4f8")


        style = ttk.Style()
        style.theme_use("clam")
        style.configure("TLabel", background="#f0f4f8", font=("Segoe UI", 10))
        style.configure("Header.TLabel", font=("Segoe UI", 14, "bold"), background="#f0f4f8")
        style.configure("TButton", font=("Segoe UI", 10), padding=6)
        style.configure("TRadiobutton", background="#f0f4f8", font=("Segoe UI", 10))

        self.create_widgets()

    def create_widgets(self):

        header = ttk.Label(self.root, text="Логические операции / Logical Operations", style="Header.TLabel")
        header.pack(pady=(15, 10))


        frame_ops = ttk.LabelFrame(self.root, text="Выберите операцию / Choose operation", padding=10)
        frame_ops.pack(padx=20, pady=5, fill="x")

        self.op_var = tk.StringVar(value="2")

        for key, op in OPERATIONS.items():
            text = f"{key}. {op['ru']}  —  {op['en']}   [{op['symbol']}]"
            rb = ttk.Radiobutton(frame_ops, text=text, variable=self.op_var, value=key,
                                 command=self.on_op_change)
            rb.pack(anchor="w", pady=2)


        frame_input = ttk.LabelFrame(self.root, text="Ввод значений / Input values", padding=10)
        frame_input.pack(padx=20, pady=10, fill="x")


        row_a = ttk.Frame(frame_input)
        row_a.pack(fill="x", pady=5)
        ttk.Label(row_a, text="A =", font=("Segoe UI", 11, "bold")).pack(side="left", padx=(0, 10))
        self.a_var = tk.IntVar(value=1)
        ttk.Radiobutton(row_a, text="1 (Истина / True)", variable=self.a_var, value=1).pack(side="left", padx=5)
        ttk.Radiobutton(row_a, text="0 (Ложь / False)", variable=self.a_var, value=0).pack(side="left", padx=5)


        self.row_b = ttk.Frame(frame_input)
        self.row_b.pack(fill="x", pady=5)
        ttk.Label(self.row_b, text="B =", font=("Segoe UI", 11, "bold")).pack(side="left", padx=(0, 10))
        self.b_var = tk.IntVar(value=1)
        ttk.Radiobutton(self.row_b, text="1 (Истина / True)", variable=self.b_var, value=1).pack(side="left", padx=5)
        ttk.Radiobutton(self.row_b, text="0 (Ложь / False)", variable=self.b_var, value=0).pack(side="left", padx=5)


        frame_btn = ttk.Frame(self.root)
        frame_btn.pack(pady=10)

        ttk.Button(frame_btn, text="▶  Вычислить / Calculate", command=self.calculate).pack(side="left", padx=8)
        ttk.Button(frame_btn, text="📋  Показать таблицу / Show table", command=self.show_table).pack(side="left", padx=8)
        ttk.Button(frame_btn, text="Очистить / Clear", command=self.clear_result).pack(side="left", padx=8)


        frame_result = ttk.LabelFrame(self.root, text="Результат / Result", padding=10)
        frame_result.pack(padx=20, pady=5, fill="both", expand=True)

        self.result_text = scrolledtext.ScrolledText(frame_result, height=8, font=("Consolas", 11),
                                                     wrap=tk.WORD, state="disabled", bg="#ffffff")
        self.result_text.pack(fill="both", expand=True)


        self.on_op_change()

    def on_op_change(self):
        """Скрываем/показываем поле B в зависимости от операции"""
        op = OPERATIONS[self.op_var.get()]
        if op["needs_b"]:
            self.row_b.pack(fill="x", pady=5)
        else:
            self.row_b.pack_forget()

    def calculate(self):
        op_key = self.op_var.get()
        op = OPERATIONS[op_key]
        a = bool(self.a_var.get())

        if op["needs_b"]:
            b = bool(self.b_var.get())
            result = op["func"](a, b)
            text = (f"Операция: {op['ru']}\n"
                    f"Operation: {op['en']}\n"
                    f"Обозначение: {op['symbol']}\n\n"
                    f"A = {int(a)}   B = {int(b)}\n\n"
                    f"Результат = {int(result)}   "
                    f"({'ИСТИНА / TRUE' if result else 'ЛОЖЬ / FALSE'})")
        else:
            result = op["func"](a)
            text = (f"Операция: {op['ru']}\n"
                    f"Operation: {op['en']}\n"
                    f"Обозначение: {op['symbol']}\n\n"
                    f"A = {int(a)}\n\n"
                    f"Результат = {int(result)}   "
                    f"({'ИСТИНА / TRUE' if result else 'ЛОЖЬ / FALSE'})")

        self.show_result(text)

    def show_table(self):
        op_key = self.op_var.get()
        op = OPERATIONS[op_key]

        lines = []
        lines.append(f"Таблица истинности: {op['ru']}")
        lines.append(f"Truth table: {op['en']}")
        lines.append(f"Обозначение: {op['symbol']}")
        lines.append("=" * 40)

        if not op["needs_b"]:
            lines.append(f"{'A':^6} | {'Результат':^12}")
            lines.append("-" * 22)
            for a in (1, 0):
                res = int(op["func"](bool(a)))
                lines.append(f"{a:^6} | {res:^12}")
        else:
            lines.append(f"{'A':^5} | {'B':^5} | {'Результат':^12}")
            lines.append("-" * 28)
            for a in (1, 0):
                for b in (1, 0):
                    res = int(op["func"](bool(a), bool(b)))
                    lines.append(f"{a:^5} | {b:^5} | {res:^12}")

        self.show_result("\n".join(lines))

    def show_result(self, text: str):
        self.result_text.config(state="normal")
        self.result_text.delete("1.0", tk.END)
        self.result_text.insert(tk.END, text)
        self.result_text.config(state="disabled")

    def clear_result(self):
        self.show_result("")


if __name__ == "__main__":
    root = tk.Tk()
    app = TruthTableApp(root)
    root.mainloop()
