# ProyectoFinalArqui
Inicio:	    
	    MOV ACC, VAR_A      ;Vamos al ACC y almacenamos VAR_A que es diferente al registro A
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos VAR_A
            MOV ACC, 0x00       ;Cargamos una constante
            MOV [DPTR], ACC     ;Vamos al VAR_A inicializada en 0000 0000
Inicializar_Count:
            MOV ACC, Count      ;Vamos al ACC y almacenamos Count n-bits
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos Count
            MOV ACC, 0b00001000 ;Vamos al ACC y almacenamos 0000 1000 (8 en decimal)
            MOV [DPTR], ACC     ;Vamos al Count y almacenamos 0000 1000
Inicializar_Q-1:
            MOV ACC, Q-1        ;Vamos al ACC y almacenamos Q-1
            MOV DPTR, ACC       ;Vamos al DPTR y movemos Q-1
            MOV ACC, 0x00       ;Vamos al ACC y almacenamos 0000 0000
            MOV [DPTR], ACC     ;Vamos al Q-1 y almacenamos 0000 0000
 Calcular_Q0:         
            MOV ACC, Q    	;Vamos al ACC y almacenamos Q
            MOV DPTR, ACC       ;Vamos al DPTR y movemos Q
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos el valor que contiene el apuntados
	    MOV A, ACC		;Vamos al registro A y almacenamos el valor del acumulador
            MOV ACC, 0b00000001 ;Vamos al ACC y almacenamos el numero 0000 0001 
            AND ACC, A          ;Vamos al ACC y calculamos AND de 0000 0001 con el valor de Q
            MOV A, ACC          ;Vamos al A y almacenamos ACC              
Guardar_Q0:
            MOV ACC, Q0     	 ;Vamos al ACC y almacenamos Q0
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos Q0
            MOV ACC, A          ;Vamos al ACC y almacenamos el valor del registro A
            MOV [DPTR], ACC     ;Vamos a Q0 y almacenamos el valor del acumulador
Preguntar_Q-1=0: 
	    MOV ACC, Q0		  	;Vamos al ACC y almacenamos Q0
	    MOV DPTR, ACC	    ;Vamos al DPTR y almacenamos el valor que contiene el ACC
  	    MOV ACC, [DPTR]	 	;Vamos al ACC y almacenamos el valor que contiene el apuntador
	    MOV A, ACC		  	;Vamos al registro A y almacenamos el valor que contien el acumulador
            MOV ACC, Q-1	    ;Vamos al ACC y almacenamos Q-1  
            MOV DPTR, ACC     ;Vamos al DPTR y almacenamos Q-1
            MOV ACC, [DPTR]   ;Vamos al ACC y almacenamos 0000 0000 
            MOV DPTR, ACC     ;Se mueve la variable al registro A para la bandera
            JZ Preguntar_0-	  ;Saltamos a la instruccion que pregunta por 0  
Preguntar_-1:
            MOV ACC, A        ;Vamos al ACC y almacenamos el valor del registro A 
            JZ Hacer_01       ;Saltamos a la instruccion que opera por el 01
Preguntar_0-:
            MOV ACC, A        ;Vamos al ACC y almacenamos el valor del registro A
            JZ DesplazarAritmetico ;Saltamos a la instruccion que desplaza por aritmetica
	    MOV ACC, [DPTR]	  ;Vamos al ACC y almacenamos la dirección de memoria del DPTR
	    JZ Hacer_10		  	;Saltamos a la instruccion que para hacer el caso 10
Hacer_11:
            JMP DesplazarAritmetico ;Saltamos a la instruccion que desplaza por aritmetica
Hacer_10:
            MOV ACC, M          ;Vamos a ACC y almacenamos M
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos M
            MOV ACC, [DPTR]     ;Vamos al ACC y se almacena el valor que contiene el apuntador
	    INV ACC		      	  ;Invertimos M
	    MOV A, ACC		  	  ;Movemos el acumulador al registro A
	    MOV ACC, 0b00000001 ;Cargamos una constante 1
	    ADD ACC, A		  	  ;Hacemos complemente A2  de M
            MOV A, ACC          ;Vamos a almacenar - M en el registro A
            MOV ACC, VAR_A      ;Vamos al ACC y almacenamos VAR_A
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos VAR_A
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos 0000 0000
            ADD ACC, A          ;Sumamos A y -M 
            MOV [DPTR], ACC     ;Vamos a A y almacenamos A-M
            JMP DesplazarAritmetico ;Saltamos a la instruccion que desplaza por aritmetica
