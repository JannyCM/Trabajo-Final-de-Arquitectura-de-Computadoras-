# Trabajo-Final-de-Arquitectura-de-Computadoras-
Proyecto 21
Mi proyecto es el numero 21 el cual consiste en desarrollar una aplicación en lenguaje ensamblador que calcule el área y perímetro de figuras geométricas como el triángulo, cuadrado y circulo mediante la entrada de datos correspondientes por el usuario.
Para esto me he apoyado en las siguientes ecuaciones:
Triangulo:
Area: A= (b x h) /2
Perímetro: P=b + h + l
Cuadrado:
Área=b x h
Perímetro=4 x l
Circulo:
Area: A=πr^2
Perímetro: P=2 x π x r
En primera instancia el usuario deberá escoger la opción de la cual quiere saber su respuesta (triangulo, cuadrado y circulo) o si quiere salir del programa para esto se ha creado  un menú :
*Al seleccionar la opción 1 y presionar ENTER 	el programa ejecutara la parte de triangulo 
*Al seleccionar la opción 2 y presionar ENTER 	el programa ejecutara la parte de cuadrado3                           *Al seleccionar la opción 3 y presionar ENTER 	el programa ejecutara la parte de circulo 
*Al seleccionar la opción 0 y presionar ENTER 	el programa terminara su ejecución 
Luego que entre a la parte seleccionada se le pedirán los datos correspondientes que hacen falta para el cálculo de dichas figuras 
A la vez que se terminan de introducir estas datos y presionar ENTER sale la respuesta que el usuario ha solicitado 

El programa contiene tres segmentos:
*Segmento de Datos : este es donde se declaran las variables 
*Segmento de Pila : se declara la capacidad de la pila (DB 64 DUP(?))
*Segmento de Código: se muestra todo el código del programa 
CODIGO
En este hice uso de una biblioteca importada llamada emu8086.inc
A continuación cada línea de código con su explicación correspondiente 
INICIO PROC FAR    ;inicio: nombre del proceso, proc:proceso: far:visibilidad(publica)
ASSUME DS:DATOS, CS:CODIGO, SS:PILA    ;asumir que los segmentos que creaste son los de datos, codigo y pila

PUSH DS     ;ubicar el segmento de datos en la pila
MOV AX, 0   ;mover a ax el valor 0
PUSH AX     ;ubicar ax en la pila

MOV AX, DATOS    ;mover a ax los datos
MOV DS, AX       ; mover a ds, ax
MOV ES, AX       ;mover a es, ax 

MENU:                   ;imprimir el menu
CALL CLEAR_SCREEN       ;limpia la pantalla
MOV X, 2                ;mover el valor 2 a la variable x
MOV Y, 2                ;mover el valor 2 a la variable y
GOTOXY X, Y             ;corro el cursor a las nuevas coordenadas 
CALL PTHIS              
DB "INSERTE LA OPCION DESEADA:", 0
ADD Y, 2       ;sumo 2 al valor y
GOTOXY X, Y    ;corro el cursor a la nuevas coordenada 
CALL PTHIS
DB "1-TRIANGULO", 0
INC Y        ;sumo 1 al valor y
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas 
CALL PTHIS
DB "2-CUADRADO", 0
INC Y        ;sumo 1 al valor y
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas 
CALL PTHIS
DB "3-CIRCULO", 0
INC Y        ;sumo 1 al valor y
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas 
CALL PTHIS
DB "0-SALIR", 0    ;fin del menu

MOV AX, 0      ;muevo a ax el valor 0
ADD Y, 2       ;sumo 2 al valor y
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas

CALL SCAN_NUM  ;llamo al macro escanear numero 
MOV AL, CL     ;mover a ax cl
CMP AL, 1      ;cmp es una instruccion para comparar
JE TRIANGULO   ;je es una instruccion que hace que el programa salte a la etiqueta que le pongas si la comparacion dio como resultado igual.
CMP AL, 2      ;comparo el valor almacenado em al
JE CUADRADO    ;je es una instruccion que hace que el programa salte a la etiqueta que le pongas si la comparacion dio como resultado igual.
CMP AL, 3      ;comparo el valor almacenado em al
JE CIRCULO     ;je es una instruccion que hace que el programa salte a la etiqueta que le pongas si la comparacion dio como resultado igual.
CMP AL, 0      ;comparo el valor almacenado em al
JE SALIR       ;je es una instruccion que hace que el programa salte a la etiqueta que le pongas si la comparacion dio como resultado igual.

