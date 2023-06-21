# PRACTICA ESP32 con DHT22 y Ultrasonico
Este repositorio muestra como podemos programar una **HC-SR04 Ultrasonic Distance Sensor** con el sensor ultrasonico, un **DHT22** para obtener temperatura y distancia y un **LCD** el cual programaremos con los valores pedidos por el docente.
## MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor **HC-SR04 Ultrasonic Distance Sensor**
- Sensor **DHT22 Digital Humidity and Temperature sensor**
- Pantalla LCD **16x2 I2C**
## INTRODUCCION
### DESCRIPCION
La (```Esp32```) la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04 Ultrasonic Distance Sensor```) para obtener el valor de distancia y un sensor (```DHT22 Digital Humidity and Temperature sensor```) para obtener el valor de temperatura y humedad; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/). 
### INSTRUCCIONES
1. Abrir la terminal de programación y colocar la siguente programación:

```
// defines pins numbers
const int Trigger = 4;
const int echoPin = 2;

// defines variables
long duration;
int distance;
int safetyDistance;
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(Trigger, OUTPUT); 
pinMode(echoPin, INPUT); 

Serial.begin(115200); 
dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
   pinMode(Trigger, OUTPUT); 
  pinMode(echoPin, INPUT);  
}


void loop() {
// Clears the trigPin
digitalWrite(Trigger, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(Trigger, HIGH);
delayMicroseconds(10);
digitalWrite(Trigger, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
  
long t; 
  long d; 

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(echoPin, HIGH); 
  d = t/59;             
  
  Serial.print("Distancia: ");
  Serial.print(d);     
  Serial.print("cm");
  Serial.println();
  delay(1000);          
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(d) +"cm");
  lcd.setCursor(0, 1);
  lcd.print(" Rodrigo Vega   ");
  delay(1000);
}

```
2.- Se buscaran las herramientas necesarias en el programa como : **HC-SR04 Ultrasonic Distance Sensor**, **DHT22 Digital Humidity and Temperature sensor** y **LCD 16x2 (I2C)** como se muestra en la imagen.
![](https://github.com/InboardDelta/DH22_ultrasonico/blob/main/elementos.png?raw=true)

3.- Realizaremos las conexiones de el sensor **HC-SR04 Ultrasonic Distance Sensor**, **DHT22 Digital Humidity and Temperature sensor** y la pantalla **LCD 16x2 (I2C)** como se muestra en la imagen.
![](https://github.com/InboardDelta/DH22_ultrasonico/blob/main/conexiones.png?raw=true)
4. Instalaremos las librerias de **LiquidCrystal I2C** y **DHT sensor library for ESPx** como se muestra en la siguente imagen.
![](https://github.com/InboardDelta/DH22_ultrasonico/blob/main/librerias.png?raw=true)

## RESULTADOS
Cuando haya funcionado, verás los valores dentro del monitor serial considerando que tendremos los valores de distancia, una segunda pantalla que ostrara los valores de temperatura y humedad como se muestran en las imagenes.
![](https://github.com/InboardDelta/DH22_ultrasonico/blob/main/distancia.png?raw=true)
![](https://github.com/InboardDelta/DH22_ultrasonico/blob/main/temperatura.png?raw=true)

# Comentarios del alumno
Esta practica nos mostro la programación, conexión y funcionamiento de los dos sensores en conjunto con una pantalla LCD para obtener el valor del los sensores y mostrarlo en la pantalla.

# Créditos

Desarrollado por RODRIGO VEGA
- [GitHub](https://github.com/InboardDelta)