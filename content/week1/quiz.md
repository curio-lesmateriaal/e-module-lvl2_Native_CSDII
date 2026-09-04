---
week: 1
title: Quiz Week 1 — OOP in C#
passScore: 70
questions:
  - id: w1q1
    question: Wat is een class in C#?
    options:
      - Een specifiek exemplaar met ingevulde waarden
      - Een sjabloon met eigenschappen (fields) en mogelijkheden (methoden)
      - Een methode die objecten opruimt
      - Een variabele die altijd public is
    correct: 1
    explanation: Een class is de blauwdruk/het sjabloon. Een object is een ingevuld exemplaar daarvan.
  - id: w1q2
    question: Waar dient de constructor van een class voor?
    options:
      - Het object opruimen als het niet meer gebruikt wordt
      - Een kopie van het object maken
      - Een nieuw object opbouwen en beginwaarden instellen
      - De class omzetten naar JSON
    correct: 2
    explanation: De constructor wordt uitgevoerd bij `new` en zet het object in een bruikbare begintoestand.
  - id: w1q3
    question: "Welke regel maakt een nieuw object aan volgens het sjabloon Car?"
    options:
      - "Car myCar = Car(\"BMW\", \"M4\", \"Black\", 300);"
      - "new Car myCar = (\"BMW\", \"M4\", \"Black\", 300);"
      - "Car myCar = new Car(\"BMW\", \"M4\", \"Black\", 300);"
      - "Car.new(\"BMW\", \"M4\", \"Black\", 300);"
    correct: 2
    explanation: Je gebruikt `new Car(...)` en geeft tussen haakjes de parameters voor de constructor op.
  - id: w1q4
    question: Je hebt twee Car-objecten. Je roept `auto1.Brake()` aan. Wat gebeurt er met auto2?
    options:
      - Niets, methoden werken op één specifiek object
      - auto2 remt ook af
      - Er ontstaat een compilerfout
      - auto2 wordt verwijderd
    correct: 0
    explanation: Een instance-methode werkt alleen op het object waarop je hem aanroept.
  - id: w1q5
    question: Welke van deze types is een value type in C#?
    options:
      - string
      - int
      - Een zelfgemaakte class
      - Een array
    correct: 1
    explanation: "int, float, double, char, bool, struct en enums zijn value types; de meeste andere types (waaronder string en classes) zijn reference types."
  - id: w1q6
    question: "Een <code>int</code>-variabele <code>number</code> is 5. Je geeft <code>number</code> mee aan een methode; in die methode wordt de parameter op 10 gezet. Wat is <code>number</code> daarna?"
    options:
      - "10"
      - "5"
      - "0"
      - Niets, het geeft een fout
    correct: 1
    explanation: number is een value type; de methode krijgt een kopie. De originele variabele blijft 5.
  - id: w1q7
    question: "Je maakt <code>var obj = new SimpleClass(5)</code>. Je geeft <code>obj</code> mee aan een methode die <code>o.Value = 10</code> uitvoert. Wat is <code>obj.Value</code> daarna?"
    options:
      - "5"
      - Niets, het geeft een fout
      - "10"
      - "null"
    correct: 2
    explanation: Een class is een reference type. De methode werkt op hetzelfde object, dus Value is nu 10.
  - id: w1q8
    question: Waarom geef je in een racespel de RaceCar mee aan de RaceDriver-constructor?
    options:
      - Zodat de RaceDriver een referentie heeft en de methoden van die auto kan aanroepen
      - Omdat een constructor altijd een parameter nodig heeft
      - Zodat er een kopie van de auto ontstaat voor de driver
      - Dat is niet nodig, de driver vindt de auto vanzelf
    correct: 0
    explanation: Via de meegegeven referentie kan de driver op verschillende plekken in zijn code `Car.Accelerate()` en dergelijke aanroepen.
---
