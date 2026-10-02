# ESP8266 - Komplett Guide

## Vad är ESP8266?

ESP8266 är ett mycket prisvärt System-on-Chip (SoC) från Espressif som innehåller en Wi-Fi-stack och en 32-bit mikrocontroller. Vanliga utvecklingskort (NodeMCU) gör det enkelt att programmera med USB-kabel och använda GPIO, ADC, UART, SPI/I²C-bibliotek m.m. Det används ofta för IoT-projekt där du vill ha trådlös uppkoppling på liten hårdvara.

## Vad du behöver hårdvarumässigt

- **Ett utvecklingskort**: t.ex. NodeMCU
- **USB-kabel** (data)
- **Drivrutiner för USB-serial-chip**
- **Strömkälla**: 3.3V 

## Installera Arduino-miljön för ESP8266

1. Ladda ner och installera Arduino IDE 
2. Öppna Arduino → Preferences → i fältet Additional Boards Manager URLs lägg in:
   ```
   https://arduino.esp8266.com/stable/package_esp8266com_index.json
   ```
3. Öppna Tools → Board → Boards Manager, sök efter esp8266 och installera "ESP8266 by ESP8266 Community"
4. Välj rätt kort under Tools → Board (t.ex. "NodeMCU 1.0 (ESP-12E Module)" eller "Generic ESP8266 Module")
5. Välj COM-port och rätt programmeringshastighet

## Grundläggande regler vid uppspelning/flashing

- För vanliga dev-kort (NodeMCU) kopplar du via USB och trycker upload i IDE
- Seriebuss (Serial Monitor) brukar vara 115200 baud för boot-loggar

## Arduino-programstruktur

### setup() funktionen
Körs en gång när kortet startar. Här sätter du upp pinnar, startar seriell kommunikation, ansluter till Wi-Fi etc.

```cpp
void setup() {
  Serial.begin(115200);
  pinMode(LED_BUILTIN, OUTPUT);
  // Andra initialiseringar
}
```

### loop() funktionen
Körs kontinuerligt efter setup(). Här skriver du huvuddelen av ditt program.

```cpp
void loop() {
  // Huvudprogramkod som körs om och om igen
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

## Vanliga inbyggda funktioner

### 1. pinMode(pin, mode)
Innan du använder en pinne måste du tala om för Arduino hur du ska använda den.

```cpp
pinMode(13, OUTPUT);        // Sätter pin 13 som utgång
pinMode(2, INPUT);          // Sätter pin 2 som ingång
pinMode(3, INPUT_PULLUP);   // Ingång med intern pull-up resistor
```

#### När ska jag använda OUTPUT och när INPUT?

Fråga dig själv: **Vem bestämmer spänningen på pinnen – ESP8266 eller komponenten?**

| Läge | ESP8266... | Använd när du vill... | Exempel på komponenter | Funktion i koden |
|------|------------|------------------------|------------------------|------------------|
| `OUTPUT` (utgång) | **skickar ut** spänning (HIGH/LOW) | **styra** något | LED, summer, relä, motordrivare | `digitalWrite()` |
| `INPUT` (ingång) | **läser av** spänning (HIGH/LOW) | **känna av** något | knapp, brytare, rörelsesensor (PIR) | `digitalRead()` |
| `INPUT_PULLUP` | läser av, med inbyggd pull-up-resistor | läsa en knapp utan extra resistor | knapp kopplad mellan pinne och GND | `digitalRead()` |

**Tumregel:**
- Ska ESP8266 **göra** något med världen (tända, låta, starta)? → `OUTPUT`
- Ska ESP8266 **ta reda på** något om världen (är knappen tryckt?)? → `INPUT` eller `INPUT_PULLUP`

```cpp
const int ledPin = D5;     // LED – ESP8266 styr den
const int knappPin = D2;   // Knapp – ESP8266 läser av den

void setup() {
  pinMode(ledPin, OUTPUT);         // vi vill TÄNDA/SLÄCKA lysdioden
  pinMode(knappPin, INPUT_PULLUP); // vi vill LÄSA om knappen är tryckt
}

