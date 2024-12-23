

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
```
//PROGRAMA COMBINADOS DHT22 CON ULTRASONICO y lcd
#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT
const int Trigger = 4;   //Pin digital 4 para el Trigger del sensor
const int Echo = 2;   //Pin digital 2 para el Echo del sensor
const int DHT_PIN = 15; //pin del sensor de temperatura
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

}

void loop() {

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
 
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  //delay(2000); 
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  Serial.println("---");
  delay(2000);          //Hacemos una pausa de 200ms

  lcd.clear(); 
  lcd.setCursor(3, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(1, 1);
  lcd.print("AUTOMATIZACION");
 delay(2000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("ing.Alberto Fandino");
  lcd.setCursor(2, 1);
  lcd.print("ing Electrico");
  delay(2000);

 lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);

}
 

```

**RESULTADOS**

**DISTANCIA**


![](https://github.com/FANDINO7/DHT22-CON-ULTRASONICO-CON-LCD/blob/main/DISTANCIA.png?raw=true)



**HUMEDAD**

![](https://github.com/FANDINO7/DHT22-CON-ULTRASONICO-CON-LCD/blob/main/SENSOR%20ULTRASONICO%20CON%20DHT22%20Y%20LCD%20RESULTADO%20DE%20HUMEDAD.png?raw=true)


**realizado poR**
ALBERTO FANDIÑO 
