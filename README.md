# Inleiding
Deze oefening is deel van de course BEWD aan de Hogeschool Arnhem/Nijmegen. Doel is het bekend raken met Exceptions.

In deze oefening ga je verder met de String-kata die je hebt ontwikkeld. Je kunt (zie stap 1 hieronder) gebruik maken van de uitwerking die beschikbaar is. We gaan zorgen dat gebruikers duidelijke meldingen krijgen als ze ongeldige invoer produceren.

Op dit moment werkt de voorbeelduitwerking zo dat er alleen een resultaat wordt geproduceerd wanneer de invoer geldig is (waarom is dat een goed idee?). Is de invoer ongeldig, dan krijgt de gebruiker -1 terug. Dat kan natuurlijk beter (waarom zou dat een goed idee kunnen zijn?).

# Oefening

Voer de onderstaande stappen één voor één uit. Het is van belang dat je nadenkt over de vraag hoe elke stap volgt uit de vorige.

Ga als volgt te werk:

1. Ga naar https://github.com/AIM-CNP/bewd-workshop-string-kata-uitwerking. Download de zip of gebruik git om het gehele project te downloaden (```git clone```) naar je computer en open dit project in IntelliJ.

2. Aan het einde van de functie `StringCalculator.add(String numbers)` wordt -1 teruggegeven als de invoer niet wordt herkend als geldig. Schrijf code in de main-functie van StringKata.java die detecteert dat dit bij ongeldige invoer gebeurt en een melding toont dat ongeldige invoer correct is herkend.

`StringCalculator.add` is nu op zich prima bruikbaar. Je stopt er invoer in en als het resultaat niet herkenbaar is als evident fout, is het kennelijk het resultaat van het optellen van de twee ingevoerde getallen.

3. Schrijf een nieuwe functie in StringKata.java die twee getallen als invoer heeft en die met behulp van `StringCalculator.add` de twee getallen bij elkaar optelt (dus: `int StringKata.addNumbers(int num1, int num2)` of iets dergelijks). Kijk wat er gebeurt als je aan deze functie als invoer de waarden -3 en 8 meegeeft.

4. -3 + 8 is natuurlijk niet -1. Het is duidelijk dat onze StringCalculator niet met negatieve getallen overweg kan. We zouden er natuurlijk voor kunnen zorgen dat hij dat wel kan, maar dat is erg veel werk. In deze oefening concentreren we ons op onze nieuwe functie `int StringKata.addNumbers(int num1, int num2)`. We moeten voorkomen dat deze functie ongeldige invoer doorgeeft aan `int StringCalculator.add(String numbers)`. Breid addNumbers daarom uit met een controle die voorkomt dat `add(String numbers)` wordt aangeroepen als `num1` of `num2` negatief is.

Waarschijnlijk heb je stap 3 uitgevoerd door met `if` te kijken of zowel `num1` als `num2` groter zijn dan of gelijk zijn aan 0. Misschien heb je ook wel (met `System.out.println`) een foutmelding getoond. Maar wat gaf je functie vervolgens terug? Als dat alsnog 0, -1 of een ander getal was, dan verplicht je degene die jouw functie `int StringKata.addNumbers(int num1, int num2)` om zelf ook te controleren of `num1` en `num2` groter zijn dan of gelijk zijn aan 0. Feitelijk heb je het probleem nu gewoon verplaatst!

Controleren of twee getalletjes groter zijn dan of gelijk zijn aan nul is natuurlijk niet heel veel werk, maar je kunt je voorstellen dat je met complexere functies veel complexere controles moet doen. In dat geval is het erg onwenselijk om die controles overal te moeten uitvoeren op plekken waar de functies in kwestie direct of indirect worden aangeroepen. Voor je het weet, bestaat je complete programma uit controles op de invoer!

Beter is het om gewoon op één plek te constateren dat de invoer ongeldig is en het programma dan verder niet meer uit te voeren.

5. Pas `int StringKata.addNumbers(int num1, int num2)` zo aan dat er wordt gecontroleerd of num1 en num2 allebei een geldige waarde hebben. Is dat niet het geval, toon dan een foutmelding *en* stop het programma (gebruik hiervoor `System.exit(-1)` - de waarde -1 is op zich arbitrair, maar komt overeen met de -1 die we eerder gebruikten als `StringCalculator.add` de invoer niet kon verwerken).

Probleem opgelost.

Alleen ... nu stopt het programma iedere keer dat we negatieve getallen bij elkaar optellen. In sommige gevallen is dat precies wat je wil, maar je kunt je voorstellen dat het in programma's voor eindgebruikers niet handig is als ze vastlopen iedere keer dat een gebruiker per ongeluk iets verkeerds intypt.

Wat we eigenlijk willen is een soort `System.exit` waarmee we het programma kunnen stoppen als er echt niet met de invoer te werken is maar die we ook kunnen afvangen als we de gebruiker alleen maar willen laten *weten* dat zijn of haar invoer ongeldig is.

Zo'n `System.exit` bestaat - en noemen we een Exception.

6. Pas je `int StringKata.addNumbers(int num1, int num2)` zo aan dat je geen `System.exit` aanroept als `num1` of `num2` kleiner is dan nul  maar een Exception produceert (dat noemen we "een Exceptie gooien", met `throw`). Om technische redenen moet je een zogenoemde RuntimeException gebruiken: `throw new RuntimeException("FOUT: negatief getal ingevoerd.");`.

Wat is er nu veranderd? Nog helemaal niets: als `num1` of `num2` kleiner is dan 0 dan stopt het programma.

Maar nu komt het: omdat we een exception gooien en geen `System.exit` gebruiken, kunnen we de exceptie "afvangen", zoals dat heet.

7. Voeg een zogenoemd "try catch"-blok toe aan je aanroep naar `int StringKata.addNumbers(int num1, int num2)`: 
    ```java
    try { 
        // aanroep naar addNumbers
    } catch(RuntimeException e) {
        // Wat er moet gebeuren als het fout gaat
    }
    ```

Gefeliciteerd! Je hebt er nu voor gezorgd dat je voortaan de *keuze* hebt om je programma te beëindigen als er iets ongeldigs is ingevoerd of om het opnieuw te laten proberen.


# Extra's

Java kent allerlei typen exceptions. Dat geeft je de mogelijkheid om degene die je code aanroept precies te laten weten wat er is fout gegaan. In dit voorbeeld is er feitelijk bijvoorbeeld sprake van een `IllegalArgumentException`: de waarden van de argumenten van de functie `int StringKata.addNumbers(int num1, int num2)` is ongeldig (illegaal).

Probeer je functie zo aan te passen dat er geen `RuntimeException` wordt geproduceerd maar een `IllegalArgumentException`. Je zult merken dat je hier allerlei extra dingen voor moet doen. Vraag de docent in de les waarom dat is!




