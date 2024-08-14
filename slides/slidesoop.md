# Objektorienteret programmering i Python
- Introduktion til det objektorienterede paradigme
- Klasser og objekter samt forskellen på disse
- Konstruktører og destruktører
- Attributter og metoder
- Dunder metoder
- Principperne bag objektorienteret programmering
- Indkapsling
- Nedarvning
- Polymorfi
- Abstrakte klasser og metoder


# Introduktion til objektorienteret paradigme
- Objektorienteret programmering (OOP) er et meget anvendt programmeringsparadigme (dvs. en måde at tænke)
- En måde at strukturere og designe programmer på så det er nemmere at forstå og vedligeholde
- Hovedideen er at tænke i objekter, som indeholder data og metoder
er bygger på konceptet om objekter, som kan indeholde data i form af attributter og metoder. 
- Fundamentale begreber i OOP er klasser og objekter
- Objekter er konkrete instanser af klasser, som er skabeloner for objekter. 
- Klasser er en slags skabelon for objekter, som indeholder attributter og metoder

# Et eksempel på hvorfor objektorienteret programmering er smart
Forestil dig at du skal lave et program, som skal håndtere vektorer i et 2D rum.
Uden klasser og objekter kunne du lave en liste med to elementer, som repræsenterer x- og y-koordinaterne: 
```python
xkomponent = 3
ykomponent = 4

print("Vektoren har en x-komponent på", xkomponent, "og en y-komponent på", ykomponent)

# Beregning af vektorlængde
længde = (xkomponent**2 + ykomponent**2)**0.5
print("Vektorlængden er", længde)
```
Hvad er ulempen ved denne løsning hvis vi bruger vektorer mange steder i programmet?
Hvor mange linjer kode skal vi skrive for at lave en ny vektor og printe vektorlængden samt koordinaterne? Hvad med fejlhåndtering og flere der arbejder på samme kode?

# En bedre løsning med klasser og objekter
```python
class Vektor:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def længde(self):
        return (self.x**2 + self.y**2)**0.5

    def __str__(self):
        return f"Vektoren har en x-komponent på {self.x} og en y-komponent på {self.y}"
```
Her har vi defineret en klasse `Vektor`, som har tre metoder: init, længde og str.
- `__init__` er en konstruktør, som initialiserer objektet med x- og y-koordinaterne
- `længde` er en metode, som beregner vektorlængden
- `__str__` er en metode, som returnerer en strengrepræsentation af objektet

# Brug af klassen Vektor
```python
v = Vektor(3, 4)
print(v)
print("Vektorlængden er", v.længde())
```
Her har vi skabt en instans `v` af klassen `Vektor` med x- og y-koordinaterne 3 og 4.
Vi har derefter printet vektoren og beregnet vektorlængden.

Tænk på hvor mange linjers kode og hvor meget gentagelse vi har sparet ved at bruge klasser og objekter!


# Øvelser
1. Udvid klassen `Vektor` med en metode `add`, som tager en anden vektor som argument og returnerer en ny vektor, som er summen af de to vektorer.
2. Udvid klassen `Vektor` med en metode `skalar_mult`, som tager en skalar som argument og returnerer en ny vektor, som er skalarproduktet af vektoren og skalaren.
3. Udvid klassen `Vektor` med en metode `vinkel`, som tager en anden vektor som argument og returnerer vinklen mellem de to vektorer.
4. Udvid klassen `Vektor` med en attribut navn, som er en streng, der beskriver vektoren. Skriv en metode `__str__`, som returnerer denne strengrepræsentation af vektoren.
5. Udvid klassen med en metode til at beregne prikproduktet af to vektorer


# Klasser og objekter
- En klasse er en skabelon for objekter, som indeholder attributter og metoder
- Attributter er data, som objektet indeholder. F.eks. x- og y-koordinater for en vektor
- Metoder er funktioner, som objektet kan udføre. F.eks. beregning af vektorlængde.
- Objekter er konkrete instanser af klasser
- Objekter har adgang til attributter og metoder i klassen

# Forskellen på klasser og objekter
- En klasse er en skabelon for objekter, som indeholder attributter og metoder
- Objekter er konkrete instanser af klasser, som indeholder data og metoder
- Klasser definerer objekter, mens objekter er instanser af klasser
- Tænk på klasser som en opskrift på en kage og objekter som de kager, som du bager ud fra opskriften

