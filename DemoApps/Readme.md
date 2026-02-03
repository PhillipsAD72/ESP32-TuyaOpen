## Upravené vzorové příklady od TuyaOpen
[Originální příklady od TuyaOpen](https://github.com/tuya/arduino-TuyaOpen/tree/main/libraries/TuyaIoT/examples)

Úpravy kódu spočívají především v tom, že MCU ESP32, který předpokládá TuyaOpen, má LED_BUILDIN a BUTTON_BUILDIN připojené k jiným GPIO, než mnou použitá vývojová deska [Devkit V1](https://lastminuteengineers.com/esp32-pinout-reference/).

![ESP32devkitV1](https://lastminuteengineers.com/wp-content/uploads/iot/ESP32-Pinout.png)

TuyaOpen má jako LED_BUILDIN definován pin33 a jako BUTTON_BUILDIN pin35, ale na mé desce by to měly být GPIO2 a GPIO0 (viz soubor pins_arduino.h). Opravdu nějak nechápu, jaký hardware je takto zapojený, ale uznávám, že v tom zas tak velký přehled nemám.

V jednotlivých adresářích s příklady pak přeložím do češtiny originální soubory README.
