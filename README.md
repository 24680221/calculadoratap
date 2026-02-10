# calculadoratap

Se explicara el desarrollo de una interfaz de una calculadora para ello primero se nesecesita instalar flet:
Se creara un entorno virtual para nuestros proyectos  flet:

1.- se crea un nuevo directorio para el proyecto
```Python
mkdir my-app
cd my-app
```
2.- pasamos a crear el entorno virtual
```Python
python -m venv .venv  
source .venv/bin/actívate
```
3.- se instala flet y agregarlo a las dependencias del proyecto
```Python
pip install 'flet[all]'
```
4.- verificar que el flet se allá instalado correctamente
```Python
flet --version
o
flet doctor
```
5.- actualizer flet
```Python
pip install 'flet[all]' –upgrade
```
despues de haber hecho la instalación de flet, se abre visual studio code, ir ala carpeta que se creo de flet.


Inicialmente se genera una pagina donde pondremos el codigo, en el primer renglon se importa la libreria donde se importa el flet la cual se encarga de crear la interfaz grafica.
```Python
import flet as ft
```
En el primer parrafo se encarga de crear la ventana de la aplicacion la funcion se llama page, tambien se agrega la calculadora tap que sera el titulo de la ventana, se define width que es el ancho y height la altura de la ventana.
```Python
def main(page: ft.Page):
    page.title = "calculadora tap"
    page.window_width = 250
    page.window_height = 400
```
En esta parte se encarga de crear el texto que se mostrara, empieza en cero y su tamaño de letra,el texto cambiara una vez que se presionen los botones.
```Python
display_text = ft.Text("0", size=30)
```
En el segundo parrafo se creara el display, el cual se encarga de diseñar lo que va adentro es decir el texto (content), color de fondo,sus bordes sean redondeados, la alineacion del texto, el espacio interno y el tamaño del display.   
```Python
display = ft.Container(
        content=display_text,
        bgcolor=ft.Colors.BLACK12,
        border_radius=8,
        alignment=ft.alignment.Alignment(1, 0),
        padding=10,
        width=210, #Forzamosel ancho manualmente
        height=70,

    )
```
En el tercer parrafo se crea la funcion del botón,  la funcion botton_click se encarga de ejecutar cuando se presione un boton, en el resto del parrafo se crea un evento con e, control es el encargado del boton presionado. y data es el valor del boton, despues se verfica que boton se presiono y la logica del boton presionado si se preosina AC se devuelve 0 y lo reemplazza, para despues refrescar la interfaz.
```Python
def botton_click(e):
        valor = str(e.control.data).strip()
        print("boton presionado:", valor)

        if valor == "AC":
            display_text.value = "0"
        else:
            if display_text.value == "0":
                display_text.value = valor
            else:
                display_text.value += valor    

        page.update()
```
En el cuarto parrafo se crea la funcion de botones, el crear_boton se encarga de crear botones sin repetir codigo, lo que sigue es que cada boton muestra un texto, tiene un tamaño, guarda su valor y ejecuta la funcion al hacer clic.
```Python
def crear_boton(valor):
        return ft.Button(
            content=ft.Text(valor),
            width=90,
            height=50,
            data=valor,
            on_click=botton_click 

        )  
```
En el quinto parrafo se crea la cuadricula de botones, la cual crea un espacio para colocar los botones con 2 columnas, un espacio entre los botones y un tamaño fijo (ancho y alto), el expand indicara si el componente mantiene un tamaño fijo y no se expande para ocupar el espacio disponible.
```Python
grid = ft.GridView(
        runs_count=2,
        spacing=10,
        run_spacing=10,
        width=210, #Ancho fijo igual al display
        height=200, #Alto fijo para que no crezca
        expand=False

    )
```
El sexto parrafo se encarga de agregar botones (1,2,3,AC), el grid.controls se encarga de en listar los elementos dentro del grid,append agrega un nuevo elemento en la lista y crear_boton crea el boton.
```Python
    grid.controls.append(crear_boton("1"))
    grid.controls.append(crear_boton("2"))
    grid.controls.append(crear_boton("3"))
    grid.controls.append(crear_boton("AC")) 
```
En el septimo parrafo se crea el layout principal que se encarga de la organizacion de la interfaz, arriba el display y abajo los botones y todo en una columna vertical.
```Python
layout_principal = ft.Column(
        controls=[
            display,
            grid
        ],
        tight=True
    )
```
Esta linea del codigo se encarga de mostrar la interfaz en la pantalla.
```Python
page.add(layout_principal)
```
En esta parte y ultima se encarga de iniciar la aplicacion y llamar ala funcion main
```Python
ft.app(target=main)
```

A contiuacion se muestra el codigo completo:
```Python
import flet as ft
def main(page: ft.Page):
    page.title = "calculadora tap"
    page.window_width = 250
    page.window_height = 400
    

    display_text = ft.Text("0", size=30)

    display = ft.Container(
        content=display_text,
        bgcolor=ft.Colors.BLACK12,
        border_radius=8,
        alignment=ft.alignment.Alignment(1, 0),
        padding=10,
        width=210, #Forzamosel ancho manualmente
        height=70,

    )

    
    def botton_click(e):
        valor = str(e.control.data).strip()
        print("boton presionado:", valor)

        if valor == "AC":
            display_text.value = "0"
        else:
            if display_text.value == "0":
                display_text.value = valor
            else:
                display_text.value += valor    

        page.update()   


    def crear_boton(valor):
        return ft.Button(
            content=ft.Text(valor),
            width=90,
            height=50,
            data=valor,
            on_click=botton_click 

        )      

    grid = ft.GridView(
        runs_count=2,
        spacing=10,
        run_spacing=10,
        width=210, #Ancho fijo igual al display
        height=200, #Alto fijo para que no crezca
        expand=False

    )

    grid.controls.append(crear_boton("1"))
    grid.controls.append(crear_boton("2"))
    grid.controls.append(crear_boton("3"))
    grid.controls.append(crear_boton("AC"))   
   
    layout_principal = ft.Column(
        controls=[
            display,
            grid
        ],
        tight=True
    )

    

    page.add(layout_principal)
   
ft.app(target=main)
```

A continuacion se visualiza el resultado de todo el codigo:


<img width="289" height="420" alt="image" src="https://github.com/user-attachments/assets/d2c9bb7a-f56e-4094-aa35-192e93aeb804" />
