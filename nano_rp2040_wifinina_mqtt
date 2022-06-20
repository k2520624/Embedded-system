#include <PDM.h>
#include <TimeLib.h>
#include <Arduino_LSM6DSOX.h>
#include <PubSubClient.h>
#include <ArduinoMqttClient.h>   // C++에서 mqtt를 수행하기 위한 libraries   github에서 다운 로드 가능
#include <WiFiNINA.h>            // mqtt를 사용하기 위해서는 rp2040 역시 wifi에 접속되어 하며 이를 위한 libraries github에서 다운 로드 가능

char ssid[] = "ncs" ;        // your network SSID (name)
char pass[] = "12312300" ;    // your network password (use for WPA, or use as key for WEP)

WiFiClient wifiClient;  // wifinina 라이브러리 폴더의 src 폴더에 있는 wificlient.h 파일내의 WifiClient 클래스의 생성자를 사용하여 하나의 wificlient 객체를 생성함
MqttClient mqttClient(wifiClient);  // 위에서 생성된 wificlient 객체를 mqttclient 클래스에서 생성되는 mqttclient() 생성자의 argument로 사용함 
                       
const char broker[] = "192.168.0.52";   // mqtt_broker가 실행되고 있는 jeston 또는 rapa 의 내부 ip address
int        port     = 1883;            // mqtt_broker의 포트
const char topic[]  = "hello";       // topic 이름
const char imu_a[] = "imu_a";
const char imu_g[] = "imu_g";
const char temperature[] = "temperature";
const char state[] = "state";
const char timer[] = "timer";
const char adc_val[] = "adc";
const char interval_t[] = "interval";
const char training[] = "training";
//const char led[] = "led";
//const char db[] = "db";

const long interval = 1000;
unsigned long previousMillis = 0;
int temperature_deg = 0;

float Ax, Ay, Az;
float Gx, Gy, Gz;
float abs_x, abs_y, abs_z;
float val;
int analogPin = A3;
int adc = 0;
bool st1 = true, st2 = true, st3 = true;
int mint, sec;
int mint2, sec2;
int count = 0;
//bool LED_SWITCH = false;
//static const char channels = 1;
//static const int frequency = 16000;
//short sampleBuffer[512];
//volatile int samplesRead;

//void onPDMdata() 
//{
//  int bytesAvailable = PDM.available();
//  PDM.read(sampleBuffer, bytesAvailable);
//  samplesRead = bytesAvailable / 2;
//}

void setup() 
{
  Serial.begin(9600);
  //pinMode(LEDB, OUTPUT);
  while (!Serial) { ; }
  
  Serial.print("Attempting to connect to WPA SSID: ");
  Serial.println(ssid);
  //PDM.onReceive(onPDMdata);
  while (WiFi.begin(ssid, pass) != WL_CONNECTED) 
  {
    Serial.print(".");
    delay(5000);
  }

  if (!mqttClient.connect(broker, port)) 
  {
    Serial.print("MQTT connection failed! Error code = ");
    Serial.println(mqttClient.connectError());

    while (1);
  }

  if (!IMU.begin()) 
  {
    Serial.println("Failed to initialize IMU!");
    while (1);
  }

//  if (!PDM.begin(channels, frequency)) 
//  {
//    Serial.println("Failed to start PDM!");
//    while (1);
//  }
  
  Serial.println("You're connected to the MQTT broker!");
  Serial.println();
}

