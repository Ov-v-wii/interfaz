aqui esta mi codigo de esamblador 

; Definir las direcciones de memoria donde están los números
NUM1 = 0x10
NUM2 = 0x11
NUM3 = 0x12

; Cargar los tres números en los registros
lod Ra, NUM1      ; Cargar el primer número en Ra
lod Rb, NUM2      ; Cargar el segundo número en Rb
add Ra            ; Sumar el valor de Rb a Ra (Ra = NUM1 + NUM2)
lod Rc, NUM3      ; Cargar el tercer número en Rc
add Ra            ; Sumar el valor de Rc a Ra (Ra = NUM1 + NUM2 + NUM3)

; Dividir la suma por 3
; Para esto, podemos usar una aproximación simple: restar 3 en un ciclo
; y contar cuántas veces lo hacemos para obtener el cociente.

; Inicializamos el divisor
mvb #3           ; Rb = 3 (el divisor)

; Empezamos la división
clr Rd            ; Limpiamos Rd (se usará para contar las divisiones)
.loop:
    sub Ra, Rb    ; Restamos 3 de Ra
    cmp Ra        ; Comparamos el resultado con 0
    jn .done      ; Si Ra es negativo, terminamos la división
    inc Rd        ; Incrementamos el contador (Rd)
    jmp .loop     ; Continuamos el ciclo

.done:
; Ahora el resultado de la división está en Rd, que es el promedio
; Guardamos el resultado en memoria o en el registro deseado
mov Ra, Rd        ; Guardamos el promedio en Ra

; Finalizamos
hlt

#Explicaicon 

primero se definen tres posiciones de memoria donde se almacenan los números de entrada.

NUM1 = 0x10
NUM2 = 0x11
NUM3 = 0x12

acontinuacion se cargan los tres números en registros y se suman en Ra, que ahora contiene NUM1 + NUM2 + NUM3.


lod Ra, NUM1     ; se carga el primer número en Ra
lod Rb, NUM2      ; se carga el segundo número en Rb
add Ra            ; sumar el valor de Rb a Ra (Ra = NUM1 + NUM2)
lod Rc, NUM3      ; se carga el tercer número en Rc
add Ra            ; sumar el valor de Rc a Ra (Ra = NUM1 + NUM2 + NUM3)

Aquí se usa una aproximación a la división por restas sucesivas. Se inicializa Rb con 3, y en cada iteración se resta 3 de Ra, contando cuántas veces se puede hacer antes de que Ra se vuelva negativo. Este conteo (Rd) representa el cociente, es decir, el promedio de los tres números.

mvb #3           ; Rb = 3 (el divisor)
clr Rd            ; Rd se usa para contar el número de restas (el cociente)

.loop:
    sub Ra, Rb    ; Restamos 3 de Ra
    cmp Ra        ; Comparamos el resultado con 0
    jn .done      ; Si Ra es negativo, terminamos la división
    inc Rd        ; Incrementamos el contador (Rd)
    jmp .loop     ; Repetimos el proceso

El resultado (promedio) queda almacenado en Ra.

.done:
mov Ra, Rd        ; Guardamos el promedio en Ra

Se detiene la ejecución.

hlt


by: Ruiz Luevano Odalys Itzel
