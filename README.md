# Arquitectura TOY-8

Nombre: Juan Cruz Gimenez

## Instrucciones

- Forkear este repo
- Completar nombre y apellido
- Responder editando este mismo archivo
- Pushear a GitHub y pasarme el link de su fork (el repo tiene que ser público)


Tienen un emulador de la computadora y el circuito para el Logisim en el [blog](https://la35.net/orga/emulador.html). Usenlos sabiamente para responder.

**Tip:** si editan en el Atom tienen un _preview_ de Markdown tocando `Ctrl + Shift + M` mientras editan este archivo.
## Ejercicios

1. Considerar el siguiente programa de TOY-8 en lenguaje máquina. Traducir a hexadecimal en la tercer columna y a ensamblador en la cuarta como se muestra en la primera línea. ¿Cuál es el valor de 0xE cuando el programa se detiene? ¿Qué es lo que hace este programa si 0xE es el resultado del mismo?

```

0x1:  10101011    #  AB  #  lw B
0x2:  11101010    #  EA  #  bze A
0x3:  00101101    #  2D  #  add D
0x4:  11001011    #  CB  #  sw B
0x5:  10101110    #  AE  #  lw E
0x6:  00101100    #  2C  #  add C
0x7:  11001110    #  CE  #  sw E
0x8:  10100000    #  A0  #  lw 0
0x9:  11100001    #  E1  #  bze 1
0xA:  00000000    #  00  #  halt
0xB:  00000011    #  03  #   
0xC:  00000110    #  06  #   
0xD:  11111111    #  FF  #  
0xE:  00000000    #  00  #

```




``Si este mismo deja de funcionar su valor de la direccion de la memoria 0xE es producto de los numeros que esten presentes en 0xB y 0xC ``

2. Consideren el siguiente _hexdump_ de la memoria de TOY-8. O sea un volcado de la memoria en hexadecimal. ¿Cuántos programas distintos pueden encontrar? Indicar cuáles bytes interpretan como instrucciones y cuáles como datos.



```


0x0   00 A5 26 C7
0x4   00 08 05 00
0x8   A7 6D 2E C7
0xc   00 FF 01 00


```


``Esta memoria funcionan dos tipos de programas diferentes entre si, las intrucciones del primer programa, pertencen a  bytes de 0x1,0x2,0x3,0x4 siendo asi estos los datos de 0x5,0x6,0x7.Despues se encuentra otro programa con determinadas instrucciones en 0x8,0x9,0xA,0xB y 0xC,y datos 0x7, 0xD y 0xE.``



3. Para el primer programa del ejercicio anterior. ¿Qué líneas de control se activan para cada instrucción? ¿Cuál es el valor del bus de datos y de instrucciones en cada instrucción? Completen la siguiente tabla, agreguen las filas que sean necesarias.


|Instrucción|Reloj|Control|Data bus|Address Bus|
|---|---|--------------|---|---|
|A5 |0  |IR en         |A5 |1  |
|A5 |1  |R en, addr mux|08 |5  |
|26 |0  |IR en         |26 |2  |
|26 |1  |R en, addr mux|05 |6  |
|c7 |0  |IR en         |c7 |3  |
|c7 |1  |R en, addr mux|0D |7  |
|00 |0  |Ir en         |0  |4  |
|00 |1  |R en, addr mux|0  |0  |  


4. El siguiente programa suma los números que encuentra en la entrada hasta que aparece un cero, y luego envía el resultado a la salida. Traducirlo a ensamblador y a C siguiendo el ejemplo de las primeras dos líneas.

```


0x1:  A0   #  lw  0  #  int r = dir_0 ;
0x2:  CE   #  sw  E  #  int dir_e = r ;
0x3:  AF   #  lw  F  #  r = dir_f ;
0x4:  E9   #  bze 9  #  if (r == 0) r = dir_e ;
0x5:  2E   #  add E  #  r = r + dir_e ;
0x6:  CE   #  sw  E  #  dir_e = r ;
0x7:  A0   #  lw  0  #  r = dir_0 ;
0x8:  E3   #  bze 3  #  if (r == 0) r = dir_f ;
0x9:  AE   #  lw  E  #  r = dir_e ;
0xA:  CF   #  sw  F  #  dir_f = r ;  
0xB:  00   #  halt   #  exit(-1) ;


```

5. Una mejora que le podríamos hacer a esta computadora es duplicar la cantidad de memoria, pasar de 16 bytes a 32 bytes. ¿Cómo lo harían manteniendo la longitud de las instrucciones en 8 bits? ¿Qué partes de la CPU habría que modificar y cómo?


```
El duplicar la cantidad total de memoria de una computadora, se podria realizar agregando otra memoria de 16 bytes. Asi lograriamos una para almacenar instrucciones que se ejecutan por la CPU y la otra para almacenar datos o numeros que mas tarde se utilizaran para operaciones.
Si se quiere lograr esto se necesitara de al menos: Un demultiplexor que su entrada sea el RAM str de la Unidad de Control y las salidas sean las dos memorias,el demultiplexor entre el multiplexor del bus de direcciones y ambas memorias,el multiplexor debe tener como entrada a ambas memorias y su salida al bus de datos
para asi poder lograr, una memoria que sea capaz de leer y guardar datos en si misma, poder elegir la memoria que se utilize  en el momento preciso del ciclo de una instrución,selecionar que una memoria se lean los datos o instrucciones.Es necesario sincronizar el circuito para que se lea una instrucción en una de las memorias ademas que para que se tomen o escriban datos en la otra memoria.La forma de resolver esto es a traves de la conexion de los controles de los demultiplexores y multiplexores a la salida de la Unidad de Control Addr mux.

```