void loop() 
{
  mqttClient.poll();
  unsigned long currentMillis = millis();

  adc = analogRead(analogPin);
  mqttClient.beginMessage(adc_val);  
  mqttClient.print(adc);
  mqttClient.endMessage();
  
  if (IMU.accelerationAvailable()) 
  {
    IMU.readAcceleration(Ax, Ay, Az);
    abs_x = abs(Ax);
    abs_y = abs(Ay);
    abs_z = abs(Az);
    val = abs_x + abs_y + abs_z;
    clock_t start2;
    if(count == 0)
    {
      start2 = clock(); 
    }
    count++;
    if(val < 1.1)
    {
      st2 = true;
      st3 = true;
      clock_t start;
      if(st1)
      {
        start = clock();
      }
      mqttClient.beginMessage(state);
      mqttClient.print("휴식");
      mqttClient.endMessage();
      mqttClient.beginMessage(interval_t);
      mqttClient.print(0);
      mqttClient.endMessage();
      clock_t end = clock();
      int time = end - start;
      Serial.println(end);
      Serial.println();
      Serial.println(start);
      Serial.println();
      Serial.println();
      //Serial.println(start);
      time = time / 100;
      mint = time / 60;
      sec = time % 60;
      mqttClient.beginMessage(timer);
      mqttClient.print(mint);
      mqttClient.print("분");
      mqttClient.print(" ");
      mqttClient.print(sec);
      mqttClient.print("초");
      mqttClient.endMessage();
      st1 = false;
    }
    else if( val < 2.5)
    {
      st1 = true;
      st3 = true;
      clock_t start;
      if(st2)
      {
        start = clock();
      }
      mqttClient.beginMessage(state);
      mqttClient.print("걷기");
      mqttClient.endMessage();
      mqttClient.beginMessage(interval_t);
      mqttClient.print(1);
      mqttClient.endMessage();
      clock_t end = clock();
      int time = end - start;
      time = time / 100;
      mint = time / 60;
      sec = time % 60;
      mqttClient.beginMessage(timer);
      mqttClient.print(mint);
      mqttClient.print("분");
      mqttClient.print(" ");
      mqttClient.print(sec);
      mqttClient.print("초");
      mqttClient.endMessage();
      st2 = false;
    }
    else
    {
      st1 = true;
      st2 = true;
      clock_t start;
      if(st3)
      {
        start = clock();
      }
      mqttClient.beginMessage(state);
      mqttClient.print("뛰기");
      mqttClient.endMessage();
      mqttClient.beginMessage(interval_t);
      mqttClient.print(2);
      mqttClient.endMessage();
      clock_t end = clock();
      int time = end - start;
      time = time / 100;
      mint = time / 60;
      sec = time % 60;
      mqttClient.beginMessage(timer);
      mqttClient.print(mint);
      mqttClient.print("분");
      mqttClient.print(" ");
      mqttClient.print(sec);
      mqttClient.print("초");
      mqttClient.endMessage();
      st3 = false;
    }
    mqttClient.beginMessage(imu_a);
    mqttClient.print(Ax);
    mqttClient.print(" ");
    mqttClient.print(Ay);
    mqttClient.print(" ");
    mqttClient.print(Az);
    mqttClient.endMessage();
    clock_t end2 = clock();
    int time2 = end2 - start2;
    time2 = time2 / 100;
    mint2 = time2 / 60;
    sec2 = time2 % 60;
    mqttClient.beginMessage(training);
    mqttClient.print(mint2);
    mqttClient.print("분");
    mqttClient.print(" ");
    mqttClient.print(sec2);
    mqttClient.print("초");
    mqttClient.endMessage();
  }

  if (IMU.gyroscopeAvailable()) 
  {
    IMU.readGyroscope(Gx, Gy, Gz);
    mqttClient.beginMessage(imu_g);
    mqttClient.print(Gx);
    mqttClient.print(" ");
    mqttClient.print(Gy);
    mqttClient.print(" ");
    mqttClient.print(Gz);
    mqttClient.endMessage();
  }

  if (IMU.temperatureAvailable())
  {
    IMU.readTemperature(temperature_deg);
    mqttClient.beginMessage(temperature);
    mqttClient.print(temperature_deg);
    mqttClient.endMessage();
  }

//  if (samplesRead) 
//  {
//    for (int i = 0; i < samplesRead; i++) 
//    {
//      if (channels == 2) 
//      {
//        Serial.print("L:");
//        Serial.print(sampleBuffer[i]);
//        Serial.print(" R:");
//        i++;
//      }
//      Serial.println(sampleBuffer[i]);
//
//      if (sampleBuffer[i] > 10000 || sampleBuffer[i] <= -10000) 
//      {
//        LED_SWITCH = !LED_SWITCH;
//        if (LED_SWITCH) 
//        {
//          digitalWrite(LEDB, HIGH);
//          mqttClient.beginMessage(led);
//          mqttClient.print("ON!");
//          mqttClient.endMessage();
//          delay(1000);
//        }
//        else 
//        {
//          Serial.println();
//          Serial.println("OFF!");
//          Serial.println();
//          delay(1000);
//        }
//      }
//    }
//  }
  delay(1000);
}