# Konstruktører og destruktører
- En konstruktør er en metode, som initialiserer objektet
- I Python hedder konstruktøren `__init__`
- En destruktør er en metode, som rydder op efter objektet
- I Python hedder destruktøren `__del__`

# Eksempel på konstruktør og destruktør
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        print("Objektet er blevet initialiseret")

    def __del__(self):
        print("Objektet er blevet slettet")
```

# Eksempel på klasse med flere konstruktører
```python
class Vector:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y
        print("Objektet er blevet initialiseret")
    
    def __init__(self, x, y, navn):
        self.x = x
        self.y = y
        self.navn = navn
        print("Objektet er blevet initialiseret")
```
Bemærk lighedstegnet i `def __init__(self, x=0, y=0):`, som angiver defaultværdier for x og y hvis ikke andet er angivet.

# Instanser af klassen vektor
```python
v1 = Vector(3, 4)
v2 = Vector(5, 6, "v2")
v3 = Vector()
```
Hvad sker der når vi kører koden?
Hvad er forskellen på v1, v2 og v3?
Hvad er attributterne her?

# Attributter
- Attributter er data, som objektet indeholder
- Attributter er tilgængelige for alle metoder i klassen
- Attributter kan være enten klasseattributter eller instansattributter
- Klasseattributter er fælles for alle instanser af klassen
- Instansattributter er unikke for hver instans af klassen

# Eksempel på klasseattribut
```python
class Vector:
    antal_vektorer = 0

    def __init__(self, x, y):
        self.x = x
        self.y = y
        Vector.antal_vektorer += 1
```
Her har vi defineret en klasseattribut `antal_vektorer`, som tæller antallet af instanser af klassen `Vector`. Denne attribut er fælles for alle instanser af klassen.
Tilgentæld er x og y instansattributter, som er unikke for hver instans af klassen.

# Navngivning af attributter, metoder og klasser
- Attributter, metoder og klasser bør navngives med sigende navne, som beskriver deres formål
- Attributter bør navngives med små bogstaver og understregninger imellem ordene (snake_case)
- Metoder bør navngives med små bogstaver og understregninger imellem ordene (snake_case)
- Klasser bør navngives med store bogstaver og ingen understregninger imellem ordene (CamelCase)

# Øvelser om attributter
1. Tilføj en klasseattribut `antal_vektorer` til klassen `Vector`, som tæller antallet af instanser af klassen.
2. Tilføj en instansattribut `navn` til klassen `Vector`, som er en streng, der beskriver vektoren.
3. Skriv en metode `__str__`, som returnerer en strengrepræsentation af vektoren, som indeholder vektorens navn og koordinater.
4. Udvid med en attribut `farve`, som er en streng, der beskriver vektorens farve. Skriv en metode `farve`, som returnerer vektorens farve.

# Øvelser om navngivning
1. Skriv en klasse `Bil`, som har attributterne `model`, `farve` og `årgang`. Skriv en metode `__str__`, som returnerer en strengrepræsentation af bilen.
2. Skriv en klasse `Person`, som har attributterne `navn`, `alder` og `køn`. Skriv en metode `__str__`, som returnerer en strengrepræsentation af personen.
3. Skriv en klasse `Hund`, som har attributterne `navn`, `race` og `alder`. Skriv en metode `__str__`, som returnerer en strengrepræsentation af hunden.

# Øvelse om linje segment
1. Skriv en klasse `LinjeSegment`, som har attributterne `start` og `slut`, som er instanser af klassen `Vector`. Skriv en metode `længde`, som returnerer længden af linjesegmentet.
2. Skriv en metode `__str__`, som returnerer en strengrepræsentation af linjesegmentet.
3. Skriv en metode `vinkel`, som returnerer vinklen mellem linjesegmentet og x-aksen.
4. Skriv en metode som finder midtpunktet af linjesegmentet

# Metoder
- Metoder er funktioner, som objektet kan udføre
- Metoder defineres på samme måde som
- Metoder har adgang til objektets attributter
- Metoder kan tage argumenter på samme måde som funktioner
- Metoder kan returnere værdier på samme måde som funktioner

Vi kan tænke på metoder som funktioner, som er bundet til objekter og kan udføre operationer på objektets attributter, og dermed ændre objektets tilstand.

# Eksempel på metode
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def længde(self):
        return (self.x**2 + self.y**2)**0.5
```
Her har vi defineret en metode `længde`, som beregner vektorlængden af vektoren.

