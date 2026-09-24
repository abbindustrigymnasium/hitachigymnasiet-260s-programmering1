# C++ Övningar

## Instruktioner

**Editor:**
Använd OneCompiler för övningarna

<a href="https://onecompiler.com/cpp">https://onecompiler.com/cpp</a>

**Viktigt:** Alla övningar är uppdaterade för att fungera utan `cin` (användarinput) eftersom det inte fungerar i online miljöer som OneCompiler.

**Exempel på C++-struktur:**

```cpp
#include <iostream>
using namespace std;

int main() {
    // Övning 1.1 - Variabler
    string name = "Kalle Kula";
    int age = 18;
    bool hasDriverLicense = true;
    
    cout << "Namn: " << name << endl;
    cout << "Ålder: " << age << endl;
    cout << "Körkort: " << (hasDriverLicense ? "Ja" : "Nej") << endl;
    
    return 0;
}
```

**Arbetsprocess:**

- Använd `cout` för att visa resultat i terminalen
- Använd hårdkodade värden istället för `cin` (fungerar bättre i online miljöer)

## Innehåll

1. [Variabler](#11-variabler)
2. [Datatyper](#12-datatyper)
3. [Operatorer](#13-operatorer)
4. [Jämförelser](#14-jämförelser)
5. [If-satser](#15-if-satser)
6. [Loopar](#16-loopar-while-och-for)
7. [Switch](#17-switch-satsen)
8. [Funktioner](#18-funktioner)
9. [Referenser och Pekare](#19-referenser-och-pekare)
10. [Klasser](#110-klasser)
11. [Vektorer](#111-vektorer)

---

## 1.1 Variabler

### Övningsuppgifter

### **Övning 1.1.1 - Grundläggande variabler**

1. Deklarera 3 variabler: `name`, `age`, `hasDriverLicense`
2. Tilldela värden: `"Kalle Kula"`, `18`, `true`
3. Skriv ut alla variabler till konsolen

### **Övning 1.1.2 - Kopiera variabler**

1. Deklarera två variabler: `admin` och `name`
2. Tilldela värdet `"John"` till `name`
3. Kopiera värdet från `name` till `admin`
4. Skriv ut värdet på `admin` (ska visa "John")

### **Övning 1.1.3 - Variabelnamngivning**

1. Skapa en variabel med namnet på vår planet (fundera på bra variabelnamn)
2. Skapa en variabel för att lagra namnet på en webbplatsbesökare (fundera på bra variabelnamn)

### **Övning 1.1.4 - Konstanter**

1. Skapa en konstant `PI` med pi-värdet (3 decimaler)
2. Försök tilldela `PI` ett annat värde
3. Skriv ut `PI` - vad händer och varför?

## 1.2 Datatyper

### Övningsuppgifter

### **Övning 1.2.1 - Identifiera datatyper**

**Uppgift:** Fundera först över vilka datatyper följande värden har, skriv ner dina gissningar:

1. `5`
2. `3.14`
3. `"3.14"`
4. `true`
5. `'A'`

## 1.3 Operatorer

### Övningsuppgifter

### **Övning 1.3.1 - Grundläggande räkneoperationer**

1. Skapa 2 variabler med valfria tal (t.ex. `tal1 = 5`, `tal2 = 3`)
2. Skriv ut addition, subtraktion och multiplikation av talen med `cout`

**Kontroll:** Bekräfta genom att skriva ut värdena med `cout`.

### **Övning 1.3.3 - Tilldelningsoperatorer**

**Fråga:** Vilka värden får `a` och `x`?

```cpp
int a = 2;
int x = 1 + (a *= 2);
```

**Kontroll:** Bekräfta med `cout`.

### **Övning 1.3.4 - Typkonvertering**

**Fråga:** Vad blir resultatet av dessa uttryck? Gissa först!

```cpp
1. 5 / 2
2. 5.0 / 2
3. 5 / 2.0
4. static_cast<int>(5.7)
5. static_cast<double>(5)
```

**Kontroll:** Bekräfta med `cout`.

## 1.4 Jämförelser

### Övningsuppgifter

### **Övning 1.4.1 - Jämförelseoperatorer**

**Fråga:** Vad blir resultatet för dessa uttryck? Gissa först!

```cpp
1. 5 > 4
2. "apple" > "pineapple"
3. 2 > 12
4. 5 == 5
5. 5 != 5
```

**Kontroll:** Bekräfta med `cout`.

## 1.5 If-satser

### Övningsuppgifter

**Övning 0. If sats**

1. Skapa en variabel med `age` som tilldelas värdet 16.
2. Använd if-sats för att kontrollera om age är större eller lika med 18. Stämmer det skriv ut "Du får ta körkort".
3. Utöka sedan med else del där du skriver ut "Du får inte ta körkort!".

**Övning 1. If sats**

1. Skapa en variabel `name` med värdet "Kalle".
2. Använd en if-sats för att kontrollera om namnet är "Kalle". Stämmer det skriv ut "Du heter Kalle".
3. Utöka sedan med else del där du skriver ut "Du heter inte Kalle!".

**Övning 2. Namnet C++**
Med `if..else`-konstruktionen, skriv koden som kontrollerar om namnet "C Plus Plus" är korrekt.

Skapa en variabel `userAnswer` med värdet "C Plus Plus".

Om svaret är "C Plus Plus", skriv ut "Korrekt!", Annars skriv ut: "Du vet inte? C Plus Plus!"

**Övning 3. Visa tecknet**
Använd `if..else` och skriv koden som kontrollerar ett nummer och visar sedan beroende på värdet:

Skapa en variabel `number` med värdet 5.

- `1`, om värdet är större än noll,
- `-1`, om mindre än noll,
- `0`, om det är lika med noll.

**Övning 4. Skriv om 'if' med '?'**
Skriv om `if` så att vi istället använder `?` operatorn:

```cpp
int result;
int a = 1;
int b = 2;

if (a + b < 4) {
    result = 0;
} else {
    result = 1;
}
```

## 1.6 Loopar: while och for

### Övningsuppgifter

**Övning 0. For-loop**
Skapa en for-loop som skriver ut siffrorna 1-10.

**Övning 1. While-loop**
Skapa en while-loop som skriver ut siffrorna 1-10.

**Övning 2. Vilka värden visas av while-loopen?**
För varje loop-iteration, skriv ner vilket värde det matar ut och jämför sedan det med lösningen.

Båda looparna skriver ut samma värden eller inte?

1. prefix formen `++i`:

```cpp
int i = 0;
while (++i < 5) {
    cout << i << endl;
}
```

2. postfix formen `i++`:

```cpp
int i = 0;
while (i++ < 5) {
    cout << i << endl;
}
```

**Övning 3. Vilka värden visas av for-loopen?**
För varje loop ska du skriva ner vilka värden den ska visa. Jämför sedan med svaret.

Båda looparna skriver ut samma värden eller inte?

1. postfix formen:

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}
```

2. prefix formen:

```cpp
for (int i = 0; i < 5; ++i) {
    cout << i << endl;
}
```

**Övning 4. Skriv ut jämna siffror i loopen**
Använd `for`-loopen för att skriva ut jämna siffror från `2` till `10`.

**Övning 5. Ersätt "for"-loopen med "while"-loopen**
Skriv om koden som ändrar `for`-loopen till `while`-loopen utan att ändra dess beteende (utgången ska förbli densamma).

```cpp
for (int i = 0; i < 3; i++) {
    cout << "number " << i << "!" << endl;
}
```

## 1.7 Switch-satsen

### Övningsuppgifter

**Övning 1. Skriv om "switch"-satsen till "if"-satser**
Skriv koden med `if..else` som motsvarar följande switch:

```cpp
switch (browser) {
    case 'E':
        cout << "You've got the Edge!" << endl;
        break;
    case 'C':
    case 'F':
    case 'S':
    case 'O':
        cout << "Okay we support these browsers too" << endl;
        break;
    default:
        cout << "We hope that this page looks ok!" << endl;
}
```

**Övning 2. Skriv om "if"-satserna till "switch"-satsen**
Skriv om koden nedan med hjälp av ett enda `switch`-sats:

```cpp
int a = 2; // Hårdkodat värde istället för cin

if (a == 0) {
    cout << 0 << endl;
}
if (a == 1) {
    cout << 1 << endl;
}
if (a == 2 || a == 3) {
    cout << "2,3" << endl;
}
```

## 1.8 Funktioner

### Övningsuppgifter

### **Övning 1.8.1 - Enkel adderingsfunktion**

1. Skapa en funktion `add` som tar in 1 parameter `x` och returnerar `x + x`
2. Anropa funktionen med värdet 5 och skriv ut resultatet med `cout`

### **Övning 1.8.2 - Funktioner med if-satser**

**Uppgift:** Följande funktion returnerar `true` om `age` är högre än 18, annars skriver den ut "Du är för ung tyvärr!":

```cpp
bool checkAge(int age) {
    if (age > 18) {
        return true;
    } else {
        cout << "Du är för ung tyvärr!" << endl;
        return false;
    }
}
```

**Fråga:** Fungerar funktionen annorlunda om `else`-delen tas bort?

```cpp
bool checkAge(int age) {
    if (age > 18) {
        return true;
    }
    cout << "Du är för ung tyvärr!" << endl;
    return false;
}
```

Testa båda varianterna och förklara skillnaden.

**Övning 2. Skriv om funktionen med '?' eller '||'**
Följande funktion returnerar sant om parametern `age` är högre än 18.
Annars skriver den ut "Du är för ung tyvärr!":

```cpp
bool checkAge(int age) {
    if (age > 18) {
        return true;
    } else {
        cout << "Du är för ung tyvärr!" << endl;
        return false;
    }
}
```

**Övning 3. Funktionen min(a, b)**
Skriv en funktion `min(a, b)` som returnerar det minsta av två siffror `a` och `b`.
Till exempel:

```cpp
min(2, 5) == 2
min(3, -1) == -1
min(1, 1) == 1
```

### **Övning 1.8.4 - Potens-funktion**

Skriv en funktion `pow(x, n)` som returnerar `x` upphöjt till `n`. Med andra ord: multiplicera `x` med sig själv `n` gånger.

**Exempel:**

```cpp
pow(2, 3) == 8; // 2 * 2 * 2
pow(3, 2) == 9; // 3 * 3
pow(5, 1) == 5; // 5
```

**Tips:** Använd en loop för att multiplicera `x` med sig själv `n` gånger.

## 1.9 Referenser och Pekare

### Övningsuppgifter

### **Övning 1.9.1 - Referenser**

1. Skapa en variabel `x` med värdet 10
2. Skapa en referens `ref` som refererar till `x`
3. Ändra värdet på `ref` till 20
4. Skriv ut värdet på `x` - vad händer och varför?

### **Övning 1.9.2 - Pekare**

1. Skapa en variabel `y` med värdet 15
2. Skapa en pekare `ptr` som pekar på `y`
3. Ändra värdet på `y` genom pekaren till 25
4. Skriv ut värdet på `y` med `cout`

## 1.10 Klasser

### Enklare övningar – Glass

Börja här! Övningarna bygger på varandra, så använd samma kod och bygg vidare på den. Titta på OOP-bilderna med glassexemplet i presentationen om du kör fast.

### **Övning 1.10.1 - Din första klass**

1. Skapa en klass `Glass` med `public:` och två medlemmar: `string smak` och `int kulor`
2. Skapa ett objekt `glass1` av klassen i `main()`: `Glass glass1;`
3. Ge objektet värden: `glass1.smak = "Choklad";` och `glass1.kulor = 2;`
4. Skriv ut smak och antal kulor med `cout`

**Tips:** Glöm inte semikolon efter klassens avslutande `};`

### **Övning 1.10.2 - Flera objekt**

1. Skapa två objekt till, `glass2` och `glass3`, med andra smaker och antal kulor
2. Skriv ut alla tre glassarna
3. Ändra antal kulor på `glass2` och skriv ut den igen. Ändrades `glass1` också? Varför inte?

### **Övning 1.10.3 - Konstruktor**

1. Lägg till en konstruktor i klassen:

```cpp
Glass(string s, int k) {
    smak = s;
    kulor = k;
}
```

2. Skapa nu glassarna på en rad var: `Glass glass1("Choklad", 2);`
3. Skriv ut alla glassarna igen

### **Övning 1.10.4 - Metoden beskriv()**

1. Lägg till metoden `void beskriv()` i klassen som skriver ut t.ex. `Choklad: 2 kulor`
2. Anropa `beskriv()` på alla tre glassarna: `glass1.beskriv();`

### **Övning 1.10.5 - Metoden pris()**

1. Lägg till metoden `int pris()` som returnerar priset. En kula kostar 15 kr.
2. Skriv ut priset för varje glass
3. Uppdatera `beskriv()` så att den också visar priset: `Choklad: 2 kulor, 30 kr`

### **Övning 1.10.6 - Metoden laggTillKula()**

1. Lägg till metoden `void laggTillKula()` som ökar `kulor` med 1
2. Anropa den två gånger på `glass1` och anropa sedan `beskriv()`. Vad kostar glassen nu?

### **Övning 1.10.7 - Egen klass**

Skapa en egen klass om något du gillar, t.ex. `Hund`, `Bil` eller `Spel`:

1. Klassen ska ha minst 2 medlemmar och en konstruktor
2. Klassen ska ha minst 1 metod som skriver ut något
3. Skapa minst 2 objekt och anropa metoden på båda

### Fler övningar

**Övning 0. En djur-klass**

1. Skapa en klass `Animal` med minst 3 medlemmar, tex `color`, `age`, `name`.
2. Skapa några metoder på klassen också, tex `sound()` och `sleep()` som skriver ut något till konsolen.
3. Lägg till medlemmen `surname` med värdet `"Smith"`.
4. Skriv ut medlemmarna med `cout`.
5. Anropa metoderna.

**Övning 1. Hello Klass**
Skriv koden, en rad för varje åtgärd:

1. Skapa en tom klass `User`.
2. Lägg till medlemmen `name` med värdet `"John"`.
3. Lägg till medlemmen `surname` med värdet `"Smith"`.
4. Ändra på värdet av `name` till `"Pete"`.
5. Skriv ut `name` och `surname`.

**Övning 2. Kolla efter tomhet**
Skriv funktionen `isEmpty()` som returnerar `true` om klassen inte har några medlemmar, `false` annars.

**Övning 3. Summera klassmedlemmar**
Vi har en klass som lagrar löner för vårt team:

```cpp
class Salaries {
public:
    int John = 100;
    int Ann = 160;
    int Pete = 130;
};
```

Skriv koden för att summera alla löner och lagra den i variabeln `sum`. Bör vara `390` i exemplet ovan.

## 1.11 Vektorer

### Övningsuppgifter

**Övning 1. Loopa igenom vektor med namnen i er grupp**

1. Skapa en vektor med namn på alla gruppmedlemmar.
2. Använd en for-loop och loopa igenom alla gruppmedlemmar i vektorn.
3. För varje medlem skriv ut namnet med `cout`.

### **Övning 1.11.2 - Vektor-referenser**

**Fråga:** Vad kommer denna kod att visa? Gissa först!

```cpp
vector<string> fruits = {"Apples", "Pear", "Orange"};

// Skapa en "kopia"
vector<string> shoppingCart = fruits;
shoppingCart.push_back("Banana");

// Vad finns i fruits nu?
cout << fruits.size() << endl; // ?
```

**Kontroll:** Kör koden och förklara resultatet. Varför blev det så?

**Övning 3. Vektor operationer**

Låt oss prova 5 vektoroperationer.

1. Skapa en vektor `styles` med "Jazz" och "Blues".
2. Lägg till "Rock-n-Roll" till slutet av listan.
3. Byt ut värdet i mitten med "Classics". Din kod för att hitta mittvärdet bör fungera för alla listor med udda längd.
4. Ta bort det första värdet i listan och visa det.
5. Lägg till `Rap` och `Reggae` längst fram i listan.

Så här ser resultatet ut i varje steg:

```
Jazz, Blues
Jazz, Blues, Rock-n-Roll
Jazz, Classics, Rock-n-Roll
Classics, Rock-n-Roll
Rap, Reggae, Classics, Rock-n-Roll
```