void loop() {
  if (digitalRead(knappPin) == LOW) {  // LOW = tryckt (pga pull-up)
    digitalWrite(ledPin, HIGH);        // tänd
  } else {
    digitalWrite(ledPin, LOW);         // släck
  }
}
```

> **Vanligt misstag:** Glömmer du `pinMode(ledPin, OUTPUT)` kan lysdioden lysa väldigt svagt eller inte alls, eftersom pinnen då inte driver ut ström ordentligt. Glömmer du `pinMode` för en knapp kan `digitalRead()` ge slumpmässiga värden.

### 2. digitalWrite(pin, value)
Används för att sätta en digital utgång till HIGH (1) eller LOW (0).

```cpp
digitalWrite(13, HIGH);     // Sätter pin 13 till hög nivå (tänd LED)
digitalWrite(13, LOW);      // Sätter pin 13 till låg nivå (släck LED)
```

### 3. digitalRead(pin)
Läser logiskt värde från en digital ingång. Returnerar HIGH eller LOW.

```cpp
int knapp = digitalRead(2); // Läser av knapp på pin 2
if (knapp == HIGH) {
  // knappen är tryckt (beroende på koppling)
}
```

### 4. delay(ms)
Pausar programmet i millisekunder.

```cpp
delay(1000);                // väntar 1 sekund
```

### 5. millis()
Returnerar antal millisekunder sedan kortet startade. Bra för icke-blockerande timers.

```cpp
unsigned long tid = millis();
```

### 6. Serial-funktioner
För att kommunicera via USB/serial med datorn.

```cpp
Serial.begin(9600);         // Starta seriell kommunikation
Serial.print("Hej!");       // Skicka text
Serial.println("Ny rad");   // Skicka text + ny rad
```

## #define vs const int - Vilket ska jag använda?

### #define (Preprocessor directive)
```cpp
#define LED_PIN 13
#define BUTTON_PIN 2
```

### const int (Konstant variabel)
```cpp
const int ledPin = 13;
const int buttonPin = 2;
```

### Varför #define?
- **Minne**: Tar inget RAM-minne (textersättning före kompilering)
- **Prestanda**: Ingen overhead
- **Tradition**: Vanligt i C-språket

### Varför const int?
- **Typsäkerhet**: Kompileringsfel vid fel typ
- **Debugging**: Syns i debugger
- **Modern C++**: Rekommenderat i modern kod

### Rekommendation
**Använd `const int`** för pin-nummer och enkla konstanter. Använd `#define` bara för kompileringstidsvillor och makro-funktioner.

## ESP8266 Pinnar och funktioner

### GPIO-pinnar (General Purpose Input/Output)

**Viktigt**: På NodeMCU finns det både GPIO-nummer och D-pin nummer som kan vara förvirrande!

#### GPIO vs D-pin nummer på NodeMCU:
- **D1** = GPIO5
- **D2** = GPIO4  
- **D3** = GPIO0
- **D4** = GPIO2
- **D5** = GPIO14
- **D6** = GPIO12
- **D7** = GPIO13
- **D8** = GPIO15

#### I koden använder du GPIO-nummer:
```cpp
const int ledPin = 2;     // GPIO2 = D4 på NodeMCU
const int buttonPin = 4;  // GPIO4 = D2 på NodeMCU
// eller
const int ledPin = D4;    // Samma som GPIO2
const int buttonPin = D2; // Samma som GPIO4
```

#### GPIO-funktioner:
- **GPIO0**: Kan användas som digital I/O, men viktig för boot-läge
- **GPIO1 (TX)**: UART TX, används för seriell kommunikation
- **GPIO3 (RX)**: UART RX, används för seriell kommunikation
- **GPIO2**: Digital I/O, används ofta för LED
- **GPIO4 (SDA)**: I²C SDA, digital I/O
- **GPIO5 (SCL)**: I²C SCL, digital I/O
- **GPIO12-15**: Digital I/O pinnar
- **GPIO16**: Digital I/O, kan användas för wake-up från deep sleep

### ADC (Analog-to-Digital Converter)
- **A0**: Endast analog ingång på ESP8266 (0-1V, mappas till 0-1023)

### Strömförsörjning
- **VCC**: 3.3V (viktigt: inte 5V!)
- **GND**: Jord (referenspunkt för alla spänningar)
- **3V3**: 3.3V utgång (begränsad ström)

## GND/Jord - Vad är det?

**GND (Ground)** är referenspunkten för alla spänningar i en krets. Det är den "nollpunkten" som alla andra spänningar mäts mot.

### Varför behövs GND?
- **Referenspunkt**: Alla spänningar behöver en referens för att ha mening
- **Slutledning**: Strömmen måste ha en väg att gå tillbaka till källan
- **Säkerhet**: Ger en säker referenspunkt för mätningar

### Kopplingsexempel
```
ESP8266          Komponent
------           ---------
3.3V     ----->  LED (+)
GPIO2    ----->  LED (-) -----> GND
GND      ----->  Knapp ena sidan
GPIO4    ----->  Knapp andra sidan
```