TRIANGULO:
MOV X, 2       ;sumo 2 a la variable x
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "INTRODUZCA LA BASE:", 0
INC Y           ;sumo 1 a la variable x
GOTOXY X, Y     ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM   ;llamo al macro escanear numero 
MOV BASE, CL    ;mover a base cl
INC Y           ;sumo 1 a la variable y
GOTOXY X, Y     ;corro el cursor a la nueva coordenadas
CALL PTHIS
DB "INTRODUZCA LA ALTURA:", 0
INC Y            ;sumo 1 a la variable y
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM    ;llamo al macro escanear numero 
MOV ALTURA, CL   ;mover a altura cl 
INC Y            ;sumo 1 a la variable y
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "INTRODUZCA EL TERCER LADO:", 0
INC Y            ;sumo 1 a la variable y
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM    ;llamo al macro escanear numero
MOV LADO, CL     ;mover a lado cl
ADD Y, 2         ;sumo 2 a valor y
GOTOXY X, Y      ;corro el cursor a la nuevas coordenada
CALL PTHIS
DB "EL AREA ES:", 0
MOV AL, BASE     ;mover a al base 
MUL ALTURA       ;multiplicar altura 
MOV BL, 2        ;mover a bl 2 
MOV AREA, AL     ;mover a area al
MOV AL, AREA     ;mover a al area
DIV BL           ;dividir bl
MOV X, 14        ;sumo 14 a valor x
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL PRINT_NUM_UNS ;llamo al macro imprimir numero
MOV X, 2         ;sumar 2 a valor x
INC Y            ;sumar 1 a valor y
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas 
CALL PTHIS
DB "EL PERIMETRO ES:", 0
MOV AL, BASE     ;mover a al base 
ADD AL, ALTURA   ;sumo a al altura 
ADD AL, LADO     ;sumo a al lado
MOV PERIMETRO, AL  ;muevo a perimetro al 
MOV AX, 0         ;muevo a ax cero
MOV AL, PERIMETRO  ;muevo a al perimetro 
CALL PRINT_NUM_UNS ;llamo al macro imprimir numero 
MOV X, 22         ;sumo a valor x 22
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM
JMP MENU            ;saltar a la etiqueta menu

CUADRADO:
MOV X, 2         ;muevo a valor x 2 
GOTOXY X, Y      ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "INTRODUZCA EL LADO:", 0
INC Y          ;sumo 1 a valor y 
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM  ;llamo al macro escanear numero 
MOV LADO, CL   ;muevo a lado cl
ADD Y, 2       ;sumo al valor y 2
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "EL AREA ES:", 0
MOV AL, LADO    ;muevo a al lado 
MUL LADO        ;multipicar lado 
MOV AREA, AL    ;muevo a area al 
MOV AX, 0       ;muevo a ax 0
MOV AL, AREA    ;muevo a al area 
MOV X, 14       ;muevo al valor x 14
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas
CALL PRINT_NUM_UNS  ;llamo al macro imprimir numero
MOV X, 2        ;muevo al valor x 2 
INC Y           ;sumo 1 al valor y
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "EL PERIMETRO ES:", 0
MOV BL, 4        ;muevo a bl 4
MOV AL, LADO     ;muevo a al lado 
MUL BL           ;multiplicar bl
MOV PERIMETRO, AL  ;muevo a perimetro al 
MOV AX, 0          ;muevo a ax cero
MOV AL, PERIMETRO  ;muevo a al perimetro
CALL PRINT_NUM_UNS  ;llamo al macro imprimir numero
MOV X, 23       ;muevo al valor x 23
GOTOXY X, Y     ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM   ;llamo al macro escanear numero
JMP MENU        ;saltar a la etiqueta menu

CIRCULO:
MOV X, 2     ;mover a valor x 2
GOTOXY X, Y  ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "INTRODUZCA EL RADIO:", 0
INC Y         ;sumar 1 al valolr y
GOTOXY X, Y   ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM ;llamo al macro escanear numero
MOV RADIO, CL ;mover a radio cl
ADD Y, 2      ;sumar a valor y 2
GOTOXY X, Y   ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "EL AREA ES APROXIMADAMENTE:", 0
MOV BL, 3      ;muevo a bl 3
MOV AL, RADIO  ;muevo a al radio
MUL RADIO      ;multiplicar radio 
MUL BL         ;multiplicar bl
MOV AREA, AL   ;mover a area al 
MOV AX, 0      ;mover a ax 0
MOV AL, AREA   ;mover a al area 
MOV X, 30      ;mover al valor x 30
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL PRINT_NUM_UNS  ;llamo al macro imprimir numero
MOV X, 2       ;muevoal valor x 2
INC Y          ;muevo 1 al valor y 
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL PTHIS
DB "EL PERIMETRO ES APROXIMADAMENTE:", 0
MOV BL, 6      ;muevo a bl 6
MOV AL, RADIO  ;muevo a al radio 
MUL BL         ;multiplico bl
MOV PERIMETRO, AL  ;muevo a perimetro al
MOV AX, 0          ;muevo a ax 0
MOV AL, PERIMETRO  ;muevo a al perimetro 
CALL PRINT_NUM_UNS  ;llamo al macro imprimir numero 
MOV X, 38      ;muevo al valor x 38
GOTOXY X, Y    ;corro el cursor a la nuevas coordenadas
CALL SCAN_NUM  ;llamo al macro escanear numero
JMP MENU       ;saltar a la etiqueta menu

SALIR:

RET

INICIO ENDP  ;aqui cierra el proceso inicio

CODIGO ENDS  ;cierra el segmento codigo

DEFINE_PTHIS        ;macros
DEFINE_SCAN_NUM
DEFINE_PRINT_NUM_UNS
DEFINE_CLEAR_SCREEN

END INICIO   ;termina el programa

