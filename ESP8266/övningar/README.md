# Övning 1 – Blinka en lysdiod med ESP8266

I den här övningen kopplar du en lysdiod (LED) och en resistor på en experimentplatta (breadboard) till en ESP8266 och programmerar lysdioden så att den blinkar.

## Mål

När du är klar ska du kunna:

- koppla komponenter på en experimentplatta (breadboard)
- förklara varför en lysdiod behöver en resistor i serie
- veta vilket ben på lysdioden som är plus och vilket som är minus
- använda `pinMode()`, `digitalWrite()` och `delay()`
- ladda upp ett program till ESP8266 från Arduino-mjukvaran

## Material

- 1 st ESP8266 (NodeMCU) på expansionskort
- 1 st USB-kabel (data)
- 1 st lysdiod (LED)
- 1 st resistor (t.ex. 220 Ω)
- 1 st experimentplatta (breadboard)
- 2 st kopplingskablar

> Har du inte installerat Arduino-mjukvaran och stödet för ESP8266 än? Följ först avsnittet *Installera Arduino-miljön för ESP8266* i [ESP8266-guiden](../README.md).

---

## Steg 1 – Lär känna komponenterna

### Stiften på ESP8266

Bredvid ESP8266 finns det många metallstift som sticker upp. Vi ska använda stiften **5** och **G**.

![ESP8266 på expansionskort. Stiften 5 och G finns i raden med siffror.](bild1.png)

- **5** är det digitala stiftet **D5**. **D** står för *digital*, det vill säga att stiftet antingen har **låg** (`LOW`) eller **hög** (`HIGH`) spänningsnivå jämfört med jord.
- **G** står för *ground* (jord). Det är strömmens väg tillbaka till ESP8266.

### Lysdioden

En lysdiod leder bara ström åt **ett** håll. Därför spelar det roll hur du vänder den.

| Ben         | Namn  | Pol | Kopplas mot     |
|-------------|-------|-----|-----------------|
| Långa benet | Anod  | +   | resistorn (D5)  |
| Korta benet | Katod | −   | G (jord)        |

> Tips: Kanten på lysdioden är ofta **platt** på samma sida som det korta benet (−).

### Resistorn

En lysdiod släpper igenom nästan hur mycket ström som helst när den väl lyser. Utan resistor kan det gå så mycket ström att lysdioden eller ESP8266-stiftet går sönder. Resistorn **begränsar strömmen**. Det spelar ingen roll åt vilket håll du vänder resistorn.

### Experimentplattan

Hålen på experimentplattan har **elektrisk kontakt med varandra i grupper om fem hål**. En sådan grupp kallas här för en **rad**. Det betyder:

- En kabel och ett komponentben som sitter i **samma rad** är ihopkopplade.
- Ett komponentben som sitter i en **annan rad** är **inte** ihopkopplat.
- Grupperna på var sin sida om mittspåret är **inte** ihopkopplade med varandra.

