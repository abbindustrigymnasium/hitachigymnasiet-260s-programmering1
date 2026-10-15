# DOM (Document Object Model) Övningar

---

## Övning 1 - DOM Element Selection (Grundläggande)

**Mål:** Lära dig de viktigaste metoderna för att hitta HTML-element med JavaScript.

**Förväntat resultat:** Du kommer att förstå skillnaden mellan klassiska och moderna DOM-selektorer.

### Del A: Klassiska DOM-metoder

**Uppgift:**
Skapa en HTML-sida och använd klassiska DOM-metoder för att hitta element.

**Steg:**

1. Skapa HTML-filen med koden nedan
2. Använd följande metoder:
   - `document.getElementById('myDiv')` → hitta div-elementet
   - `document.getElementsByTagName('li')` → hitta alla li-element
   - `document.getElementsByClassName('myClass')` → hitta element med klassen "myClass"
3. Skriv ut varje elements `.nodeName` med `console.log()`

**Vad ska hända:** Du ska se "DIV", "LI" (två gånger), "H4" och "P" i konsolen.

### Del B: Moderna selektorer (Rekommenderat)

**Uppgift:**
Gör samma sak som Del A men använd moderna CSS-baserade selektorer.

**Steg:**

1. Använd samma HTML-struktur
2. Använd istället:
   - `document.querySelector('#myDiv')` → hitta div-elementet
   - `document.querySelectorAll('li')` → hitta alla li-element
   - `document.querySelectorAll('.myClass')` → hitta alla element med klassen

**Varför moderna selektorer?**

- Mer flexibla (använder CSS-syntax)
- Bättre prestanda
- Enklare att läsa och förstå

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="myDiv">Users:</div>
    <ul>
      <li>John</li>
      <li>Pete</li>
    </ul>
    <h4 class="myClass">These were all the users</h4>
    <p class="myClass">Thanks for checking in</p>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Tips:**

- `querySelector()` använder CSS-selektorer: `#id`, `.class`, `tagname`
- `querySelectorAll()` returnerar en NodeList som du kan loopa igenom

---

## Övning 2 - Avancerad Element Selection

**Mål:** Träna på att navigera i komplexa HTML-strukturer och använda olika selektorstrategier.

**Förväntat resultat:** Du kommer att kunna hitta element i kapslade strukturer och förstå när du ska använda olika selektorer.

**Uppgift:**
Skapa JavaScript-kod för att hitta följande element i den komplexa HTML-strukturen:

**Element att hitta:**

1. **Tabellen** med `id="age-table"`
2. **Alla label-element** inuti tabellen (ska vara 3 stycken)
3. **Första td-elementet** i tabellen (med texten "Age")
4. **Formuläret** med `name="search"`
5. **Första input-elementet** i det formuläret
6. **Sista input-elementet** i det formuläret

**Bonus-utmaning:**

- Hitta alla input-element med `name` som börjar med "info"
- Räkna antalet radio buttons i formuläret

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <body>
    <form name="search">
      <label
        >Search the site:
        <input type="text" name="search" />
      </label>
      <input type="submit" value="Search!" />
    </form>

    <hr />

    <form name="search-person">
      Search the visitors:
      <table id="age-table">
        <tr>
          <td>Age:</td>
          <td id="age-list">
            <label>
              <input type="radio" name="age" value="young" />less than 18</label
            >
            <label>
              <input type="radio" name="age" value="mature" />18-50</label
            >
            <label>
              <input type="radio" name="age" value="senior" />more than
              50</label
            >
          </td>
        </tr>

        <tr>
          <td>Additionally:</td>
          <td>
            <input type="text" name="info[0]" />
            <input type="text" name="info[1]" />
            <input type="text" name="info[2]" />
          </td>
        </tr>
      </table>

      <input type="submit" value="Search!" />
    </form>

    <script>
      // Din kod här - hitta alla element enligt listan ovan
    </script>
  </body>
</html>
```

**Tips:**

- Använd `document.forms` för att hitta formulär
- `querySelector()` kan kombinera selektorer: `"table#age-table label"`
- `querySelectorAll()` + `[0]` och `[length-1]` för första/sista element

---

## Övning 3 - Data Attributes

**Mål:** Lära dig arbeta med HTML5 data-attribut.

**Uppgift:**

1. Hitta elementet med attributet `data-widget-name`
2. Skriv ut dess värde med `console.log()`
3. **Bonus:** Ändra värdet till något annat

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <body>
    <div data-widget-name="menu">Choose the genre</div>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Tips:**

- Använd `querySelector('[data-widget-name]')` för att hitta elementet
- Använd `.getAttribute('data-widget-name')` för att läsa värdet
- Använd `.setAttribute('data-widget-name', 'nytt-värde')` för att ändra

---

## Övning 4 - Styla Externa Länkar

**Mål:** Lära dig manipulera CSS-stilar med JavaScript baserat på villkor.

**Uppgift:**
Gör alla externa länkar orange genom att ändra deras `style`-egenskap.

**Definition av extern länk:**
En länk är extern om dess `href`-attribut innehåller `://`

