# DHT 22 Ultrasónico con pantalla LCD
## Descripción
### En este repositorio se muestra como  podemos programar la pantalla LCD con lo anteriormente programado con el ESP32, un Ultrasonic Distance Sensor, un sensor dht 22 para temperatura y humedad y una pantalla LCD, se actualiza cada 2 segundos, y se tienen que agregar la librería de la pantalla de liquid crystal y la librería del DHT22 y también en el código se tiene que iniciar la pantalla. 
## Material Necesario
- wokwi
- ESP32
- Ultrasonic Distance Sensor
- DHT22
- lcd1602
## Programación
```
const int Trigger = 4;   //Pin digital 4 para el Trigger del sensor
const int Echo = 2;   //Pin digital 2 para el Echo del sensor

#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT

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

  long t; 
  long d; 

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); 
  d = t/59;            
 
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
  lcd.setCursor(2,0);
  lcd.print("Diplomado V");
  lcd. setCursor(2,1);
  lcd.print("Mecatronica");
  delay(2000);
  

   lcd.clear();
  lcd.setCursor(1,0);
  lcd.print("Guillermo Hdz");
  lcd. setCursor(2,1);
  lcd.print("Ing Mecanica");
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
## Librerías

1. LiquidCrystal I2C
2. DHT22

## Conexión

![image](https://github.com/user-attachments/assets/8b07572b-754d-4e2b-915e-e9ab2889dd8f)



##Instrucciones de operación 

1. Iniciar Simulador
2. Visualizar los datos en la pantalla LCD
3. Subir y Bajar la distancia dando doble click al sensor ultrasonico o al dht 22 

## Resultados

Cuando funcione y Corra los valores serán mostrados en la pantalla LCD, cada 2 segundos se actualizará, mostrará primero el número del modulo, el nombre del diplomado. Luego mostrará mi nombre y mi carrera, y finalmente mostrará la distancia y la humedad/temperatura.

![image](https://github.com/user-attachments/assets/57210466-ecc9-4ceb-98ff-6e9e901a34e1)
![image](https://github.com/user-attachments/assets/0a48703c-a429-4d08-9c80-ddf4761be812)
![image](https://github.com/user-attachments/assets/6c4b8f89-892a-4be4-8d8f-0159146c56a4)

## Desarrollado por

Guillermo de Jesús Hernández Yáñez
[GitHub](https://github.com/inward182)