Hacer_01:
            MOV ACC, M          ;Vamos a ACC y almacenamos M
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos M
            MOV ACC, [DPTR]     ;Vamos a ACC y almacenamos 0000 0011
            MOV A, ACC          ;Vamos al R y almacenamos 0000 0011
            MOV ACC, VAR_A	  	;Vamos al ACC y almacenamos VAR_A            
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos VAR_A
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos 0000 00000
            ADD ACC, A          ;Sumamos 0000 0000 con 0000 0011
            MOV [DPTR], ACC     ;Vamos a VAR_A y almacenamos 0000 0011

DesplazarAritmetico:
            MOV ACC, Q0         ;Vamos al ACC y almacenamos Q0
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos Q0
            MOV ACC, [DPTR]     ;Vamos al ACC y el valor que contiene el apuntador
            MOV A, ACC          ;Vamos al registro A y almacenamos el valor del acumulador
            MOV ACC, Q-1        ;Vamos al ACC y almacenamos Q-1
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos Q-1
            MOV ACC, A          ;Vamos al ACC y almacenamos el valor del registro A
            MOV [DPTR], ACC     ;Vamos a Q-1 y almacenamos el valor del acumulador
Obtener_VAR_A0:
            MOV ACC, VAR_A      ;Vamos al ACC y almacenamos VAR_A
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos VAR_A
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos el valor que contiene el apuntador
            MOV A, ACC          ;Vamos al registro A y almacenamos el valor del acumulador
            MOV ACC, 0b00000001 ;Vamos al ACC y almacenamos una constante 
            AND ACC, A          ;Calculamos AND entre los valores del registro A y el acumulador
            MOV A, ACC          ;Vamos al registro A y almacenamos el valor que contiene el acumulador
            JZ DesplazarDerecha_Q ;Se hace la verificación y saltamos a la instruccion que desplaza Q
            MOV ACC, 0b10000000 ;Vamos al ACC y almacenamos una constante
            MOV A, ACC          ;Vamos al registro A y almacenamos el valor del acumulador
DesplazarDerecha_Q:
            MOV ACC, Q          ;Vamos al ACC y almacenamos Q
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos Q
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos el valor que contiene el apuntador
            RSH ACC, 0x1        ;Desplazamos un bit a la derecha 
            ADD ACC, A          ;Sumamos los valores que contienen el registro A y el acumulador
            MOV [DPTR], ACC     ;Vamos a Q y almacenamos el valor que contiene el acumulador
Empezar_A:
            MOV ACC, VAR_A      ;Vamos al ACC y almacenamos VAR_A
            MOV DPTR, ACC       ;Vamos al DPTR y almacenamos VAR_A
            MOV ACC, [DPTR]     ;Vamos al ACC y almacenamos el valor que contiene el apuntador
            MOV A, ACC          ;Vamos al A y almacenamos el valor del acumulador
            MOV ACC, 0b10000000 ;Vamos al ACC y almacenamos una constante para conservar el bit más significativo
            AND ACC, A          ;Calculamos AND entre el valor del acumulador y el registro A
            MOV A, ACC          ;Vamos al A y almacenamos el valor del acumulador
	    MOV ACC, [DPTR]	    ;Vamos al ACC y almacenamos el valor del DPTR 
Desplazar_A:
            RSH ACC, 0x1        ;Desplazamos un bit a la derecha 
            ADD ACC, A          ;Sumamos el valor que contiene el acumulador y el registro A
            MOV [DPTR], ACC     ;Vamos a VAR_A y almacenamos el valor del acumulador
Cargamos_Count: 
	    MOV ACC, Count 	    ;Vamos al ACC y almacenamos la variable Count
	    MOV DPTR, ACC	      ;Vamos al apuntador y almacenamos la direacción de memoria del acumulador
	    MOV ACC, [DPTR]	    ;Vamos al acumulador y almacenamos el valor que contiene el apuntador
	    MOV A, ACC		      ;Vamos al registro A y almacenamos el valor del acumulador
	    MOV ACC, 0b11111111	;Vamos al acumulador y cargamos una constante
            ADD ACC, A		      ;Sumamos Count y -1 
Guardar_Count:
            MOV [DPTR], ACC     ;Vamos a Count y almacenamos el valor del acumulador
            JZ Terminar_Algoritmo ;Verificación de 0 y saltamos a la instruccion que guarda los resultados
            JMP Calcular_Q0	    ;Saltamos a la instruccion que calcula Q0 para el ciclo
Terminar_Algoritmo:
            HLT				          ;Terminación del programa
Inicialización de las variables: 
VAR_A	: 0b0 
Q: 0b10000000; Multiplicador
Q-1: 0b0
M: 0b00001000; Multiplicando
Count: 0x8
Q0: 0b0

;Rúbrica de instrucciones adicionales del PDUA:

;OPCODE: 	NEMÓNICO:	Bytes: 
; 01000xxx	AND ACC, A 	1
; 1xxxxxxx	SHR ACC		1
