# Navegue até o diretório onde você deseja criar seu projeto
cd caminho/para/seu/diretorio

# Clone o repositório recém-criado
git clone https://github.com/SEU-USUARIO/tkinter-calculator.git

# Navegue para o diretório do repositório
cd tkinter-calculator

# Crie um ambiente virtual (opcional, mas recomendado)
python -m venv venv
source venv/bin/activate  # No Windows use `venv\Scripts\activate`
# calculator.py

import tkinter as tk

class Calculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Calculadora")
        
        self.display = tk.Entry(root, width=16, font=('Arial', 24), bd=2, insertwidth=4, width=14, borderwidth=4, relief='ridge')
        self.display.grid(row=0, column=0, columnspan=4)
        
        self.create_buttons()

    def create_buttons(self):
        buttons = [
            ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
            ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
            ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
            ('0', 4, 0), ('.', 4, 1), ('+', 4, 2), ('=', 4, 3),
            ('C', 5, 0, 4)
        ]

        for (text, row, col, colspan) in buttons:
            button = tk.Button(self.root, text=text, padx=20, pady=20, font=('Arial', 18), command=lambda t=text: self.on_button_click(t))
            button.grid(row=row, column=col, columnspan=colspan if colspan else 1, sticky='nsew')

        for i in range(6):
            self.root.grid_rowconfigure(i, weight=1)
        for i in range(4):
            self.root.grid_columnconfigure(i, weight=1)

    def on_button_click(self, char):
        if char == 'C':
            self.display.delete(0, tk.END)
        elif char == '=':
            try:
                result = eval(self.display.get())
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, str(result))
            except:
                self.display.delete(0, tk.END)
                self.display.insert(tk.END, "Error")
        else:
            self.display.insert(tk.END, char)

if __name__ == "__main__":
    root = tk.Tk()
    calculator = Calculator(root)
    root.mainloop()
# Adicione todos os arquivos ao estágio para commit
git add calculator.py

# Faça o commit das mudanças
git commit -m "Adiciona calculadora GUI usando tkinter"

# Envie as mudanças para o GitHub
git push origin main
python calculator.py
