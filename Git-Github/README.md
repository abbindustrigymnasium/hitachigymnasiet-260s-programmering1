# Git & GitHub

Git och GitHub är grundläggande verktyg för modern mjukvaruutveckling. I denna guide lär du dig både **terminal-kommandon** och hur du använder **Visual Studio Code** för Git-operationer.

## Snabbstart

### Viktiga resurser

- [Microsoft Learn: Git & GitHub med VS Code](https://docs.microsoft.com/en-us/learn/modules/introduction-to-github-visual-studio-code/)
- [VS Code Git-funktioner](https://vscode.github.com/)
- [GitHub Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) (obligatoriskt från 2021)

### VS Code Extensions (Rekommenderas starkt)

Installera dessa tillägg i Visual Studio Code:

- **GitLens** - Förbättrad Git-visualisering
- **Git History** - Visa Git-historik
- **GitHub Pull Requests and Issues** - GitHub-integration

---

## Introduktion

Denna guide ger dig en praktisk introduktion till Git och GitHub med fokus på två arbetsmetoder:

- **Terminal/Kommandorad** - Kraftfull och precis kontroll
- **Visual Studio Code** - Grafisk och användarvänlig interface

**Fördjupning:** [Pro Git (gratis bok)](https://git-scm.com/book/en/v2) för djupare förståelse.

## Vad är Git & GitHub?

### Git - Versionhanteringssystem

**Git** är ett distribuerat versionhanteringssystem som låter dig:

- **Spåra ändringar** i dina filer över tid
- **Gå tillbaka** till tidigare versioner
- **Samarbeta** med andra utvecklare
- **Hantera olika versioner** (branches) parallellt
- **Se vem som ändrat vad** och när

**Historik:** Git skapades av **Linus Torvalds** (Linux-skaparen) för att hantera utvecklingen av Linux-kärnan.

### GitHub - Cloud-plattform för Git

**GitHub** är en webbaserad tjänst som ger dig:

- **Molnlagring** för dina Git-repositories
- **Samarbetsverktyg** (Issues, Pull Requests, Discussions)
- **Kodgranskning** och projekthantering
- **Portfoliovisning** - ditt "CV för kod"
- **Automation** med GitHub Actions
- **Dokumentation** med GitHub Pages

**Tänk på GitHub som** "Facebook för kod" - en social plattform där utvecklare delar, samarbetar och bygger på varandras projekt.

## Varför vill vi att du använder Git och GitHub?

- Först och främst kommer Git och GitHub vara något du med säkerhet kommer stöta på i ditt kommande arbetsliv.

- Ditt GitHub-konto kommer fungera som ett CV där du samlar dina projekt och där eventuella arbetsgivare kan se vad du kan och har producerat tidigare. Detta är något vi märker fler och fler arbetsgivare tycker är viktigt så att redan från början bygga upp sitt GitHubkonto bör vara en viktig punkt i din utveckling.

- Du kommer enklare kunna hantera dina filer. Inga datorkrasher kommer få dina filer att försvinna (om du är noga med att synka dina filer med GitHub). Du kan också komma åt dina filer från flera olika datorer och enheter.

- Du kan enkelt dela dina filer med dina lärare. Vid examinering av t.ex. koduppgifter vill läraren titta på din kod och kan då via GitHub enkelt komma åt denna. Vid t.ex. frågor kring eller problem med din kod kan läraren enkelt komma åt den senaste versionen.

- I vissa kurser kommer ni att arbeta i grupper och GitHub ger en bra möjlighet att sammarbeta i mjukvaruprojekt.

- GitHub är ett kraftfullt verktyg för att studera och lära sig av andras kod.

- Läraren kan följa dina versioner och se hur du ligger till i kursen.

- GitHub har också ett system för att skriva kommentarer, ToDo-listor m.m som underlättar vid arbetsgången.

---

## Viktig terminologi

### Grundläggande begrepp

| Begrepp               | Förklaring                                        | VS Code motsvarighet                   |
| --------------------- | ------------------------------------------------- | -------------------------------------- |
| **Repository (repo)** | Ett projekt/mapp med versionshanterade filer      | Mapp som öppnas i VS Code med Git-stöd |
| **Commit**            | Spara en ögonblicksbild av dina ändringar lokalt  | Source Control-panelen (Ctrl+Shift+G)  |
| **Push**              | Skicka commits till GitHub-servern                | "Sync Changes" eller Push-knappen      |
| **Pull**              | Hämta ändringar från GitHub-servern               | "Sync Changes" eller Pull-knappen      |
| **Clone**             | Kopiera ett repository från GitHub till din dator | Command Palette: `Git: Clone`          |

### Avancerade begrepp

| Begrepp               | Förklaring                                              | VS Code motsvarighet                       |
| --------------------- | ------------------------------------------------------- | ------------------------------------------ |
| **Branch**            | Parallell utvecklingslinje (t.ex. ny funktion)          | Branch-växlare i statusraden               |
| **Merge**             | Slå samman två branches                                 | Command Palette: `Git: Merge Branch`       |
| **Fork**              | Kopiera någon annans projekt till ditt GitHub-konto     | GitHub-webbsidan                           |
| **Pull Request (PR)** | Föreslå ändringar till ett projekt                      | GitHub Pull Requests extension             |
| **Staging**           | Välja vilka ändringar som ska inkluderas i nästa commit | "+" knappen bredvid filer i Source Control |

## Kort video serie som beskriver hur man jobbar med Visual Studio Code och Github (Rekommenderas starkt!).

<https://www.youtube.com/playlist?list=PLpPVLI0A0OkLBWbcctmGxxF6VHWSQw1hi><br>

Lägg till två extensions till Visual Studio Code:<br>

**Git History** och **Git Easy**

## Kom igång med GitHub

Det första Du bör göra är att skapa dig ett konto på GitHub. Här är det viktigt att du registrar dig med din studentmejl från Hitachi Industrigymnasium.

Fyll i formuläret som nedan fast med ditt eget användarnamn och e-post.
![Github Signup](https://github.com/abbjoafli/Programmering-1/blob/master/Git-Github/Github_SignUp.PNG)


## Övning Praktisk Git-användning

I denna sektion lär du dig Git på **två sätt**:

- **Terminal** - Kraftfull och precis kontroll
- **VS Code** - Visuell och användarvänlig

**Rekommendation:** Lär dig båda metoderna. Terminal ger djupare förståelse, VS Code är snabbare för dagligt arbete.

Du ska klona det här repositorit från Github Classroom. Du kommer använda det för att göra övningar i JavaScript, HTML och CSS.

---

## Grundläggande Git-workflow

### 1. Klona repositorit från Github Classroom

#### Terminal

```bash
# Klona från GitHub
git clone https://github.com/username/repository-name.git

# Gå in i mappen
cd repository-name
```

#### VS Code

1. **Command Palette** (`Ctrl+Shift+P`)
2. Skriv `Git: Clone`
3. Klistra in repository-URL
4. Välj lokal mapp
5. Öppna i VS Code

### 2. Kontrollera status

#### Terminal

```bash
# Se status för alla filer
git status

# Se ändringar i detalj
git diff
```

#### VS Code

- **Source Control panel** (`Ctrl+Shift+G`)
- Modifierade filer visas med **M**
- Nya filer visas med **U** (untracked)
- Klicka på fil för att se ändringar

### 3. Lägg till filer (Stage)

#### Terminal

```bash
# Lägg till en specifik fil
git add filename.txt

# Lägg till alla ändringar
git add .

# Lägg till alla filer av en typ
git add *.html
```

#### VS Code

- Klicka **+** bredvid fil i Source Control
- Eller högerklicka → "Stage Changes"
- "+" bredvid "Changes" för att stage alla

### 3.1 Ta bort från staging (Reset)

#### Terminal

```bash
# Ta bort en fil från staging
git reset HEAD filename.txt

# Ta bort alla filer från staging
git reset HEAD

# Ta bort alla filer från staging (modern syntax)
git restore --staged .
```

#### VS Code

- Klicka **-** bredvid fil i Source Control
- Eller högerklicka → "Unstage Changes"

### 4. Commit (spara ändringar)

#### Terminal

```bash
# Commit med meddelande
git commit -m "Beskrivning av ändringar"

# Commit och lägg till automatiskt
git commit -am "Beskrivning av ändringar"
```

#### VS Code

1. Skriv commit-meddelande i textrutan
2. Klicka **Commit** (`Ctrl+Enter`)
3. Eller **Commit & Push** för att göra båda

### 5. Skicka till GitHub (Push)

#### Terminal

```bash
# Skicka till GitHub
git push

# Första gången (sätt upstream)
git push -u origin main
```

#### VS Code

- Klicka **Sync Changes** i Source Control
- Eller **Push**-knappen i statusraden
- Eller Command Palette: `Git: Push`

### 6. Hämta ändringar (Pull)

#### Terminal

```bash
# Hämta senaste ändringar
git pull

# Hämta utan att merge
git fetch
```

#### VS Code

- Klicka **Sync Changes** i Source Control
- Eller **Pull**-knappen i statusraden
- Eller Command Palette: `Git: Pull`

---

## Arbeta med Branches

Branches låter dig arbeta på nya funktioner utan att påverka huvudkoden.

### Skapa och växla branch

#### Terminal

```bash
# Visa alla branches
git branch

# Skapa ny branch
git branch feature-name

# Växla till branch
git checkout feature-name

# Skapa och växla i ett kommando
git checkout -b feature-name

# Modern syntax (Git 2.23+)
git switch -c feature-name
```

#### VS Code

1. Klicka på branch-namn i **statusraden** (längst ner)
2. Välj "Create new branch"
3. Ange branch-namn
4. Eller **Command Palette**: `Git: Create Branch`

### Merge branches

#### Terminal

```bash
# Växla till main
git checkout main

# Merge feature-branch
git merge feature-name

# Ta bort branch efter merge
git branch -d feature-name
```

#### VS Code

1. **Command Palette**: `Git: Merge Branch`
2. Välj branch att merge från
3. Eller högerklicka på branch i Git History

---

## GitHub-specifika funktioner

### Personal Access Token (2024)

GitHub kräver inte längre lösenord för Git-operationer. Använd istället:

1. **GitHub.com** → Settings → Developer settings → Personal access tokens
2. Generera ny token med rätt behörigheter
3. Använd token istället för lösenord

### GitHub CLI (moderna alternativet)

```bash
# Installera GitHub CLI
# Windows: winget install GitHub.cli
# macOS: brew install gh

# Logga in
gh auth login

# Klona med gh
gh repo clone username/repo-name

# Skapa repository
gh repo create my-new-repo
```