# Eksempel på brug af metode
```python
v = Vector(3, 4)
print(v.længde())
```
Her har vi skabt en instans `v` af klassen `Vector` med x- og y-koordinaterne 3 og 4.
Vi har derefter kaldt metoden `længde` på objektet `v` og printet resultatet.

# Øvelser om metoder på vektorer
1. Skriv en metode `sub`, som tager en anden vektor som argument og returnerer en ny vektor, som er summen af de to vektorer.
2. Skriv en metode `enheds_vektor`, som tager en anden vektor som argument og returnerer en enhedsvektor i samme retning som vektoren.
3. Skriv en metode `vinkel`, som tager en anden vektor som argument og returnerer vinklen mellem de to vektorer.


# Principperne bag objektorienteret programmering
- Objektorienteret programmering bygger på fire grundprincipper: indkapsling, nedarvning, polymorfi og abstraktion (og til dels komposition)
- Indkapsling handler om at skjule data og metoder i klassen, så de ikke er tilgængelige udefra
- Nedarvning handler om at lade en klasse arve attributter og metoder fra en anden klasse
- Polymorfi handler om at lade en metode opføre sig forskelligt afhængigt af objektets type
- Abstraktion handler om at fokusere på det væsentlige og skjule detaljerne

# Indkapsling
- Indkapsling handler om at skjule data og metoder i klassen, så de ikke er tilgængelige udefra
- Attributter bør være private, dvs. ikke tilgængelige udefra. 
- Metoder bør være offentlige, dvs. tilgængelige udefra
- Ved at gøre attributter private kan vi sikre, at de kun ændres på en kontrolleret måde
- Ved at gøre metoder offentlige kan vi sikre, at objektets tilstand ændres på en kontrolleret måde

# Eksempel på indkapsling
Vi kan gøre attributter private ved at tilføje dobbelt underscore foran attributnavnet:

```python
class Vector:
    def __init__(self, x, y):
        self.__x = x
        self.__y = y

    def længde(self):
        return (self.__x**2 + self.__y**2)**0.5
```
Her er attributterne `x` og `y` blevet gjort private ved at tilføje dobbelt underscore foran attributnavnet.

# Eksempel på brug af private attributter
```python
v = Vector(3, 4)
print(v.__x) # Dette vil give en fejl, da attributtet er private
```
Her forsøger vi at tilgå attributtet `__x` udefra, hvilket vil give en fejl, da attributtet er private. 

# Hvordan kan vi tilgå private attributter?
- Vi kan tilgå private attributter ved at bruge getter- og setter-metoder
- Getter-metoder bruges til at hente værdien af attributter
- Setter-metoder bruges til at ændre værdien af attributter

# Eksempel på getter- og setter-metoder
```python
class Vector:
    def __init__(self, x, y):
        self.__x = x
        self.__y = y

    def get_x(self):
        return self.__x

    def set_x(self, x):
        self.__x = x
```
Her har vi defineret getter- og setter-metoder for attributtet `__x`.

# Eksempel på brug af getter- og setter-metoder
```python
v = Vector(3, 4)
print(v.get_x()) # Dette vil give 3
v.set_x(5)
print(v.get_x()) # Dette vil give 5
```
Her har vi skabt en instans `v` af klassen `Vector` med x- og y-koordinaterne 3 og 4.
Vi har derefter brugt getter- og setter-metoderne til at tilgå og ændre attributtet `__x`.

# Fordelene ved getter- og setter-metoder (indkapsling)
Fordelene ved at bruge getter- og setter-metoder er, at vi kan kontrollere, hvordan attributterne ændres og læses, og dermed sikre, at objektets tilstand ændres på en kontrolleret måde. 
- Vi kan f.eks. validere input, før det gemmes i attributtet. 
- Og vi kan sikre, at attributterne ikke ændres udefra.
- Vi kan også ændre attributtets repræsentation, f.eks. ved at ændre fra meter til kilometer.
- Vi kan også lave lazy loading, dvs. først hente data, når det er nødvendigt.
- Vi kan også lave logging, dvs. logge, hvornår attributtet ændres.
- Vi ved at attributterne kun kan ændres et sted i koden, hvilket gør det lettere at fejlfinde.