### Viktiga regler
- Alla GND ska vara sammankopplade i en krets
- Använd alltid GND som referens för mätningar
- GND är inte nödvändigtvis 0V - det är bara referenspunkten

## Kodexempel

### Enkel Blink (NodeMCU)
```cpp
// Blinka inbyggd LED på NodeMCU
void setup() {
  pinMode(LED_BUILTIN, OUTPUT); // LED_BUILTIN är ofta LOW-aktiv på NodeMCU
}

void loop() {
  digitalWrite(LED_BUILTIN, LOW);   // tänd (beroende på board)
  delay(500);
  digitalWrite(LED_BUILTIN, HIGH);  // släck
  delay(500);
}
```

### LED på D1 (GPIO5) - Blink var 3:e sekund
```cpp
const int ledPin = D1;  // D1 = GPIO5 på NodeMCU

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(115200);
  Serial.println("LED blinkar var 3:e sekund på D1");
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Tänd LED
  Serial.println("LED ON");
  delay(3000);                 // Vänta 3 sekunder
  
  digitalWrite(ledPin, LOW);   // Släck LED
  Serial.println("LED OFF");
  delay(3000);                 // Vänta 3 sekunder
}
```

#### Kopplingsschema för LED på D1
```
NodeMCU/ESP8266          Komponenter
===============          ===========

D1 (GPIO5)     ----->    220Ω Resistor -----> LED (+) (långa benet)
                                                      |
LED (-) (korta benet) <------------------------------+
                                                      |
GND            ----->    GND (jord)
```

**Kopplingsanvisningar:**
1. Koppla en 220Ω resistor från D1 till LED:s positiva ben (långa benet)
2. Koppla LED:s negativa ben (korta benet) till GND
3. Ladda upp koden och se LED:en blinka var 3:e sekund

### Anslut till Wi-Fi och köra enkel webserver
```cpp
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>

const char* ssid = "DIN_SSID";
const char* pass = "DITT_LÖSENORD";

ESP8266WebServer server(80);

void handleRoot() {
  server.send(200, "text/plain", "Hej från ESP8266!");
}

void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, pass);
  Serial.print("Ansluter till WiFi ");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println();
  Serial.print("IP: ");
  Serial.println(WiFi.localIP());
  server.on("/", handleRoot);
  server.begin();
}

void loop() {
  server.handleClient();
}
```

### Knappstyrd LED
```cpp
const int buttonPin = D4;   // D4 = GPIO2 på NodeMCU
const int ledPin = LED_BUILTIN;  // LED på inbyggd pin

int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  if (buttonState == LOW) {  // Knapp tryckt (LOW pga PULLUP)
    digitalWrite(ledPin, LOW);   // Tänd LED
    Serial.println("LED ON");
  } else {
    digitalWrite(ledPin, HIGH);  // Släck LED
    Serial.println("LED OFF");
  }
  
  delay(50); // Debounce
}
```

#### Kopplingsschema för knapp
```
NodeMCU D4 (GPIO2) -----> Knapp ena sidan
Knapp andra sidan -----> GND
(Intern pull-up resistor aktiveras i kod)
```

## Tips & felsökning

- **Kontrollera drivrutiner**: CH340/CP2102 för USB-serial kommunikation
- **Upload-problem**: Välj lägre upload-speed i Tools, kontrollera COM-port
- **Strömproblem**: Om boardet blir instabilt under Wi-Fi kan det bero på otillräcklig 3.3V-ström
- **Råa ESP-moduler**: Läs pinout-guide (GPIO0/GPIO2/CH_PD/RST) innan du kopplar

## Vanliga utvecklingskort

### NodeMCU
- Inbyggd USB-TTL (CH340/CP2102)
- 3.3V regulator
- Enkelt att programmera via USB
- Många GPIO-pinnar tillgängliga

## Användningsområden

- **IoT-projekt**: Temperaturmätning, fjärrstyrning
- **Webbservrar**: Enkla webbsidor för kontroll
- **Sensorer**: Läsning av olika typer av sensorer
- **Automation**: Hemautomatisering, trädgårdsvattning
- **Prototyper**: Snabb utveckling av trådlösa projekt

## Vanliga komponenter