**Steg för steg:**

1. Hämta alla `<a>`-element med `querySelectorAll()`
2. Loopa igenom dem med en `for`-loop
3. Kontrollera om `href`-attributet innehåller `://` (använd `.includes()`)
4. Om ja: sätt `style.color = 'orange'`

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <body>
    <a name="list">the list</a>
    <ul>
      <li><a href="http://google.com">http://google.com</a></li>
      <li><a href="/tutorial">/tutorial.html</a></li>
      <li><a href="local/path">local/path</a></li>
      <li><a href="ftp://ftp.com/my.zip">ftp://ftp.com/my.zip</a></li>
      <li><a href="http://nodejs.org">http://nodejs.org</a></li>
      <li><a href="http://internal.com/test">http://internal.com/test</a></li>
    </ul>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Resultat ska se ut så här:**
![Externa länkar i orange](https://github.com/abbjoafli/Programmering-1/blob/master/1.Javascript/%C3%B6vningar/DOM_2_4.PNG)

**Tips:**

- `element.href` ger dig href-attributets värde
- `string.includes('://')` returnerar `true` eller `false`
- `element.style.color = 'orange'` ändrar textfärgen

---

## Övning 5 - Tre sätt att koppla en knapp till en funktion

**Mål:** Lära dig de tre olika sätten att koppla ett klick-event till en funktion.

**Förväntat resultat:** Du kommer att förstå skillnaden mellan `onclick` i HTML, `onclick` i JavaScript och `addEventListener()`.

**Uppgift:**
Skapa 3 knappar och 3 funktioner. Varje funktion ska skriva ut ett eget meddelande till konsolen med `console.log()`. Varje knapp ska kopplas till sin funktion på ett **eget sätt**.

**Steg:**

1. **Knapp 1 – `onclick` direkt i HTML:**
   Skriv attributet `onclick="knapp1()"` direkt på `<button>`-elementet.
2. **Knapp 2 – Tilldela en funktion från JavaScript:**
   Hämta knappen med `querySelector()` och tilldela funktionen till dess `onclick`-egenskap: `knapp.onclick = knapp2;`
3. **Knapp 3 – `addEventListener()`:**
   Hämta knappen med `querySelector()` och koppla funktionen med `knapp.addEventListener('click', knapp3);`

**Vad ska hända:** När du klickar på respektive knapp ska rätt meddelande skrivas ut i konsolen, t.ex. "Knapp 1 klickad (onclick i HTML)".

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Tre sätt att koppla events</h1>

    <button id="btn1">Knapp 1</button>
    <button id="btn2">Knapp 2</button>
    <button id="btn3">Knapp 3</button>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Tips:**

- Vid sätt 2 och 3 skriver du funktionens namn **utan** parenteser (`knapp2`, inte `knapp2()`). Med parenteser körs funktionen direkt istället för vid klick.
- Om du tilldelar `onclick` en gång till skrivs den första funktionen över. Med `addEventListener()` kan du koppla flera funktioner till samma knapp.
- `addEventListener()` är det rekommenderade sättet, eftersom det håller isär HTML och JavaScript.

**Bonus:**
Koppla en andra funktion till knapp 3 med `addEventListener()` och se att båda körs. Försök sedan göra samma sak med `onclick` på knapp 2 – vad händer?

---

## Övning 6 - Event Handling (Klick-events)

**Mål:** Lära dig hur JavaScript reagerar på användarinteraktioner.

**Förväntat resultat:** Du kommer att förstå hur man skapar interaktiva webbsidor som svarar på användarens handlingar.

**Uppgift:**
Skapa en enkel interaktiv applikation med knappar som ändrar webbsidans utseende.

**Funktioner att implementera:**

1. **Knapp 1:** Ändra bakgrundsfärg till slumpmässig färg
2. **Knapp 2:** Visa/dölja en text
3. **Knapp 3:** Lägg till en ny listpunkt med aktuell tid

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .hidden {
        display: none;
      }
      .time-list {
        list-style: none;
        padding: 0;
      }
      .time-list li {
        background: #f0f0f0;
        margin: 5px 0;
        padding: 10px;
        border-radius: 5px;
      }
    </style>
  </head>
  <body>
    <h1>Interaktiv Webbsida</h1>

    <button id="colorBtn">Ändra bakgrundsfärg</button>
    <button id="toggleBtn">Visa/Dölj text</button>
    <button id="timeBtn">Lägg till tid</button>

    <p id="toggleText" class="hidden">Denna text kan visas och döljas!</p>

    <h3>Tidspunkter:</h3>
    <ul id="timeList" class="time-list"></ul>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Ledtrådar:**

- Använd `addEventListener('click', function)` för att lyssna på klick
- `Math.random()` för slumpmässiga färger
- `classList.toggle()` för att växla CSS-klasser
- `new Date()` för att få aktuell tid

---

## Övning 7 - Formulärhantering

**Mål:** Lära dig validera och hantera formulärdata med JavaScript.

**Förväntat resultat:** Du kommer att kunna skapa formulär med validering och dynamisk feedback.

**Uppgift:**
Skapa ett registreringsformulär med validering och dynamisk feedback.

**Valideringsregler:**

- Namn: minst 2 tecken
- E-post: måste innehålla @
- Lösenord: minst 6 tecken
- Bekräfta lösenord: måste matcha lösenord

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .error {
        color: red;
        border-color: red;
      }
      .success {
        color: green;
        border-color: green;
      }
      .feedback {
        margin-top: 5px;
        font-size: 14px;
      }
    </style>
  </head>
  <body>
    <h1>Registrering</h1>

    <form id="registerForm">
      <div>
        <label for="name">Namn:</label>
        <input type="text" id="name" name="name" required />
        <div class="feedback" id="nameFeedback"></div>
      </div>

      <div>
        <label for="email">E-post:</label>
        <input type="email" id="email" name="email" required />
        <div class="feedback" id="emailFeedback"></div>
      </div>

      <div>
        <label for="password">Lösenord:</label>
        <input type="password" id="password" name="password" required />
        <div class="feedback" id="passwordFeedback"></div>
      </div>

      <div>
        <label for="confirmPassword">Bekräfta lösenord:</label>
        <input
          type="password"
          id="confirmPassword"
          name="confirmPassword"
          required
        />
        <div class="feedback" id="confirmPasswordFeedback"></div>
      </div>

      <button type="submit">Registrera</button>
    </form>

    <div id="result"></div>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Ledtrådar:**

- Använd `addEventListener('input', function)` för realtidsvalidering
- `preventDefault()` för att stoppa formulärsubmit
- `value.length` för att kontrollera längd
- `includes('@')` för e-postvalidering

---

## Övning 8 - Dynamisk Innehåll

**Mål:** Lära dig skapa, modifiera och ta bort DOM-element dynamiskt.

**Förväntat resultat:** Du kommer att kunna bygga interaktiva listor och dynamiska användargränssnitt.

**Uppgift:**
Skapa en "To-Do Lista" där användare kan lägga till, markera som klar och ta bort uppgifter.

**Funktioner:**

- Lägg till nya uppgifter
- Markera uppgifter som klara (genomstrykning)
- Ta bort uppgifter
- Räkna antal uppgifter

**HTML-kod:**

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .todo-item {
        display: flex;
        align-items: center;
        padding: 10px;
        border: 1px solid #ddd;
        margin: 5px 0;
        border-radius: 5px;
      }
      .completed {
        text-decoration: line-through;
        opacity: 0.6;
      }
      .delete-btn {
        margin-left: auto;
        background: #ff4444;
        color: white;
        border: none;
        padding: 5px 10px;
        border-radius: 3px;
        cursor: pointer;
      }
      .add-section {
        margin-bottom: 20px;
      }
      .stats {
        margin-top: 20px;
        padding: 10px;
        background: #f0f0f0;
        border-radius: 5px;
      }
    </style>
  </head>
  <body>
    <h1>Min To-Do Lista</h1>

    <div class="add-section">
      <input
        type="text"
        id="newTask"
        placeholder="Lägg till ny uppgift..."
        maxlength="100"
      />
      <button id="addBtn">Lägg till</button>
    </div>

    <div id="todoList"></div>

    <div class="stats">
      <p>Totalt: <span id="totalTasks">0</span> uppgifter</p>
      <p>Klar: <span id="completedTasks">0</span> uppgifter</p>
    </div>

    <script>
      // Din kod här
    </script>
  </body>
</html>
```

**Ledtrådar:**

- `createElement()` för att skapa nya element
- `appendChild()` för att lägga till element
- `removeChild()` för att ta bort element
- `classList.toggle()` för att växla CSS-klasser
- `textContent` för att sätta textinnehåll

---

## Sammanfattning

**DOM-selektorer** - Hitta element med olika metoder  
**Element-manipulation** - Ändra innehåll, stilar och attribut  
**Event handling** - Reagera på användarinteraktioner  
**Formulärvalidering** - Validera användarinput  
**Dynamiskt innehåll** - Skapa interaktiva användargränssnitt