# Øvelser om indkapsling
1. Tilføj getter- og setter-metoder for attributterne `__x` og `__y` i klassen `Vector`.
2. Tilføj en klasseattribut `antal_vektorer` til klassen `Vector`, som tæller antallet af instanser af klassen. Tilføj getter- og setter-metoder for denne attribut.
3. Tilføj en instansattribut `navn` til klassen `Vector`, som er en streng, der beskriver vektoren. Tilføj getter- og setter-metoder for denne attribut.
4. Tilføj en attribut `farve`, som er en streng, der beskriver vektorens farve. Tilføj getter- og setter-metoder for denne attribut.

# Kan metoder være private?
- Ja, metoder kan også være private
- Private metoder er metoder, som kun kan tilgås indefra klassen
- Private metoder kan bruges til at udføre interne operationer, som ikke er meningsfulde at kalde udefra

# Eksempel på privat metode
```python
class Vector:
    def __init__(self, x, y):
        self.__x = x
        self.__y = y

    def __beregn_længde(self):
        return (self.__x**2 + self.__y**2)**0.5
```
Her har vi defineret en privat metode `__beregn_længde`, som beregner vektorlængden af vektoren.

# Eksempel på brug af privat metode
```python
v = Vector(3, 4)
print(v.__beregn_længde()) # Dette vil give en fejl, da metoden er private
```
Her forsøger vi at tilgå den private metode `__beregn_længde` udefra, hvilket vil give en fejl, da metoden er private.

# Øvelser om private metoder
1. Tilføj en privat metode `__beregn_vinkel`, som beregner vinklen mellem vektoren og x-aksen.
2. Tilføj en privat metode `__beregn_skalarprodukt`, som beregner skalarproduktet af vektoren og en anden vektor.
3. Tilføj en privat metode `__beregn_prikprodukt`, som beregner prikproduktet af vektoren og en anden vektor.
4. Overvej hvilke metoder der bør være private og offentlige i klassen `Vector`.

# Dunder metoder
- Dunder metoder er specielle metoder, som har dobbelt underscore foran og bagved metodenavnet
- Dunder metoder bruges til at ændre objektets adfærd, når det interagerer med Python's indbyggede funktioner
- F.eks. `__init__` bruges til at initialisere objektet, `__str__` bruges til at returnere en strengrepræsentation af objektet, `__add__` bruges til at tilføje to objekter

# Eksempel på dunder metode
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Vektoren har en x-komponent på {self.x} og en y-komponent på {self.y}"
```
Her har vi defineret en dunder metode `__str__`, som returnerer en strengrepræsentation af vektoren.

# Eksempel på brug af dunder metode
```python
v = Vector(3, 4)
print(v) # Dette vil give "Vektoren har en x-komponent på 3 og en y-komponent på 4"
```
Her har vi skabt en instans `v` af klassen `Vector` med x- og y-koordinaterne 3 og 4.
Vi har derefter printet vektoren, hvilket vil kalde dunder metoden `__str__`.

# Eksempel på flere dunder metoder
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Vektoren har en x-komponent på {self.x} og en y-komponent på {self.y}"

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
```

Her har vi defineret en dunder metode `__add__`, som tilføjer to vektorer sammen.

# Eksempel på brug af flere dunder metoder
```python
v1 = Vector(3, 4)
v2 = Vector(5, 6)
v3 = v1 + v2
print(v3) # Dette vil give "Vektoren har en x-komponent på 8 og en y-komponent på 10"
```

# Øvelser om dunder metoder
1. Tilføj en dunder metode `__sub__`, som trækker to vektorer fra hinanden.
2. Tilføj en dunder metode `__mul__`, som ganger en vektor med en skalar.
3. Tilføj en dunder metode `__truediv__`, som dividerer en vektor med en skalar.
4. Tilføj en dunder metode `__eq__`, som sammenligner to vektorer for ligehed.



# Nedarvning
- Nedarvning handler om at lade en klasse arve attributter og metoder fra en anden klasse
- Den klasse, som arver, kaldes en underklasse eller subklasse
- Den klasse, som bliver arvet fra, kaldes en superklasse eller baseklasse
- Nedarvning gør det muligt at genbruge kode og undgå gentagelse
- Nedarvning gør det muligt at opdele store klasser i mindre og mere overskuelige klasser

