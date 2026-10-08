# Övning 2 – Mät luftfuktighet och temperatur med ESP8266

I den här övningen kopplar du en luftfuktighetsmätare av typen **DHT11** till en ESP8266 och skriver ut luftfuktighet och temperatur i Serial Monitor.

DHT11 finns i två utföranden: **på ett kretskort med 3 pinnar** och **som lös sensor med 4 ben**. Oavsett vilken du har behöver du bara koppla **3 pinnar**: ström, data och jord.

## Mål

När du är klar ska du kunna:

- hitta pinnarna för ström, data och jord på din sensor
- koppla sensorn till rätt pinnar på ESP8266
- installera ett bibliotek i Arduino-mjukvaran
- läsa av sensorvärden och skriva ut dem med `Serial.print()`

## Material

- 1 st ESP8266 (NodeMCU) på expansionskort
- 1 st USB-kabel (data)
- 1 st DHT11-sensor (på kretskort med 3 pinnar, eller lös med 4 ben)
- 1 st experimentplatta (breadboard)
- 3 st kopplingskablar
- 1 st resistor på 10 kΩ (rekommenderas bara för den lösa sensorn med 4 ben)

> Har du inte installerat Arduino-mjukvaran och stödet för ESP8266 än? Följ först avsnittet *Installera Arduino-miljön för ESP8266* i [ESP8266-guiden](../README.md).

---

## Steg 1 – Hitta pinnarna på din sensor

Alla DHT11 har samma tre viktiga pinnar:

| Pinne | Betyder | Uppgift |
|-------|---------|---------|
| **VCC** (+) | Strömförsörjning | Ger sensorn ström |
| **DATA** (S) | Signal | Skickar mätvärdena till ESP8266 |
| **GND** (−) | Ground (jord) | Jord |

Var pinnarna sitter beror på vilken sensor du har.

### Alternativ A – Sensor på kretskort (3 pinnar)

Sensorn sitter på ett litet svart kretskort (t.ex. *KY-015*). Kortet har tre pinnar med märkning bredvid.

Håll kortet med den blå sensorn mot dig och pinnarna nedåt:

| Pinne (vänster → höger) | Märkning | Funktion |
|-------------------------|----------|----------|
| Vänster | **S** | DATA |
| Mitten | *(ingen)* | VCC (+) |
| Höger | **−** | GND |

> **Läs alltid märkningen på ditt kort!** Olika tillverkare kan ha olika ordning på pinnarna. Står det **S**, **+** och **−** är det de som gäller.

### Alternativ B – Lös sensor (4 ben)

Sensorn sitter inte på något kretskort och har fyra ben. Ett av benen ska **inte** kopplas in.

Håll sensorn med gallret mot dig och benen nedåt:

```
        DHT11
   ┌─────────────┐
   │ ▦  ▦  ▦  ▦  │
   │             │
   └─────────────┘
     │  │  │  │
     1  2  3  4
     │  │  │  └── GND
     │  │  └───── NC – ska INTE kopplas
     │  └──────── DATA
     └─────────── VCC (+)
```

| Ben | Funktion | Kopplas till |
|-----|----------|--------------|
| 1 | VCC (+) | ström |
| 2 | DATA | signal |
| 3 | NC (*not connected*) | **ingenting** |
| 4 | GND | jord |

> **Tips:** Kretskortet i alternativ A har en inbyggd resistor (märkt **R1**) mellan VCC och DATA. Den lösa sensorn har ingen sådan. Sätt därför gärna en **10 kΩ-resistor** mellan ben 1 (VCC) och ben 2 (DATA) – då blir mätningarna mer pålitliga.

### Spänning – använd 3V3!

ESP8266 arbetar med **3,3 V**. Koppla alltid sensorns VCC till stiftet **3V3** på ESP8266, inte till **VIN** eller **5V**.

---

## Steg 2 – Koppla sensorn till ESP8266

### Vart ska varje pinne?

| Sensor | ESP8266 | Kommentar |
|--------|---------|-----------|
| VCC (+) | **3V3** | Ström |
| DATA (S) | **D5** (GPIO14) | Signal |
| GND (−) | **G** (GND) | Jord |
| NC (bara lös sensor) | – | Kopplas inte |

