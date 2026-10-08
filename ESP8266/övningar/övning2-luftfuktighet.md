# Övning 2 – Mät luftfuktighet och temperatur med ESP8266

I den här övningen kopplar du en luftfuktighetsmätare till en ESP8266 och skriver ut luftfuktighet och temperatur i Serial Monitor.

Luftfuktighetsmätare finns med **4 pinnar** och med **3 pinnar**. De kopplas olika, så börja med att ta reda på vilken du har.

## Mål

När du är klar ska du kunna:

- avgöra vilken typ av luftfuktighetsmätare du har
- koppla sensorn till rätt pinnar på ESP8266
- installera ett bibliotek i Arduino-mjukvaran
- läsa av sensorvärden och skriva ut dem med `Serial.print()`

## Material

- 1 st ESP8266 (NodeMCU) på expansionskort
- 1 st USB-kabel (data)
- 1 st luftfuktighetsmätare (med 3 eller 4 pinnar)
- 1 st experimentplatta (breadboard)
- 4 st kopplingskablar
- 2 st resistorer på 4,7 kΩ–10 kΩ (behövs bara för sensorn med 4 pinnar)

> Har du inte installerat Arduino-mjukvaran och stödet för ESP8266 än? Följ först avsnittet *Installera Arduino-miljön för ESP8266* i [ESP8266-guiden](../README.md).

---

## Steg 1 – Vilken sensor har jag?

| Antal pinnar | Hur ser den ut? | Vanlig modell | Hur pratar den med ESP8266? |
|--------------|-----------------|---------------|-----------------------------|
| **4 pinnar** | En liten vit eller svart plastbit med galler, utan kretskort. Text på sensorn: **AM2320**. | AM2320 | **I2C** – två signalledningar (SDA och SCL) |
| **3 pinnar** | Sensorn sitter på ett litet kretskort. Pinnarna är märkta **+**, **OUT/S/DATA** och **−**. | DHT11 (blå) eller DHT22 (vit) på kretskort | **En signalledning** (DATA) |

> **Se upp:** En DHT22 eller DHT11 *utan* kretskort har också 4 pinnar, men den tredje pinnen används inte. Står det **DHT** på sensorn ska du följa instruktionerna för 3 pinnar och bara strunta i den oanvända pinnen. Fråga din lärare om du är osäker.

### Spänning – använd 3V3!

ESP8266 arbetar med **3,3 V**. Koppla alltid sensorns strömpinne till stiftet **3V3** på ESP8266, inte till **VIN** eller **5V**.

---

## Del A – Sensor med 4 pinnar (AM2320)

### Pinnarna

Håll sensorn med gallret mot dig och pinnarna nedåt. Pinnarna är då, från vänster till höger:

| Pinne | Namn | Betyder | Uppgift |
|-------|------|---------|---------|
| 1 | **VDD** | Strömförsörjning | Ger sensorn ström (3,3–5,5 V) |
| 2 | **SDA** | Serial Data | Skickar data fram och tillbaka |
| 3 | **GND** | Ground (jord) | Jord |
| 4 | **SCL** | Serial Clock | Klocksignal som håller takten i kommunikationen |

### Vart ska varje pinne?

| AM2320 | ESP8266 | Kommentar |
|--------|---------|-----------|
| 1 – VDD | **3V3** | Ström |
| 2 – SDA | **D2** (GPIO4) | I2C-data. Behöver en resistor till 3V3. |
| 3 – GND | **G** (GND) | Jord |
| 4 – SCL | **D1** (GPIO5) | I2C-klocka. Behöver en resistor till 3V3. |

### Varför behövs två resistorer?

AM2320 har **inga inbyggda pull-up-resistorer** för I2C-ledningarna. Utan dem vet SDA och SCL inte vilken spänning de ska ha när ingen skickar något, och kommunikationen fungerar inte. Därför sätter du:

- en resistor (4,7 kΩ–10 kΩ) mellan **SDA** och **3V3**
- en resistor (4,7 kΩ–10 kΩ) mellan **SCL** och **3V3**

### Kopplingsschema

```
 ESP8266          Experimentplatta              AM2320

   3V3 ──kabel──▶ rad 1 ───────────────────────▶ 1 VDD
   D2  ──kabel──▶ rad 2 ───────────────────────▶ 2 SDA
   G   ──kabel──▶ rad 3 ───────────────────────▶ 3 GND
   D1  ──kabel──▶ rad 4 ───────────────────────▶ 4 SCL

 Pull-up-resistorer på experimentplattan:

   rad 1 (VDD) ──[ resistor ]── rad 2 (SDA)
   rad 1 (VDD) ──[ resistor ]── rad 4 (SCL)
```