# Formel definition af nedarvning
```python
class SuperKlasse:
    # Superklasse attributter og metoder

class UnderKlasse(SuperKlasse):
    # Underklasse attributter og metoder
```
Her har vi defineret en superklasse `SuperKlasse` og en underklasse `UnderKlasse`, som arver fra superklassen. Alle attributter og metoder fra superklassen er tilgængelige i underklassen.

# Eksempel på nedarvning i vector klassen
```python
class Vector:
    def __init__(self, x, y):
        self.__x = x
        self.__y = y

    def længde(self):
        return (self.__x**2 + self.__y**2)**0.5

class EnhedsVektor(Vector):
    def __init__(self, x, y):
        super().__init__(x, y)
        længde = super().længde()
        self.__x = x / længde
        self.__y = y / længde
```

# Betydningen af super()
- super() bruges til at henvise til superklassen
- super() bruges til at kalde metoder fra superklassen
- super() bruges til at initialisere superklassen i underklassen
- super() bruges til at undgå gentagelse af kode

# Eksempel på brug af underklasse
```python
v = EnhedsVektor(3, 4)
print(v.længde()) # Dette vil give 1
```
Her har vi skabt en instans `v` af klassen `EnhedsVektor` med x- og y-koordinaterne 3 og 4.
Vi har derefter kaldt metoden `længde` på objektet `v` og printet resultatet.

# Øvelser om nedarvning
1. Lav en person klasse med attributterne navn, alder og køn. Lav en underklasse studerende, som arver fra person klassen og har attributterne studienummer og f
2. Lav en klasse `Dyr` med attributterne `navn`, `race` og `alder`. Lav en underklasse `Hund`, som arver fra `Dyr` og har attributterne `vægt` og `farve`.
3. Lav en klasse `Figur` med attributterne `farve` og `areal`. Lav en underklasse `Cirkel`, som arver fra `Figur` og har attributterne `radius` og `omkreds`.

# Øvelser om nedarvning på vektorklassen
- Lav en underklasse `Vektor3D`, som arver fra `Vector` og har en z-koordinat
- Lav en metode `længde`, som beregner vektorlængden i 3D
- Lav en metode `krydsprodukt`, som beregner krydsproduktet af to 3D vektorer
- Lav en metode `vinkel`, som beregner vinklen mellem to 3D vektorer

# Flere niveauer af nedarvning
- Nedarvning kan have flere niveauer, dvs. en underklasse kan have en underklasse
- Nedarvning kan have flere superklasser, dvs. en klasse kan arve fra flere klasser
- Nedarvning kan have flere niveauer og flere superklasser samtidig

# Eksempel på flere niveauer af nedarvning
```python
class A:
    pass

class B(A):
    pass

class C(B):
    pass
```
Her har vi defineret tre klasser `A`, `B` og `C`, hvor `C` arver fra `B`, som arver fra `A`. pass betyder, at klassen ikke har nogen attributter eller metoder.


# Eksempel på flere superklasser
```python
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

Her har vi defineret tre klasser `A`, `B` og `C`, hvor `C` arver fra både `A` og `B`. Dette kaldes multiple inheritance.

# Øvelser om flere niveauer af nedarvning
1. Lav en klasse `Dyr` med attributterne `navn`, `race` og `alder`. Lav en underklasse `Hund`, som arver fra `Dyr` og har attributterne `vægt` og `farve`. Lav en underklasse `Schæfer`, som arver fra `Hund` og har attributterne `lydstyrke` og `hvalpe`.
2. Lav en klasse `Figur` med attributterne `farve` og `areal`. Lav en underklasse `Cirkel`, som arver fra `Figur` og har attributterne `radius` og `omkreds`. Lav en underklasse `FyldtCirkel`, som arver fra `Cirkel` og har attributten `fyldt`.
3. Lav en person klasse med attributterne navn, alder og køn. Lav en underklasse studerende, som arver fra person klassen og har attributterne studienummer. Lav en underklasse `PhDStuderende`, som arver fra `studerende` og har attributterne `afhandling` og `vejleder`.

# Polymorfi
Poly betyder mange og morfi betyder form. Polymorfi betyder mange former.
Polymorfi handler om at lade en metode opføre sig forskelligt afhængigt af objektets type
- Polymorfi gør det muligt at 
- bruge samme metode på forskellige objekter
- skjule detaljerne i implementeringen og fokusere på det væsentlige
- opnå fleksibilitet og genbrugelighed

# Eksempel på polymorfi på vektorer
Først indlæser vi en række vektorer og enhedsvektorer i en liste:
```python
vektorer = [Vector(3, 4), EnhedsVektor(3, 4)]
```
Derefter kan vi iterere over listen og kalde metoden `længde` på hvert objekt:
```python
for v in vektorer:
    print(v.længde())
