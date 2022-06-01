César Roldan Moros
*Grup 13*
# PRÁCTICA 8: Buses de comunicación IV. uart
___
#### Objetivo 
El objetivo es comprender el funcionamiento de la comunicación serie asíncrona.
___
#### Preguntas teóricas
###### Descripción diferentes métodos de comunicación
  
- **RS232**
  Recommended Standard-232 se utiliza para la transmisión de datos por la comunicación en serie. Define las señales que se conectan entre un DTE (Equi terminal de datos), y un DCE (Equipo de comunicación de datos). Este estándar define las características eléctricas y la sincronización de las señales, el significado de las señales y los Pinouts de los connectores. En comparación con interfaces como la RS422 o la RS485, la 232 tiene menor velocidad de transmisión, menor longitud máxima de cable, mayor oscilación de voltaje, conectores estándar mayores y capacidad multipunto limitada. Actualmente, pocas computadoras vienen con este estándar.
- **RS485**
  Recommended Standard-485 es un estándar que define las características eléctricas de controladores y receptores para su uso en sistemas de comunicaciones en serie. Estos estándares sí admite sistemas múltiples, y es eficaz a largas distancias en entornos eléctricamente ruidosos. Es útil en sistema de control industrial.
- **RS422**
  Recommended Standard-422 es un estándar que especifica las características eléctricas de un circuito de señalización digital. Ofrece una mayor velocidad y longitus más largas que la 232. Este estándar especifica la señalización diferencial.
###### Descripción funciones principales Arduino
- **if(Serial)**
  Busca una condición y ejecute la siguiente declaración o conjunto de declaraciones si la condición es cierta.
  *Ejemplo:*
  ```
  if (x > 120) {
  digitalWrite(LEDpin1, HIGH);
  digitalWrite(LEDpin2, HIGH);
  }
  ```
- **available()**
 Obtiene los bytes almacenados del puerto serie que están disponibles para su lectura.
  *Ejemplo:*
  ```
  if(Serial.available( ) > 0) {  
    Serial.print("data byte received:");
  }
  ```
- **availableForWrite()**
 Obtiene el número de bytes disponibles para escribir en el buffer en serie sin bloquear la operación de escritura.
  *Ejemplo:*
  ```
  String myString = "Hello\n";
  if (Serial.availableForWrite() > myString.length()) {
    Serial.print(myString);
    delay(1000);
  }
  ```
- **begin()**
  Establece la velocidad de datos en bits por segundos (bauds) por la transmisión de datos en serie.
   *Ejemplo:*
  ```
  Serial.begin(115200)
  ``` 
- **end()**
  Desactiva la comunicación serie, lo que permite que los pines RX y TX se utilicen para la entrada y salida general.
  *Ejemplo:*
  ```
  Serial.end()
  ``` 
- **find()**
  Lee los datos del buffer en serie hasta encontrar el objetivo. La función devuelve *true* si encuentra el objetivo, *false* si se termina el tiempo de espera.
   *Ejemplo:*
  ```
  if(Serial.available()>0){
    boolean b= Serial.find("aa");
    if(b)
      Serial.println("found");}}
  ``` 
- **findUntil()**
  Lee los datos del buffer en serie hasta encontrar una cadena de destino de longitud determinada o una cadena de terminación.
  *Ejemplo:*
  ```
  if(Serial.available()){
    if(Serial.findUntil("on","$")){
      digitalWrite(13,HIGH);}}
  ```
- **parseFloat()**
  Vuelve el primer número de punto flotante del buffer. Termina con el primer carácter que no es un número de coma flotante.
  *Ejemplo:*
  ```
  if (Serial.available()){
    float num = Serial.parseFloat();
    Serial.println(num, 2);}
  ```
- **parseInt()**
  Busca el siguiente entero válido en la serie entrante.
  *Ejemplo:*
  ```
  if (Serial.available()){
    y = Serial.parseInt();
    Serial.print(y);} 
  ```
- **peek()**
  Devuelve el siguiente byte de los datos del serial entrante sin eliminarlo del buffer interno.
  *Ejemplo:*
  ```
  if (Serial.available()){
    byte car = Serial.peek();
    Serial.write(car)
    Serial.println(car);}
  ```
- **print()**
  Imprime datos en el puerto serie como texto ASCII legible por humanos.
  *Ejemplo:*
  ```
  Serial.print("Hello world.")
  ```