Gör så här, steg för steg:

1. Sätt sensorns fyra pinnar i **fyra intilliggande rader** på experimentplattan, en pinne per rad (till exempel rad 1–4).
2. Koppla en kabel från **3V3** på ESP8266 till raden där **VDD** (pinne 1) sitter.
3. Koppla en kabel från **D2** till raden där **SDA** (pinne 2) sitter.
4. Koppla en kabel från **G** till raden där **GND** (pinne 3) sitter.
5. Koppla en kabel från **D1** till raden där **SCL** (pinne 4) sitter.
6. Sätt en resistor mellan **VDD-raden** och **SDA-raden**.
7. Sätt en resistor mellan **VDD-raden** och **SCL-raden**. Är raderna långt ifrån varandra kan du använda en extra kabel från VDD-raden.

> **Kontrollera kopplingen innan du kopplar in USB-kabeln!** Byter du plats på VDD och GND kan sensorn gå sönder.

### Installera biblioteket

1. Öppna **Sketch → Include Library → Manage Libraries...**
2. Sök efter **Adafruit AM2320** och installera *Adafruit AM2320 sensor library*.
3. Får du frågan om du vill installera bibliotek som det behöver (**Adafruit Unified Sensor** och **Adafruit BusIO**), välj **Install all**. Annars söker du upp och installerar dem en och en.

### Koden

```cpp
#include "Adafruit_Sensor.h"
#include "Adafruit_AM2320.h"

Adafruit_AM2320 am2320 = Adafruit_AM2320();

void setup() {
  Serial.begin(115200);
  am2320.begin();   // Startar I2C på D2 (SDA) och D1 (SCL)
}

void loop() {
  float temperatur = am2320.readTemperature();
  float luftfuktighet = am2320.readHumidity();

  if (isnan(temperatur) || isnan(luftfuktighet)) {
    Serial.println("Kunde inte läsa från sensorn – kontrollera kopplingen!");
  } else {
    Serial.print("Temperatur: ");
    Serial.print(temperatur);
    Serial.print(" °C\t\tLuftfuktighet: ");
    Serial.print(luftfuktighet);
    Serial.println(" %");
  }

  delay(2000);   // AM2320 klarar en mätning varannan sekund
}
```

---

## Del B – Sensor med 3 pinnar (DHT11/DHT22 på kretskort)

### Pinnarna

Ordningen på pinnarna skiljer sig mellan olika kretskort. **Läs vad som står tryckt vid pinnarna** på ditt kort.

| Märkning på kortet | Betyder | Uppgift |
|--------------------|---------|---------|
| **+**, VCC eller VDD | Strömförsörjning | Ger sensorn ström |
| **OUT**, **S** eller **DATA** | Signal | Skickar mätvärdena |
| **−** eller GND | Ground (jord) | Jord |

### Vart ska varje pinne?

| Sensor (3 pinnar) | ESP8266 | Kommentar |
|-------------------|---------|-----------|
| + / VCC | **3V3** | Ström |
| OUT / S / DATA | **D5** (GPIO14) | Signal |
| − / GND | **G** (GND) | Jord |

Här behövs **ingen extra resistor** – kretskortet har redan en pull-up-resistor inbyggd.

### Kopplingsschema

```
 ESP8266                Experimentplatta          Sensor (3 pinnar)
 
   3V3 ───kabel──▶ rad 1 ──────────────────────────▶ +   / VCC
   D5  ───kabel──▶ rad 3 ──────────────────────────▶ OUT / S / DATA
   G   ───kabel──▶ rad 5 ──────────────────────────▶ −   / GND
```

1. Sätt sensorns tre pinnar i **tre olika rader** på experimentplattan.
2. Koppla en kabel från **3V3** till raden där **+** sitter.
3. Koppla en kabel från **D5** till raden där **OUT/S/DATA** sitter.
4. Koppla en kabel från **G** till raden där **−** sitter.

> **Kontrollera kopplingen innan du kopplar in USB-kabeln!** Byter du plats på + och − kan sensorn gå sönder.

### Installera biblioteket

1. Öppna **Sketch → Include Library → Manage Libraries...**
2. Sök efter **DHT sensor library** och installera biblioteket från **Adafruit**.
3. Välj **Install all** så att även **Adafruit Unified Sensor** installeras.

