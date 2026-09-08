---
week: 1
title: Quiz Week 1 — Methoden, void & OOP
passScore: 70
questions:
  - id: w1q1
    question: "Wanneer geef je een methode het returntype <code>void</code>?"
    options:
      - Als de methode iets doet maar niets terug hoeft te geven aan de aanroeper
      - Als de methode geen parameters heeft
      - Als de methode private is
      - Als de methode maar één regel code bevat
    correct: 0
    explanation: "void betekent 'geeft niets terug'. Een methode als TurnRight() of SetPlayerName(string name) voert iets uit; de aanroeper krijgt geen waarde terug."
  - id: w1q2
    question: "Je schrijft een methode <code>GetGameSpeed</code> die de huidige <code>gameSpeed</code> aan de aanroeper moet doorgeven. Welk returntype is juist?"
    options:
      - "void, want het is maar één waarde"
      - "float, zodat de methode de gameSpeed terug kan geven"
      - "void, en daarna de waarde printen met Console.WriteLine"
      - Elke Get-methode is altijd void
    correct: 1
    explanation: "Zodra de aanroeper een resultaat nodig heeft, kies je een returntype dat bij die waarde past (hier float) in plaats van void. De methode eindigt dan met return gameSpeed;."
  - id: w1q3
    question: "Een methode <code>IsRunning</code> moet aangeven of het spel draait (ja of nee). Wat is het beste returntype?"
    options:
      - "void"
      - "string met \"ja\" of \"nee\""
      - "bool"
      - "int met 0 of 1"
    correct: 2
    explanation: "Een ja/nee-vraag geef je terug als bool (true of false). Datzelfde geldt voor methoden als CanPickupItem(...) of IsReachable(...)."
  - id: w1q4
    question: Uit welke onderdelen bestaat een methodedefinitie (de signature)?
    options:
      - Alleen de naam van de methode
      - Het returntype, de naam en de parameterlijst (types en volgorde)
      - De naam en het aantal regels code in de body
      - De naam en of de methode public of private is
    correct: 1
    explanation: "Je leest een methode af aan het returntype (wat komt eruit?), de naam (wat doet hij?) en de parameters (welke gegevens heeft hij nodig?)."
  - id: w1q5
    question: "Wat is een <em>overloaded method</em>?"
    options:
      - Een methode die te veel werk doet en opgesplitst moet worden
      - Een methode met dezelfde naam als een bestaande methode, maar met een andere parameterlijst
      - Een methode die een andere methode aanroept
      - Een methode die vaker dan één keer per seconde wordt aangeroepen
    correct: 1
    explanation: "Bij overloading hebben meerdere methoden dezelfde naam, bijvoorbeeld IncreaseGameSpeed() en IncreaseGameSpeed(float amount). Ze verschillen in hun parameterlijst."
  - id: w1q6
    question: "Je hebt al <code>public int CountSteps(int top, int left)</code>. Mag je daarnaast <code>public string CountSteps(int top, int left)</code> toevoegen als overload?"
    options:
      - "Ja, want het returntype is anders"
      - "Nee, alleen een ander returntype is niet genoeg; de parameterlijst moet verschillen"
      - "Ja, maar alleen als de tweede methode private is"
      - "Ja, C# kiest dan zelf de string-versie"
    correct: 1
    explanation: "Overloads moeten verschillen in hun parameterlijst (aantal of type parameters). Alleen het returntype veranderen geeft een compilerfout."
  - id: w1q7
    question: "Je hebt <code>CountSteps(int top, int left)</code> én <code>CountSteps(Path path)</code>. Je roept <code>game.CountSteps(3, 5)</code> aan. Welke versie draait?"
    options:
      - "De versie met (int top, int left), want die past bij de meegegeven argumenten"
      - "De versie met (Path path)"
      - Allebei, na elkaar
      - Dat geeft een foutmelding omdat er twee methoden met die naam zijn
    correct: 0
    explanation: "De compiler kiest automatisch de overload waarvan de parameterlijst past bij de meegegeven argumenten. Twee ints horen bij de (int, int)-versie."
  - id: w1q8
    question: "Je maakt <code>Game game1 = new Game()</code> en <code>Game game2 = new Game()</code> en roept daarna <code>game1.IncreaseScore()</code> aan. Wat is waar?"
    options:
      - Alleen de score van game1 gaat omhoog; game2 blijft onaangeroerd
      - De score van beide games gaat omhoog
      - De score hoort bij de class Game, dus alle games krijgen dezelfde score
      - Er ontstaat een foutmelding omdat er twee Game-objecten zijn
    correct: 0
    explanation: "Een instance-methode werkt op het specifieke object waarop je hem aanroept. game2 is een ander object met zijn eigen velden."
---
