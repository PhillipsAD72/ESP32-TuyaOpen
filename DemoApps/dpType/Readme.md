# Příklad dpType v TuyaIoT

## Přehled

Tento příklad demonstruje, jak v aplikacích Tuya IoT pracovat s různými typy datových bodů (DP). Ukazuje, jak číst a zapisovat různé typy DP, včetně booleovských, hodnotových, enum, řetězcových, bitmapových a nezpracovaných datových typů.

## Funkce

- Zpracování více typů DP (boolean, hodnota, výčtový, řetězcový, bitmapový, raw)
- Čtení hodnot DP z cloudu Tuya
- Zápis hodnot DP do cloudu Tuya
- Ovládání tlačítkem pro reset zařízení
- Správa konfigurace sítě

## Hardwarové požadavky

- Vývojová deska podporovaná Tuyou (ESP32, T2, T3, T5 atd.)
- Tlačítko připojeno k pinu BUTTON_BUILTIN

## Datové body

Příklad definuje následující DP:

- `DPID_SWITCH` (20): Booleovský typ - Stav přepínače
- `DPID_MODE` (21): Typ výčtu - Provozní režim
- `DPID_BRIGHT` (22): Typ hodnoty - Úroveň jasu
- `DPID_BITMAP` (101): Typ bitmapy - Více příznaků
- `DPID_STRING` (102): Typ řetězce - Textová data
- `DPID_RAW` (103): Typ Raw - Binární data

## Konfigurace

Před nahráním nakonfigurujte tyto parametry:

```cpp
#define TUYA_DEVICE_UUID "uuidxxxxxxxxxxxxxxxx"        // Replace with your device UUID
#define TUYA_DEVICE_AUTHKEY "xxxxxxxxxxxxxxxxxxxxxxxx" // Replace with your auth key
```

ID produktu: `2avicuxv6zgeiquf` (nakonfigurováno v kódu)

## Jak to funguje

1. **Inicializace**: Inicializuje sériovou komunikaci a protokolování
2. **Nastavení licence**: Čte licenci desky nebo používá pevně zakódované přihlašovací údaje
3. **Připojení k IoT**: Připojuje se k platformě Tuya IoT
4. **Zpracování DP**: Přijímá DP příkazy z cloudu a hlásí zpět stav.
5. **Ovládání tlačítky**: Dlouhým stisknutím tlačítka odeberete zařízení

## Operace DP

### Booleovská hodnota (přepínač)
```cpp
bool switchStatus = 0;
TuyaIoT.read(event, DPID_SWITCH, switchStatus);
TuyaIoT.write(DPID_SWITCH, switchStatus);
```

### Hodnota (celé číslo)
```cpp
int brightValue = 0;
TuyaIoT.read(event, DPID_BRIGHT, brightValue);
TuyaIoT.write(DPID_BRIGHT, brightValue);
```

### Výčet (režim)
```cpp
uint32_t mode = 0;
TuyaIoT.read(event, DPID_MODE, mode);
TuyaIoT.write(DPID_MODE, mode);
```

### Řetězec
```cpp
char *strValue = NULL;
TuyaIoT.read(event, DPID_STRING, strValue);
TuyaIoT.write(DPID_STRING, strValue);
```

### Raw (binární)
```cpp
uint8_t *rawValue = NULL;
uint16_t len = 0;
TuyaIoT.read(event, DPID_RAW, rawValue, len);
TuyaIoT.write(DPID_RAW, rawValue, len);
```

## Používání

1. Nahrajte firmware do svého zařízení
2. Otevřete sériový monitor na rychlosti 115200 baudů
3. Zařízení se připojí k platformě Tuya IoT
4. Ovládejte DP pomocí aplikace Tuya Smart
5. Monitorujte sériový výstup pro zobrazení hodnot DP
6. Dlouhým stisknutím tlačítka (3 sekundy) zařízení odeberete
   
## Ovládání tlačítkem

- **Krátké stisknutí**: Žádná akce (lze přizpůsobit)
- **Dlouhý stisk (3 s)**: Odebrání zařízení z platformy Tuya IoT

## Zpracované události

- `TUYA_EVENT_BIND_START`: Párování zařízení zahájeno
- `TUYA_EVENT_ACTIVATE_SUCCESSED`: Aktivace zařízení byla úspěšná
- `TUYA_EVENT_TIMESTAMP_SYNC`: Synchronizace času
- `TUYA_EVENT_DP_RECEIVE_OBJ`: Přijatá data DP objektu
- `TUYA_EVENT_DP_RECEIVE_RAW`: Přijatá DP data nezpracovaného typu

## Závislosti

- Knihovna TuyaIoT
- Knihovna Log (protokolů)

## Poznámky

- Ujistěte se, že máte platnou licenci pro zařízení Tuya.
- Nakonfigurujte správné ID produktu pro váš typ zařízení
- Příklad demonstruje všechny běžné typy DP.
- ID DP musí odpovídat schématu vašeho produktu v platformě Tuya IoT.

## Odstraňování problémů

- Pokud se zařízení nepřipojí, ověřte UUID a AuthKey.
- Zkontrolujte, zda ID produktu odpovídá vašemu produktu na platformě Tuya.
- Zajistěte, aby ID DP odpovídala schématu vašeho produktu.
- Podrobné protokoly naleznete v sériovém výstupu

## Zjistěte více

- Pochopte, jak definovat DP v platformě Tuya IoT
- Seznamte se s různými typy DP a jejich případy použití.
- Podívejte se, jak zvládnout obousměrnou komunikaci DP

