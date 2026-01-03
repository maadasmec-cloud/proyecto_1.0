import customtkinter as ctk
import csv #NUEVO: para guardar archivos
from datetime import datetime # Para saber qué dia y hora se hizo el cálculo

class MiAppNegocio(ctk.CTk):
    def __init__(self):
        super().__init__()

       

        #1. Configuración de la ventana principal
        self.title("Sistema de negocio Integrado")
        self.geometry("500x450")
        ctk.set_appearance_mode("dark")

        #2.Crear el sistema de pestañas (Tabs)
        self.pestanas = ctk.CTkTabview(self)
        self.pestanas.pack(padx=20, pady=20, fill="both", expand=True)

        # Añadimos las dos pestañas
        self.pestanas.add("Cálculo IVA")
        self.pestanas.add("Registro Edad")

        # --- DISEÑO PESTAÑA 1 (IVA) ---
        self.label_iva = ctk.CTkLabel(self.pestanas.tab("Cálculo IVA"), text="CALCULADORA DE IVA", font=("Roboto", 20, "bold"))
        self.label_iva.pack(pady=20)

        self.entry_iva = ctk.CTkEntry(self.pestanas.tab("Cálculo IVA"),placeholder_text="Monto neto")
        self.entry_iva.pack(pady=10)

        self.btn_iva = ctk.CTkButton(self.pestanas.tab("Cálculo IVA"), text="Calcular Total", command=self.calcular_iva)
        self.btn_iva.pack(pady=10)

        self.res_iva =ctk.CTkLabel(self.pestanas.tab("Cálculo IVA"), text="Total: $0", font=("Roboto", 16))
        self.res_iva.pack(pady=20)

        # --- DISEÑO PESTAÑA 2 (EDAD) ---
        self.label_e = ctk.CTkLabel(self.pestanas.tab("Registro Edad"), text="CALCULADORA DE EDAD", font=("Roboto", 20, "bold"))
        self.label_e.pack(pady=20)

        self.entry_nombre = ctk.CTkEntry(self.pestanas.tab("Registro Edad"), placeholder_text="Nombre")
        self.entry_nombre.pack(pady=10)

        self.entry_year = ctk.CTkEntry(self.pestanas.tab("Registro Edad"), placeholder_text="Año de nacimiento")
        self.entry_year.pack(pady=10)

        self.btn_edad = ctk.CTkButton(self.pestanas.tab("Registro Edad"), text="Calcular Edad", command=self.calcular_edad)
        self.btn_edad.pack(pady=10)

        self.res_edad = ctk.CTkLabel(self.pestanas.tab("Registro Edad"), text="", font=("Roboto", 14))
        self.res_edad.pack(pady=20)


        # --- MÉTODOS (Lógica de los botones) ---
    def calcular_iva(self):
        try:
            # Capturamos el dato de la pestaña de IVA
            monto = float(self.entry_iva.get())
            total = monto * 1.19
            res_texto =f"${total:,.0f}"

            #GUARDAR EN UN EXCEL/CSV
            self.guardar_datos("IVA", f"Monto neto: {monto}", res_texto)

            # Actualizamos el Label de esa pestaña
            self.res_iva.configure(text=f"Total (con 19% IVA): ${total:,.0f}", text_color="#2ecc71")
        except ValueError:
            self.res_iva.configure(text="Error: Ingresa un número", text_color="#e74c3c")

    def calcular_edad(self):
        try:
            # Capturamos los datos de la pestaña de Edad
            nombre = self.entry_nombre.get().capitalize()
            año = int(self.entry_year.get())
            edad = 2026 - año
            res_texto =f"{edad} años"
            # Actualizamos el Label de esa pestaña
            self.res_edad.configure(text=f"Hola {nombre}, tienes {res_texto} años.", text_color="#3498db")

            #GUARDAR EN EXCEL/CSV
            self.guardar_datos("EDAD", f"Usuario: {nombre}", res_texto)
        except ValueError:
            self.res_edad.configure(text="Error: Año inválido", text_color="#e74c3c")
     # --- NUEVA FUNCIÓN: EL MOTOR DE MOMERIA---
    def guardar_datos(self, tipo_calculo, detalle, resultado):
            fecha_hora = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

            #Abrimos (o creamos) el archivo 'historial.csv' el modo "append" (añadir)
            with open("historial_negocio.csv", mode="a", newline="", encoding="utf-8") as archivo:
                escritor = csv.writer(archivo)
                #Escribimos una fila con los datos
                escritor.writerow([fecha_hora, tipo_calculo, detalle, resultado])


# --- FINAL DEL ARCHIVO ---
if __name__ == "__main__":
    app = MiAppNegocio()
    app.mainloop()
