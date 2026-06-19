import tkinter as tk
from tkinter import font

# ---------------- FUNCIONES ----------------
def click_boton(valor):
    entrada_actual = pantalla.get()
    pantalla.delete(0, tk.END)
    pantalla.insert(tk.END, entrada_actual + str(valor))

def borrar():
    pantalla.delete(0, tk.END)

def calcular():
    try:
        resultado = eval(pantalla.get())
        pantalla.delete(0, tk.END)
        pantalla.insert(tk.END, str(resultado))
    except Exception:
        pantalla.delete(0, tk.END)
        pantalla.insert(tk.END, "Error")

# ---------------- VENTANA ----------------
ventana = tk.Tk()
ventana.title("🐰 Calculadora Conejo Azul")
ventana.geometry("350x620")
ventana.configure(bg="#0f172a")
ventana.resizable(False, False)

# ---------------- FUENTES ----------------
fuente_pantalla = font.Font(
    family="Helvetica",
    size=28,
    weight="bold"
)

fuente_botones = font.Font(
    family="Helvetica",
    size=16,
    weight="bold"
)

# ---------------- DIBUJO DEL CONEJO ----------------
canvas = tk.Canvas(
    ventana,
    width=300,
    height=140,
    bg="#0f172a",
    highlightthickness=0
)
canvas.pack(pady=(10, 5))

# Orejas
canvas.create_oval(
    95, 10, 130, 90,
    outline="#7dd3fc",
    width=4
)

canvas.create_oval(
    170, 10, 205, 90,
    outline="#7dd3fc",
    width=4
)

# Interior de orejas
canvas.create_oval(
    105, 20, 120, 80,
    outline="#bae6fd",
    width=2
)

canvas.create_oval(
    180, 20, 195, 80,
    outline="#bae6fd",
    width=2
)

# Cabeza
canvas.create_oval(
    70, 60, 230, 200,
    outline="#38bdf8",
    width=4
)

# Ojos
canvas.create_oval(
    115, 105, 130, 120,
    fill="white",
    outline="white"
)

canvas.create_oval(
    170, 105, 185, 120,
    fill="white",
    outline="white"
)

# Pupilas
canvas.create_oval(
    120, 110, 125, 115,
    fill="black"
)

canvas.create_oval(
    175, 110, 180, 115,
    fill="black"
)

# Nariz
canvas.create_polygon(
    145, 125,
    155, 125,
    150, 135,
    fill="#f9a8d4",
    outline="#f9a8d4"
)

# Boca
canvas.create_line(
    150, 135,
    140, 145,
    fill="white",
    width=2
)

canvas.create_line(
    150, 135,
    160, 145,
    fill="white",
    width=2
)

# Bigotes izquierdos
canvas.create_line(
    85, 120, 140, 125,
    fill="white",
    width=2
)

canvas.create_line(
    85, 130, 140, 130,
    fill="white",
    width=2
)

canvas.create_line(
    85, 140, 140, 135,
    fill="white",
    width=2
)

# Bigotes derechos
canvas.create_line(
    160, 125, 215, 120,
    fill="white",
    width=2
)

canvas.create_line(
    160, 130, 215, 130,
    fill="white",
    width=2
)

canvas.create_line(
    160, 135, 215, 140,
    fill="white",
    width=2
)

# ---------------- PANTALLA ----------------
pantalla = tk.Entry(
    ventana,
    font=fuente_pantalla,
    bg="#1e40af",
    fg="white",
    bd=0,
    justify="right",
    insertbackground="white"
)

pantalla.pack(
    fill="both",
    ipadx=8,
    ipady=25,
    padx=20,
    pady=15
)

# ---------------- CONTENEDOR DE BOTONES ----------------
contenedor_botones = tk.Frame(
    ventana,
    bg="#0f172a"
)

contenedor_botones.pack(
    fill="both",
    expand=True,
    padx=20,
    pady=(0, 20)
)

for i in range(5):
    contenedor_botones.rowconfigure(i, weight=1)

for j in range(4):
    contenedor_botones.columnconfigure(j, weight=1)

# ---------------- BOTONES ----------------
botones = [
    ('C', 0, 0, "#ef4444", "white", borrar),
    ('(', 0, 1, "#60a5fa", "white", lambda: click_boton('(')),
    (')', 0, 2, "#60a5fa", "white", lambda: click_boton(')')),
    ('/', 0, 3, "#38bdf8", "white", lambda: click_boton('/')),

    ('7', 1, 0, "#2563eb", "white", lambda: click_boton('7')),
    ('8', 1, 1, "#2563eb", "white", lambda: click_boton('8')),
    ('9', 1, 2, "#2563eb", "white", lambda: click_boton('9')),
    ('*', 1, 3, "#38bdf8", "white", lambda: click_boton('*')),

    ('4', 2, 0, "#2563eb", "white", lambda: click_boton('4')),
    ('5', 2, 1, "#2563eb", "white", lambda: click_boton('5')),
    ('6', 2, 2, "#2563eb", "white", lambda: click_boton('6')),
    ('-', 2, 3, "#38bdf8", "white", lambda: click_boton('-')),

    ('1', 3, 0, "#2563eb", "white", lambda: click_boton('1')),
    ('2', 3, 1, "#2563eb", "white", lambda: click_boton('2')),
    ('3', 3, 2, "#2563eb", "white", lambda: click_boton('3')),
    ('+', 3, 3, "#38bdf8", "white", lambda: click_boton('+')),

    ('0', 4, 0, "#2563eb", "white", lambda: click_boton('0')),
    ('.', 4, 1, "#2563eb", "white", lambda: click_boton('.')),
    ('=', 4, 2, "#22c55e", "white", calcular)
]

# ---------------- CREACIÓN DE BOTONES ----------------
for texto, fila, col, bg_color, fg_color, comando in botones:
    boton = tk.Button(
        contenedor_botones,
        text=texto,
        bg=bg_color,
        fg=fg_color,
        font=fuente_botones,
        bd=0,
        cursor="hand2",
        activebackground="#93c5fd",
        activeforeground="black",
        command=comando
    )

    if texto == '=':
        boton.grid(
            row=fila,
            column=col,
            columnspan=2,
            sticky="nsew",
            padx=4,
            pady=4
        )
    else:
        boton.grid(
            row=fila,
            column=col,
            sticky="nsew",
            padx=4,
            pady=4
        )

# ---------------- INICIAR APP ----------------
ventana.mainloop()