### Koden

Ändra `DHT11` till `DHT22` på rad 4 om du har en vit DHT22.

```cpp
#include "DHT.h"

const byte sensorPin = D5;
DHT dht(sensorPin, DHT11);   // Byt till DHT22 om du har en vit sensor

void setup() {
  Serial.begin(115200);
  dht.begin();
}

void loop() {
  float temperatur = dht.readTemperature();
  float luftfuktighet = dht.readHumidity();

  if (isnan(temperatur) || isnan(luftfuktighet)) {
    Serial.println("Kunde inte läsa från sensorn – kontrollera kopplingen!");
  } else {
    Serial.print("Temperatur: ");
    Serial.print(temperatur);
    Serial.print(" °C\t\tLuftfuktighet: ");
    Serial.print(luftfuktighet);
    Serial.println(" %");
  }

  delay(2000);   // Vänta minst 2 sekunder mellan mätningarna
}
```

---

## Steg 2 – Ladda upp och läs av värdena

1. Koppla ESP8266 till datorn med USB-kabeln.
2. Kontrollera att rätt kort (t.ex. *NodeMCU 1.0 (ESP-12E Module)*) och rätt port är valda under **Tools**.
3. Ladda upp koden genom att trycka på **högerpilen** (Upload) uppe till vänster i Arduino-mjukvaran.
4. Öppna **Serial Monitor** (förstoringsglaset uppe till höger) och ställ in hastigheten till **115200 baud**.

Varannan sekund ska det komma en ny rad:

```
Temperatur: 22.40 °C		Luftfuktighet: 41.80 %
Temperatur: 22.40 °C		Luftfuktighet: 41.90 %
```

**Testa sensorn:** Andas försiktigt på sensorn. Luftfuktigheten och temperaturen ska stiga och sedan sakta sjunka igen.

---

## Så fungerar koden

| Kod | Vad gör den? |
|-----|--------------|
| `#include "..."` | Hämtar biblioteket som vet hur man pratar med sensorn. |
| `Serial.begin(115200)` | Startar kommunikationen med datorn så att du kan skriva ut text i Serial Monitor. |
| `am2320.begin()` / `dht.begin()` | Startar sensorn. |
| `readTemperature()` | Läser av temperaturen i °C. |
| `readHumidity()` | Läser av den relativa luftfuktigheten i %. |
| `isnan(...)` | Kontrollerar om mätningen misslyckades. `nan` betyder *not a number* (inte ett tal). |
| `delay(2000)` | Väntar 2 sekunder. Sensorerna klarar inte att mäta oftare än så. |

### Fakta om AM2320 (4 pinnar)

| Egenskap | Värde |
|----------|-------|
| Spänning | 3,3–5,5 V |
| Luftfuktighet | 0–100 %, noggrannhet ±3 % (mellan 20 och 80 %) |
| Temperatur | −40 till +80 °C, noggrannhet ±0,5 °C (vid 25 °C) |
| I2C-adress | 0x5C |
| Mätfrekvens | En mätning varannan sekund |

---

## Felsökning

| Problem | Möjlig orsak |
|---------|--------------|
| "Kunde inte läsa från sensorn" | Fel kabel i fel stift – jämför med tabellen för din sensor. |
| "Kunde inte läsa från sensorn" (4 pinnar) | Pull-up-resistorerna saknas, eller SDA och SCL har bytt plats (SDA → D2, SCL → D1). |
| "Kunde inte läsa från sensorn" (3 pinnar) | Fel sensortyp i koden – prova att byta `DHT11` mot `DHT22`. |
| Konstiga tecken i Serial Monitor | Hastigheten i Serial Monitor är inte inställd på **115200 baud**. |
| `No such file or directory` när du laddar upp | Biblioteket är inte installerat – se *Installera biblioteket*. |
| Sensorn blir varm | Ström och jord har bytt plats. Dra ur USB-kabeln direkt! |

---

## Extrauppgifter

1. **Fahrenheit** – räkna om temperaturen till Fahrenheit (`°F = °C × 1,8 + 32`) och skriv ut båda.
2. **Varning** – tänd lysdioden från [Övning 1](README.md) när luftfuktigheten är över 60 %.
3. **Högsta och lägsta** – spara det högsta och lägsta värdet som har uppmätts och skriv ut dem varje gång.
4. **Medelvärde** – gör 5 mätningar och skriv ut medelvärdet i stället för varje enskild mätning.
