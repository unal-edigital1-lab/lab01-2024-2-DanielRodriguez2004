# lab01- sumador 
## Daniel Alberto Rodríguez Porras

## Informe de Laboratorio 

### Primero se analizará paso a paso el código empleado para el sumador de un bit. 
```verilog
module sum1bcc_primitive (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;


  wire a_ab;
  wire x_ab;
  wire cout_t;

  and(a_ab,A,B);
  xor(x_ab,A,B);

  xor(S,x_ab,Ci);
  and(cout_t,x_ab,Ci);

  or (Cout,cout_t,a_ab);
endmodule
```

### Para empezar se definieron las entradas y salidas, incluyendo el carry, además de los cables que se van a utilizar.

### Posteriormente, se definen las cinco compuertas lógicas, y se debe indicar cual va a ser la salida, la entrada 1, y la entrada dos, en ese orden.

```verilog
module sum1bcc (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;

  reg [1:0] st;   // REGISTRO QEU GUARDA LA SUMA 
  assign S = st[0];
  assign Cout = st[1];

  always @ ( * ) begin
  	st  = 	A+B+Ci;
  end
  
endmodule
```

### Por otro lado, en este código no se definen manualmente las compuertas, sino que se crea un registro, en la posición menos singnificativa se guarda la suma, y en la posición más significativa se guarda el carry.
### Entonces se usa el bloque always, que se define para ejecutarse siempre que alguna entrada (A,B, o Ci) cambie, suma las variables, y las reemplaza en el registro. Automáticamente Quartus define las compuertas y conexiones necesarias para llevar a cbo la tarea.

### A continuación observamos la simulación del primitive:
![image](https://github.com/user-attachments/assets/0c57791e-7302-4360-898a-753086a46ce0)

### Y por último, la simulación del bcc:

![image](https://github.com/user-attachments/assets/d45ea73f-5f1e-4d83-a8e2-71e1895c89e7)

### Como se aprecia en las simulaciones, los resultados empleando ambos métodos son identicos. Estos se consignan en la siguiente tabla de verdad:

| A | B | Cin | S | Cout |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |







