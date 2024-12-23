

# PRACTICA-DHT22-CON-ULTRASONICO-CON-LCD
**INTRODUCCION**

Se realizara una medición con un sensor ULTRASONICO y DHT 22 donde se mostrara la distancia, temperatura y humedad en una pantalla LCD La Esp32 es una tarjeta de adquisición de datos, paralo cual en esta practica ocuparemos un sensor (DTH11) con una pantalla LCD216 para adquirir datos de temperatura y humedad del entorno cada segundo y mostrarlar los datos en la panatlla, se usara un simulador llamado WOKWI.

**MATERIAL A UTILIZAR**
WOKWI
TARJET ESP32
SENSOR ULTRASONICO
LCD 16X2 2IC
INSTRUCCIONES
Insertar el codigo dado de la practica, se realizara la misma actividad que la practica anterior mostrando datos de quien esta programando
```const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
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
  delay(1000);          //Hacemos una pausa de 100ms

lcd.clear();
  lcd.setCursor(2,0);
  lcd.print("Diplomado V");
  lcd. setCursor(2,1);
  lcd.print("Mecatronica");
  delay(2000);
  

   lcd.clear();
  lcd.setCursor(1,0);
  lcd.print("ing.Alberto Fandino");
  lcd. setCursor(2,1);
  lcd.print("Ing Electrica");
  delay(2000);

  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia " + String(d) + " cm");
  delay(2000);
}

```

**RESULTADOS**

**DISTANCIA**


![](https://github.com/FANDINO7/DHT22-CON-ULTRASONICO-CON-LCD/blob/main/DISTANCIA.png?raw=true)



**HUMEDAD**

![]()