Se videon [Hur fungerar en breadboard?](https://www.youtube.com/watch?v=W6mixXsn-Vc) om du vill veta mer.

---

## Steg 2 – Koppla ESP8266 → breadboard → resistor → diod

Strömmen ska gå i en slinga: ut från **D5**, genom **resistorn**, genom **lysdioden** och tillbaka till **G**.

```
 ESP8266                       Experimentplatta
 
   D5 ───kabel───▶ rad 1 ──[ resistor ]── rad 4 ──▶|── rad 6
                                          (+ långa ben)  (− korta ben)
                                                          │
   G  ◀──kabel────────────────────────────────────────────┘
```

Gör så här, steg för steg:

1. **Kabel från D5:** Koppla en kabel från stift **5** på ESP8266 till ett hål i **rad 1** på experimentplattan.
2. **Resistorn:** Sätt resistorns ena ben i **rad 1** (samma rad som kabeln) och det andra benet i **rad 4**.
3. **Lysdioden:** Sätt lysdiodens **långa ben (+)** i **rad 4** (samma rad som resistorn) och det **korta benet (−)** i **rad 6**.
4. **Kabel till G:** Koppla en kabel från **rad 6** (samma rad som det korta benet) tillbaka till stift **G** på ESP8266.

| Från                  | Till                  | Rad på breadboard |
|-----------------------|-----------------------|-------------------|
| ESP8266 stift 5 (D5)  | resistorns ena ben    | rad 1             |
| resistorns andra ben  | lysdiodens långa ben  | rad 4             |
| lysdiodens korta ben  | ESP8266 stift G (GND) | rad 6             |

Radnumren är bara exempel. Det viktiga är att varje koppling delar rad med nästa komponent, och att en komponents två ben **aldrig** sitter i samma rad.

> **Kontrollera kopplingen innan du kopplar in USB-kabeln!** Följ strömmens väg med fingret: D5 → resistor → långa benet → korta benet → G.

---

## Steg 3 – Ladda upp koden

1. Koppla ESP8266 till datorn med USB-kabeln.
2. Öppna Arduino-mjukvaran och skapa en ny skiss.
3. Kontrollera att rätt kort (t.ex. *NodeMCU 1.0 (ESP-12E Module)*) och rätt port är valda under **Tools**.
4. Klistra in koden nedan.
5. Ladda upp koden genom att trycka på **högerpilen** (Upload) uppe till vänster i Arduino-mjukvaran.

```cpp
const byte ledPin = D5;

void setup() {
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(1000);

  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

När uppladdningen är klar ska lysdioden lysa i en sekund, vara släckt i en sekund och sedan börja om.

---

## Så fungerar koden

### Konstanten

```cpp
const byte ledPin = D5;
```

Vi ger stiftet ett namn så att koden blir lättare att läsa. Om du flyttar kabeln till ett annat stift behöver du bara ändra på den här raden.

### setup()

Körs **en gång** när ESP8266 startar:

- `pinMode(ledPin, OUTPUT)` talar om att stiftet ska **skicka ut** spänning (inte läsa in).
- `digitalWrite(ledPin, LOW)` ser till att lysdioden är släckt från början.

### loop()

Körs **om och om igen**:

| Rad                           | Vad händer?                                    |
|-------------------------------|------------------------------------------------|
| `digitalWrite(ledPin, HIGH);` | D5 får hög spänning – lysdioden **tänds**.     |
| `delay(1000);`                | Programmet väntar 1000 ms (= 1 sekund).        |
| `digitalWrite(ledPin, LOW);`  | D5 får låg spänning – lysdioden **släcks**.    |
| `delay(1000);`                | Programmet väntar 1 sekund till.               |

Sedan börjar `loop()` om från början.

---

## Felsökning

| Problem | Möjlig orsak |
|---------|--------------|
| Lysdioden lyser aldrig | Lysdioden sitter åt fel håll – vänd på den så att långa benet sitter mot resistorn. |
| Lysdioden lyser aldrig | Kabeln till G saknas, eller två ben som ska höra ihop sitter i olika rader. |
| Lysdioden lyser aldrig | Resistorns båda ben sitter i samma rad, eller kabeln sitter i fel stift (inte 5). |
| Lysdioden lyser hela tiden | Kabeln sitter i 3V3 i stället för 5, eller koden laddades inte upp. |
| Uppladdningen misslyckas | Fel kort eller port vald under **Tools**, eller USB-kabeln klarar bara laddning (inte data). |

---

## Extrauppgifter

1. **Ändra takten** – låt lysdioden lysa i 2 sekunder och vara släckt i 0,5 sekunder.
2. **Blinka snabbt** – hur kort kan `delay()` vara innan du inte längre ser att lysdioden blinkar?
3. **SOS** – låt lysdioden blinka SOS i morsekod: tre korta, tre långa, tre korta.
4. **Byt stift** – flytta kabeln från stift 5 till stift 6. Vad måste du ändra i koden?

---

**Nästa övning:** [Övning 2 – Mät luftfuktighet och temperatur](övning2-luftfuktighet.md)
