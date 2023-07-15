# Esp32-Punto-De-Acceso-Con-Modo-Estacion
Sirve para crear un punto de acceso y luego conectarse a una red

### Codigo
```c++
#include <WiFi.h>

//Credenciales WiFi de la red a conectar
const char* wifi_network_ssid = "Wifi";
const char* wifi_network_password = "password";

//Credenciales para crear una red WiFi
const char *soft_ap_ssid = "ESP32";
const char *soft_ap_password = "123456789";
void setup()
{
  //Inicia el puerto serial
  Serial.begin(115200);

  //Configura como access point y modo estacion
  WiFi.mode(WIFI_AP_STA);

  //Imprime en el puerto serial
  Serial.println("\n[*] Creating ESP32 AP");

  //Crea una red Wifi
  WiFi.softAP(soft_ap_ssid, soft_ap_password);

  Serial.print("[+] AP Created with IP Gateway ");

  //Imprime en el puerto serial la direccion ip
  Serial.println(WiFi.softAPIP());

  //Se conecta a una red WiFi
  WiFi.begin(wifi_network_ssid, wifi_network_password);

  //Es un bucle infinito en caso que no se conecte a una red
  Serial.println("\n[*] Connecting to WiFi Network");
  while (WiFi.status() != WL_CONNECTED)
  {
    Serial.print(".");
    delay(100);
  }

  //Imprime la direccion IP de la red que se conecta
  Serial.print("\n[+] Connected to WiFi network with local IP : ");
  Serial.println(WiFi.localIP());
}
void loop()
{

}
```