### Breadboard
**Syfte**: Prototypkort för att koppla komponenter utan löda
- **Användning**: Sätt in komponenter och använd jumpers för att koppla
- **Fördelar**: Snabb prototypning, enkelt att ändra kopplingar
- **Tips**: Använd olika färger på jumpers för olika funktioner (röd=+3.3V, svart=GND)
- **Video**: [Hur fungerar en breadboard?](https://www.youtube.com/watch?v=W6mixXsn-Vc)

### Resistorer
**Syfte**: Begränsar ström och delar spänning
- **LED-skydd**: 220Ω-1kΩ för att skydda LED från för hög ström
- **Pull-up/Pull-down**: 10kΩ för knappar och digitala ingångar
- **Spänningsdelning**: Kombinera resistorer för att mäta högre spänningar

```cpp
// Exempel: LED med 220Ω resistor
// ESP8266 GPIO2 -> 220Ω resistor -> LED -> GND
digitalWrite(2, HIGH); // Tänder LED
```

### Kapacitorer
**Syfte**: Stabiliserar strömförsörjning och filtrerar brus
- **Decoupling**: 100nF nära strömförsörjning för stabilisering
- **Smoothning**: 100µF-1000µF för att jämna ut spänningsvariationer
- **Timing**: Används i oscillator-kretsar

### Dioder
**Syfte**: Leder ström i en riktning, skyddar mot felpolaritet
- **LED**: Lysdiod för indikering
- **Skyddsdiod**: Skyddar mot felpolaritet (1N4007)
- **Zenerdiod**: Konstant spänning (3.3V Zener för spänningsreglering)

### Jumpers (Kopplingskablar)
**Syfte**: Kopplar komponenter på breadboard
- **Färgkodning**: Röd (+3.3V), svart (GND), färgade (signaler)
- **Längder**: Olika längder för olika avstånd
- **Tips**: Använd korta kablar för att undvika brus

### Knappar och brytare
**Syfte**: Användarinteraktion och manuell kontroll
- **Pull-up**: Använd `INPUT_PULLUP` för enklare koppling
- **Debounce**: Lägg till `delay(50)` för att undvika flera tryck

```cpp
// Knapp med pull-up resistor
pinMode(2, INPUT_PULLUP);
int buttonState = digitalRead(2);
if (buttonState == LOW) { // Tryckt (LOW pga pull-up)
  // Knappen är tryckt
}
```

### Sensorer
**Syfte**: Mäter fysiska storheter
- **Temperatur**: DS18B20, DHT22, LM35
- **Ljus**: LDR (Light Dependent Resistor), fotodiod
- **Rörelse**: PIR-sensor, accelerometer
- **Avstånd**: Ultrasonic sensor (HC-SR04)

### Reläer
**Syfte**: Styr högre spänningar/strömmar med låg spänning
- **Koppling**: ESP8266 GPIO -> Relä -> Last (lampor, motorer)
- **Skydd**: Använd flybackdiod för att skydda mot spikar

### Kopplingsexempel med komponenter

#### LED med resistor
```
ESP8266 GPIO2 -> 220Ω resistor -> LED (+) -> LED (-) -> GND
```

#### Knapp med pull-up
```
ESP8266 GPIO4 -> Knapp ena sidan
Knapp andra sidan -> GND
(Intern pull-up resistor aktiveras i kod)
```

#### Temperatursensor (DS18B20)
```
ESP8266 3.3V -> DS18B20 VCC
ESP8266 GPIO5 -> DS18B20 Data
ESP8266 GND -> DS18B20 GND
4.7kΩ resistor mellan Data och 3.3V (pull-up)
```

## Resurser och länkar

### Officiell dokumentation
- [ESP8266 Arduino Core Documentation](https://arduino.esp8266.com/stable/index.html) - Komplett API-referens
- [Espressif ESP8266 Datasheet](https://www.espressif.com/sites/default/files/documentation/0a-esp8266ex_datasheet_en.pdf) - Teknisk specifikation

### YouTube-tutorials
- [ESP8266 Tutorial Playlist](https://youtube.com/playlist?list=PLlLe2PpVuiVLj8fOOM4cpEHbVZ1SexbtT&si=GWnsIVnBnKqW_LDv) - Omfattande video-serie om ESP8266
- [Hur fungerar en breadboard?](https://www.youtube.com/watch?v=W6mixXsn-Vc) - Så kopplar du komponenter på en experimentplatta

### Praktiska guider
- [Random Nerd Tutorials - ESP8266](https://randomnerdtutorials.com/category/esp8266/) - Steg-för-steg projekt
- [Arduino Project Hub - ESP8266](https://create.arduino.cc/projecthub/products/esp8266) - Community-projekt
- [Instructables - ESP8266](https://www.instructables.com/circuits/esp8266/) - DIY-projekt och tutorials


## Nästa steg

1. Börja med enkla exempel (Blink, knapp + LED)
2. Lägg till Wi-Fi-funktionalitet
3. Experimentera med sensorer
4. Bygg enkla IoT-projekt
5. Utforska avancerade funktioner som OTA-uppdateringar