```
Her vil metoden `længde` opføre sig forskelligt afhængigt af objektets type, da `EnhedsVektor` klassen overskriver metoden `længde`.

Vi kan med fordel bruge polymorfi, når vi har en liste af objekter, som har en fælles metode. Dette gør det muligt at bruge samme metode på forskellige objekter og skjule detaljerne i implementeringen.

# Øvelser om polymorfi
1. Lav en klasse `Dyr` med metoden `lyd`, som returnerer dyrets lyd. Lav en underklasse `Hund`, som overskriver metoden `lyd` og returnerer `vov`. Lav en underklasse `Kat`, som overskriver metoden `lyd` og returnerer `mjau`.
2. Lav en klasse `Figur` med metoden `areal`, som returnerer figurens areal. Lav en underklasse `Cirkel`, som overskriver metoden `areal` og returnerer `pi * radius**2`. Lav en underklasse `Firkant`, som overskriver metoden `areal` og returnerer `længde * bredde`.
3. Lav en klasse `Person` med metoden `beskriv`, som returnerer personens navn og alder. Lav en underklasse `Studerende`, som overskriver metoden `beskriv` og returnerer personens navn, alder og studienummer.


# Abstrakte klasser og metoder
- En abstrakt klasse er en klasse, som ikke kan instantieres
- En abstrakt metode er en metode, som ikke har en implementering
- Abstrakte klasser og metoder bruges til at definere et interface, som andre klasser kan arve fra
- Abstrakte klasser og metoder bruges til at sikre, at alle underklasser implementerer en bestemt metode

# Eksempel på abstrakt klasse og metode
Først importerer vi modulet abc og definerer en abstrakt klasse `Figur` med en abstrakt metode `areal`:
```python
from abc import ABC, abstractmethod

class Figur(ABC):
    @abstractmethod
    def areal(self):
        pass
```

Derefter definerer vi en underklasse `Cirkel`, som arver fra `Figur` og implementerer metoden `areal`:
```python
class Cirkel(Figur):
    def __init__(self, radius):
        self.radius = radius

    def areal(self):
        return 3.14 * self.radius**2
```

# Eksempel på brug af abstrakt klasse og metode
Først opretter vi en instans af klassen `Cirkel` og kalder metoden `areal`:
```python
cirkel = Cirkel(5)
print(cirkel.areal())
```
Her vil metoden `areal` i klassen `Cirkel` blive kaldt, da klassen arver fra `Figur` og implementerer metoden `areal`.

# Øvelser om abstrakte vektorklasser
1. Lav en abstrakt klasse `Vektor` med en abstrakt metode `længde`, som returnerer vektorlængden. Lav en underklasse `Vektor2D`, som arver fra `Vektor` og implementerer metoden `længde`.
2. Udvid klassen `Vektor2D` med en abstrakt metode `vinkel`, som returnerer vinklen mellem vektoren og x-aksen. Lav en underklasse `EnhedsVektor2D`, som arver fra `Vektor2D` og implementerer metoden `vinkel`.
3. Udvid klassen `Vektor2D` med en abstrakt metode `add`, som tager en anden vektor som argument og returnerer en ny vektor, som er summen af de to vektorer. Lav en underklasse `Vektor3D`, som arver fra `Vektor` og implementerer metoden `add`.


# Komposition
- Komposition handler om at lade en klasse indeholde en anden klasse
- Komposition bruges til at opdele store klasser i mindre og mere overskuelige klasser
- Komposition betrages som en stærkere form for nedarvning, da klassen ikke arver fra en anden klasse

# Eksempel på komposition på vektorer
Først definerer vi en klasse `Punkt`, som indeholder x- og y-koordinaterne:
```python
class Punkt:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

Derefter definerer vi en klasse `Vektor`, som indeholder et punkt og en længde:
```python
class Vektor:
    def __init__(self, punkt, længde):
        self.punkt = punkt
        self.længde = længde
```

