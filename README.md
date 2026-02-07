# 🦁 POO i UML: The Zoo

[![Versió](https://img.shields.io/badge/versió-1.0.0-blue.svg)](https://github.com/dmorenoar/python-codex-smx)
[![Estat](https://img.shields.io/badge/estat-ONLINE-brightgreen.svg)](https://dmorenoar.github.io/python-codex-smx/)

**Plataforma interactiva d'aprenentatge de Python** dissenyada per al mòdul "Programació i Entorns de desenvolupament" en el cicle formatiu CFGS (Desenvolupament d'Aplicacions Multiplataforma perfil Videojocs i Oci digital).

Guia interactiva per entendre la Programació Orientada a Objectes (POO) i la seva representació en UML.

🌐 **[Veure aplicació en viu](https://dmorenoar.github.io/POO/)**

---

## 📋 Descripció

Aquest projecte és una pàgina web educativa dissenyada per a l'assignatura de Desenvolupament d'Aplicacions Multiplataforma (DAMV) de l'Institut Tecnològic de Barcelona. Ofereix una explicació visual i interactiva dels conceptes fonamentals de la POO utilitzant l'analogia d'un zoològic.

---

## 🎯 Objectius d'Aprenentatge

Els estudiants aprendran:

- **Classes i Objectes**: Comprendre l'estructura bàsica d'una classe
- **Herència**: Relacions jeràrquiques entre classes
- **Abstracció**: Classes i mètodes abstractes
- **Encapsulament**: Protecció i validació de dades
- **Interfícies**: Definició de comportaments i capacitats
- **Relacions UML**: Composició, agregació i realització
- **Diagrames UML**: Lectura i creació de diagrames de classes

## 🗂️ Estructura del Projecte
```
zoo-poo-uml/
├── index.html              # Pàgina principal amb teoria
├── quiz-uml-poo.html      # Test teòric sobre UML (opcional)
├── hunt-error.html        # Exercici de depuració de codi (opcional)
└── README.md              # Aquest fitxer
```

## 📚 Continguts

### 1. La Classe
Introducció als components bàsics:
- **Atributs** (dades): `_weight`, `Name`, `_isHungry`
- **Constructor**: Inicialització de l'objecte
- **Mètodes** (comportament):
  - `Roar(int volume)` - Mètode void amb paràmetre
  - `CalculateFood()` - Mètode amb retorn de tipus double

**Representació UML:**
```
┌─────────────────┐
│      Lion       │
├─────────────────┤
│ - weight: double│
│ + Name: string  │
│ - isHungry: bool│
├─────────────────┤
│ + Roar(int)     │
│ + CalculateFood()│
└─────────────────┘
```

### 2. Herència i Abstracció
- **Classe abstracta** `Animal`: No es pot instanciar directament
- **Mètodes abstractes**: `Eat()` - sense implementació a la classe pare
- **Override**: `Lion` implementa obligatòriament el mètode `Eat()`
- **Modificador `protected`**: L'atribut `age` és accessible per les classes filles

**Jerarquia:**
```
     Animal (abstract)
          △
          │
        Lion
```

### 3. Relacions entre Classes

#### Composició (◆) - Relació Forta
- **Definició**: "Part de" - El component no té sentit sense el contenidor
- **Exemple**: Lion ◆—→ Heart
- **Cicle de vida**: Si el Lleó mor, el Cor també deixa de funcionar
- **Codi**: El contenidor crea l'objecte amb `new`
```csharp
public class Lion {
    private Heart _heart;
    public Lion() {
        _heart = new Heart(); // Composició
    }
}
```

#### Agregació (◇) - Relació Feble
- **Definició**: "Té un" - El component pot existir independentment
- **Exemple**: Lion ◇—→ Collar
- **Cicle de vida**: Si el Lleó mor, el Collar es pot reutilitzar
- **Codi**: L'objecte ve de fora (paràmetre)
```csharp
public class Lion {
    private Collar _gps;
    public void SetCollar(Collar c) {
        _gps = c; // Agregació
    }
}
```

### 4. Encapsulament
Protecció de la integritat de les dades mitjançant:
- **Camps privats**: `private double _weight`
- **Propietats públiques**: amb getters i setters
- **Validació**: Control de valors incorrectes
```csharp
public double Weight {
    get => _weight;
    set {
        if (value < 0) {
            _weight = 0;
        } else {
            _weight = value;
        }
    }
}
```

### 5. Interfícies
- **Definició**: Contracte de capacitats que una classe ha d'implementar
- **Exemple**: `IPredator` - defineix el comportament de caçar
- **Avantatge**: Separa el "ser" (Animal) del "fer" (Caçar)
- **Notació UML**: Rectangle amb línia discontínua i etiqueta `<<interface>>`

**Per què no posar `Hunt()` a Animal?**
No tots els animals cacen (Zebres, Pingüins). La interfície permet assignar aquesta capacitat només als predadors.
```csharp
public interface IPredator {
    void Hunt();
}

public class Lion : Animal, IPredator {
    public override void Eat() { ... }  // De Animal
    public void Hunt() { ... }           // De IPredator
}
```

### 6. Arquitectura Final del Zoo

**Diagrama complet amb totes les relacions:**
```
        Zoo
         ◆ (composició)
         │
    Enclosure
         ◇ (agregació)
         │
       Animal {abstract}
         △ (herència)
      ┌──┴──┐
    Lion  Penguin
      │
      ├──◆──→ Heart (composició)
      ├──◇──→ Collar (agregació)
      └──⋯▷  IPredator (realització)
```

**Llegenda de relacions:**
- **◆** Composició (rombe ple)
- **◇** Agregació (rombe buit)
- **△** Herència (triangle buit)
- **⋯▷** Realització d'interfície (línia discontínua amb triangle)

## 👨‍🎓 Guia d'Estudi per Estudiants

### Ruta d'Aprenentatge Recomanada

1. **Llegeix seqüencialment** cada secció (1 → 6)
2. **Compara** sempre el codi C# amb el diagrama UML
3. **Identifica** els modificadors d'accés (+, -, #) en UML
4. **Practica** dibuixant tu mateix els diagrames en paper
5. **Verbalitza** les relacions: "Zoo conté Enclosures" (composició)
6. **Exercicis** realitza els exercicis per verificar els teus coneixements.

### Consells per Entendre UML

| Símbol UML | Significat | Exemple Codi |
|-----------|-----------|--------------|
| `+` | public | `public string Name` |
| `-` | private | `private double _weight` |
| `#` | protected | `protected int age` |
| `◆` | Composició | `_heart = new Heart()` |
| `◇` | Agregació | `SetCollar(Collar c)` |
| `△` | Herència | `: Animal` |
| Cursiva | Abstract | `abstract class Animal` |

### Preguntes d'Autoavaluació

1. **Classe vs Objecte**: Quin és el plànol i quin és la casa construïda?
2. **Herència**: Pot un Pingüí accedir directament a `age` de Animal?
3. **Composició vs Agregació**: Quin té el rombe ple?
4. **Interfície**: Per què no posem `Hunt()` directament a `Animal`?
5. **Encapsulament**: Què passa si fem `lion.Weight = -100`?

## 🧪 Exercicis Pràctics (Opcionals)

Si tens els fitxers HTML adicionals:

### Quiz Teòric UML (`quiz-uml-poo.html`)
- Preguntes sobre simbologia UML
- Identificació de relacions
- Lectura de diagrames

### Caça d'Errors C# (`hunt-error.html`)
- Codi amb errors intencionals
- Pràctica de depuració
- Comprensió de sintaxi

## 📐 Modificadors d'Accés en C#

| Modificador | Accessible des de | UML |
|------------|------------------|-----|
| `public` | Qualsevol lloc | `+` |
| `private` | Només la mateixa classe | `-` |
| `protected` | Classe i filles | `#` |
| `internal` | Mateix assembly | `~` |

## 🔍 Glossari de Termes

- **Atribut**: Variable que conté dades d'un objecte
- **Mètode**: Funció que defineix comportament
- **Constructor**: Mètode especial que inicialitza objectes
- **Override**: Sobreescriure un mètode heretat
- **Abstract**: Classe o mètode incomplet que requereix implementació
- **Interface**: Contracte que defineix mètodes obligatoris
- **Encapsular**: Amagar detalls d'implementació

## 📖 Referències Addicionals

Per aprofundir en els conceptes:
- [Microsoft C# Documentation](https://docs.microsoft.com/dotnet/csharp/)
- [UML Class Diagrams](https://www.uml-diagrams.org/class-diagrams-overview.html)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)

## 📄 Llicència

Material educatiu © **Institut Tecnològic de Barcelona (ITB)** 2025/2026  
Curs: **CFGS Desenvolupament d'Aplicacions Multiplataforma (DAMV)**

---

**Última actualització**: Febrer 2025  
**Versió**: 1.0  
**Autoria**: ITB - Departament de Programació