### Kopplingsschema

```
 ESP8266           Experimentplatta          DHT11

   3V3 ──kabel──▶ raden för VCC ──────────▶ VCC (+)
   D5  ──kabel──▶ raden för DATA ─────────▶ DATA (S)
   G   ──kabel──▶ raden för GND ──────────▶ GND (−)
```

Gör så här, steg för steg:

1. Sätt sensorns pinnar i **olika rader** på experimentplattan, en pinne per rad.
2. Koppla en kabel från **3V3** på ESP8266 till raden där **VCC** sitter.
3. Koppla en kabel från **D5** till raden där **DATA** sitter.
4. Koppla en kabel från **G** till raden där **GND** sitter.
5. *Bara lös sensor (4 ben):* Låt **ben 3 (NC)** vara okopplat. Sätt gärna en 10 kΩ-resistor mellan VCC-raden och DATA-raden.

> **Kontrollera kopplingen innan du kopplar in USB-kabeln!** Byter du plats på VCC och GND kan sensorn gå sönder.

---

## Steg 3 – Installera biblioteket

1. Öppna **Sketch → Include Library → Manage Libraries...**
2. Sök efter **DHT sensor library** och installera biblioteket från **Adafruit**.
3. Välj **Install all** så att även **Adafruit Unified Sensor** installeras.

---

## Steg 4 – Koden

```cpp
#include "DHT.h"

const byte sensorPin = D5;
DHT dht(sensorPin, DHT11);

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

## Steg 5 – Ladda upp och läs av värdena

1. Koppla ESP8266 till datorn med USB-kabeln.
2. Kontrollera att rätt kort (t.ex. *NodeMCU 1.0 (ESP-12E Module)*) och rätt port är valda under **Tools**.
3. Ladda upp koden genom att trycka på **högerpilen** (Upload) uppe till vänster i Arduino-mjukvaran.
4. Öppna **Serial Monitor** (förstoringsglaset uppe till höger) och ställ in hastigheten till **115200 baud**.

Varannan sekund ska det komma en ny rad:

```
Temperatur: 22.00 °C		Luftfuktighet: 41.00 %
Temperatur: 22.00 °C		Luftfuktighet: 42.00 %
```

**Testa sensorn:** Andas försiktigt på sensorn. Luftfuktigheten och temperaturen ska stiga och sedan sakta sjunka igen.

---

## Så fungerar koden

| Kod | Vad gör den? |
|-----|--------------|
| `#include "DHT.h"` | Hämtar biblioteket som vet hur man pratar med sensorn. |
| `DHT dht(sensorPin, DHT11)` | Skapar sensorn och talar om vilket stift den sitter på och vilken typ den är. |
| `Serial.begin(115200)` | Startar kommunikationen med datorn så att du kan skriva ut text i Serial Monitor. |
| `dht.begin()` | Startar sensorn. |
| `readTemperature()` | Läser av temperaturen i °C. |
| `readHumidity()` | Läser av den relativa luftfuktigheten i %. |
| `isnan(...)` | Kontrollerar om mätningen misslyckades. `nan` betyder *not a number* (inte ett tal). |
| `delay(2000)` | Väntar 2 sekunder. Sensorn klarar inte att mäta oftare än så. |

### Fakta om DHT11

| Egenskap | Värde |
|----------|-------|
| Luftfuktighet | 20–90 % |
| Temperatur | 0–50 °C |
| Mätfrekvens | Högst en mätning varannan sekund |

---

## Felsökning

| Problem | Möjlig orsak |
|---------|--------------|
| "Kunde inte läsa från sensorn" | Fel kabel i fel stift – jämför med tabellen *Vart ska varje pinne?*. |
| "Kunde inte läsa från sensorn" (lös sensor) | DATA sitter på ben 3 (NC) i stället för ben 2, eller så behövs 10 kΩ-resistorn mellan VCC och DATA. |
| Konstiga tecken i Serial Monitor | Hastigheten i Serial Monitor är inte inställd på **115200 baud**. |
| `No such file or directory` när du laddar upp | Biblioteket är inte installerat – se *Steg 3*. |
| Sensorn blir varm | VCC och GND har bytt plats. Dra ur USB-kabeln direkt! |