- **println()**
  Imprimir datos en el puerto serie como texto ASCII legible por humanos seguido de un carácter de retorno de carro y un carácter de salto de línea,
  *Ejemplo:*
  ```
  Serial.println("Hola món")
  ```
- **read()**
  Lee o captura un byte (un carácter) desde el puerto serie.
  *Ejemplo:*
  ```
  if (Serial.available()){
    char car = Serial.read();
    Serial.println(car);}
  ```
- **readBytes()**
  Lee caracteres desde el buffer del puerto serie, hacia el especificado.
  *Ejemplo:*
  ```
  if (Serial.available() > 2){
    Serial.readBytes(ref, 2);
    Serial.println(ref[0]);
    Serial.println(ref[1]);}
  ```
- **readBytesUntil()**
  Lee caracteres desde el buffer del puerto serie, hacia el especificado. La función termina si la longitud determinada se ha leído, se ha encontrado el carácter terminador o el tiempo de espera ha terminado.
  *Ejemplo:*
  ```
  if (Serial.available()) {
    buffer[Serial.readBytesUntil('\r', buffer, sizeof(buffer) - 1)] = 0; 
    Serial.read(); 
    Serial.print(F("Linea de texto leida: \""));
    Serial.print(buffer);
    Serial.println('\"');}
  ```
- **readString()**
  Lee caracteres y los coloca en un String.
  *Ejemplo:*
  ```
  if (Serial.available()) {
      Serial.print("Mensaje recuperado: \"");
      Serial.print(Serial.readString());
      Serial.println('\"');}
  ```
- **readStringUntil()**
  Lee caracteres y los coloca en un String. La función termina si se ha encontrado el carácter o se ha terminado el tiempo de espera.
  *Ejemplo:*
  ```
  if (Serial.available()) {
   Serial.print(F("Linea de texto leida: \""));
   Serial.print(Serial.readStringUntil('\r')); 
   Serial.println('\"');
   Serial.read();}
  ```
- **setTimeout()**
  Establece los milisegundos máximos para esperar datos en serie al utilizar las funciones Serial.readBytes()* o Serial.readBytesUntil()*.
  *Ejemplo:*
  ```
  if (Serial.available()){
    byte c = Serial.read();
    Serial.println(c);}
  ```  
- **write()**
  Envía datos binarios al puerto serie. Esta información se envía como un byte o una serie de bytes.
  *Ejemplo:*
  ```
  Serial.write(65);            //A
  Serial.write("65");          //65
  Serial.write("Hola mundo");  //Hola mundo
  ```
- **serialEvent()**
  Se cruda cada vez que se recibe un dato en el pin RX, se ejecuta después de colocarlo en el buffer de entrada. Se utiliza *Serial.read()* para capturar aquellos datos.
  *Ejemplo:*
  ```
  void serialEvent() {
    while (Serial.available()) {
      char inChar = (char)Serial.read();
      inputString += inChar;
      if (inChar == '\n') {
        stringComplete = true;}}
  }
  ```
_____
### Ejercicio. Bucle de comunicación uart2
##### Codigo
```
#include <Arduino.h>
#define RXD2 16
#define TXD2 17
void setup()
{
  Serial.begin(115200);
  Serial2.begin(9600, SERIAL_8N1, RXD2, TXD2);
  Serial.println("Serial Txd is on pin: "+String(TX));
  Serial.println("Serial Rxd is on pin: "+String(RX));
}
void loop()
{
  while (Serial2.available()) 
  {
    Serial.print(char(Serial2.read()));
  }
  while (Serial.available())
  {
    Serial2.print(char(Serial.read()));
  }
}
```
##### Funcionamiento
Realizaremos un bucle de comunicación de forma que los datos que se envíen por el terminal rxd0 se dirijan a la uart2 tdx2 y la recepción de los datos de la uart2 se revien de nuevo a la salida txd0 para que aparezca en la pantalla del terminal

En el código, primero definimos los dos pines, el RXD2 (receptor) y el TXD2 (emisor)
En el void setup() inicializamos la velocidad de transmisión de los bits a 115200. Inicializamos otro Serial(2), el SERIAL_8N1 que le decimos que tiene 8 bits y los pinos que utilizaremos, el RXD2 y TXD2
Imprimimos por pantalla en qué pin está cada Serial
En el void loop() hacemos un while que comprueba que Serial2 esté disponible. Mientras que esté disponible, que haga un pront de lo que lee y lo envíe a otro puerto y lo que le llegue al Serial puerto que lo envíe al monitor.