# Eksempel på brug af komposition
Først opretter vi en instans af klassen `Punkt` og en instans af klassen `Vektor`:
```python
punkt = Punkt(3, 4)
vektor = Vektor(punkt, 5)
```

Derefter kan vi tilgå punktets x- og y-koordinater og vektorens længde:
```python
print(vektor.punkt.x) # Dette vil give 3
print(vektor.punkt.y) # Dette vil give 4
print(vektor.længde) # Dette vil give 5
```

# Øvelser om komposition
1. Lav en klasse `Punkt`, som indeholder x- og y-koordinaterne. Lav en klasse `LinjeSegment`, som indeholder to punkter og en længde.
2. Lav en klasse Cirkel, som indeholder et punkt og en radius. Lav en klasse `Cylinder`, som indeholder en cirkel og en højde.


# Konklusion
- Klasser og objekter er en måde at strukturere kode på og opdele store klasser i mindre og mere overskuelige klasser
- Klasser og objekter gør det muligt at genbruge kode og undgå gentagelse
- Klasser og objekter gør det muligt at opdele store klasser i mindre og mere overskuelige klasser
- Klasser og objekter gør det muligt at fokusere på det væsentlige og skjule detaljerne

# Vektorklasse i n-dimensioner
I det følgende vil vi udvide vektorklassen til at kunne håndtere vektorer i n-dimensioner. Vi vil også udvide klassen med flere metoder til at udføre operationer på vektorer.

Vi kan håndtere vektorer i n-dimensioner ved at bruge en liste til at gemme koordinaterne

# Struktur til vektorklasse i n-dimensioner
```python
class Vector:
    def __init__(self, *args):
        self.coordinates = list(args)
```
Her har vi defineret en klasse `Vector`, som tager en vilkårlig mængde argumenter og gemmer dem i en liste `coordinates`.

*args betyder, at metoden kan tage et vilkårligt antal argumenter.

# Eksempel på brug af vektorklasse i n-dimensioner
```python
v = Vector(3, 4, 5)
print(v.coordinates) # Dette vil give [3, 4, 5]
```
Her har vi skabt en instans `v` af klassen `Vector` med koordinaterne 3, 4 og 5.

Vi har derefter printet koordinaterne, hvilket vil give [3, 4, 5].

# Øvelser: Implementer metoder til vektorklasse i n-dimensioner
Vi kan udvide vektorklassen med flere metoder til at udføre operationer på vektorer i n-dimensioner. I bedes implementere følgende metoder:

- `__str__`: Returnerer en strengrepræsentation af vektoren
- `__add__`: Lægger to vektorer sammen
- `__sub__`: Trækker to vektorer fra hinanden
- `__mul__`: Ganger en vektor med en skalar
- `__truediv__`: Dividerer en vektor med en skalar
- `længde`: Beregner vektorlængden
- `enheds_vektor`: Beregner enhedsvektoren
- `vinkel`: Beregner vinklen mellem to vektorer
- `skalarprodukt`: Beregner skalarproduktet af to vektorer
- `prikprodukt`: Beregner prikproduktet af to vektorer
- `krydsprodukt`: Beregner krydsproduktet af to vektorer

# Visualisering af vektorer i n-dimensioner ved brug af pygame
I det følgende vil vi visualisere vektorer i n-dimensioner ved brug af pygame. Vi vil tegne vektorerne som pile i et koordinatsystem.

Vi kan tegne pile ved at bruge pygame's `draw` metode og `draw.line` metode.

# Struktur til visualisering af vektorer i 2 og 3 dimensioner
```python
import pygame
import sys

class Vector:
    def __init__(self, *args):
        self.coordinates = list(args)

    def draw2d(self, screen, origin, scale):
        end = (origin[0] + self.coordinates[0] * scale, origin[1] - self.coordinates[1] * scale)
        pygame.draw.line(screen, (255, 255, 255), origin, end, 2)

    def draw3d(self, screen, origin, scale):
        end = (origin[0] + self.coordinates[0] * scale, origin[1] - self.coordinates[1] * scale)
        pygame.draw.line(screen, (255, 255, 255), origin, end, 2)
```

# Forløb om boids ved brug af vektorer i 2 dimensioner
I det følgende vil vi implementere en simulation af boids ved brug af vektorer i 2 dimensioner. Vi vil simulere boids, som er små fugle, der flyver i flok. Se slides på Programmering2425/slides/boids.docx.












