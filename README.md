# Reporte-4-ultrasonico
## Introduccion 
### En esta practica procedimos a realizar unas mediciones de distancia apoyandonos de un sensor ultrasonico junto con una LCD (Liquid Crystal Display) con el que podemos monitorear las variciones que nos arroja el codigo de la simulacion.
## Equipo y materiales
- LCD (Liquid Crystal Display)
- Sensor Ultrasonico
- Esp 22
## Procedimiento
### 1. Entrar y abrir la plataforma Wokwi donde seleccionaremos la siguiente tarjeta de adquisicion ```ESP 22```
![](https://github.com/raul7ops-sketch/Reporte-3-Pantalla-LCD/blob/main/Reporte%201%20esp%2022.png?raw=true)
### 2. Una vez ahi agregaremos la libreria correspondiente para el funcionamiento de nuestra practica:
- LiquidCrystal I2C
### 3. Seleccionaremos el sensor ultrasonico
![](https://github.com/raul7ops-sketch/Reporte-4-ultrasonico/blob/main/Reporte%204%20ultrasonico.png?raw=true)
### 4. Utilizamos la LCD 16x2 
![](https://github.com/raul7ops-sketch/Reporte-4-ultrasonico/blob/main/lcd%20reporte%204.png?raw=true)
### 5. Realizamos las siguientes conexiones:
![](https://github.com/raul7ops-sketch/Reporte-4-ultrasonico/blob/main/Conexion%20reporte%204.png?raw=true)
### 6. Copiamos el siguiente codigo a nuestro simulador
``` #include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
   lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);     
  
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("modulo 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Distancia: ");
  lcd.print(d);      //Enviamos serialmente el valor de la distancia
  lcd.setCursor(14, 1);
  lcd.print("cm");
  lcd.println();
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Raul Aguilar L.");
  lcd.setCursor(2, 1);
  lcd.print("Ing. Mecanico");
  delay(1000);     
       //Hacemos una pausa de 100ms
}
```
### 7. Corremos la simulacion para analizar los resultados
## Conclusion
En la practica se realizo la programacion, conexion y revision de datos mediante una ```LCD``` el cual nos arrojaba el valor dado por el ```sensor ultrasonico``` que nos arroajaba en unidades de centimetros la distancia que dectecaba que para la practica fueron 60 cm. Ademas de arreglar la ```LCD``` para arrojar otras oraciones intermitentes.
![](https://github.com/raul7ops-sketch/Reporte-4-ultrasonico/blob/main/Conclision%20reporte%204.png?raw=true)

##Creditos
Este reporte fue realizado por Raul Aguilar Lagunas. https://github.com/raul7ops-sketch

