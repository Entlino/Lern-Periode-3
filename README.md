# Lern-Periode-3

Christian Aeschlimann

12.1. bis 23.2.2024

## Grob-Planung

1. Im Module 431 war ich besonders gut. Im Modul 319 war ich mit einer 3.5 ungenügend.
2. Mein Verbesserungsvorschlag war das ich gerne mein eigenes "kleines" Projekt starten möchte und nicht ständig die Modularbeiten aufholen möchte. Dieses geplante Projekt sollte in der Zukunft stets verbessert/verändert werden, somit hätte ich in Zukunft ebenfalls eine Aufgabe an der ich stets arbeiten kann.
3. Ich möchte gerade eine Applikation erstellen auf welcher ich einfache Spiele hinzufüge wie Tic Tac Toe, Number Guesser, Hangman usw. Ziel wäre wöchentlich ein neues Game hinzuzufügen. Das ganze möchte ich als WinForm-Application implementieren.

![image](https://github.com/Entlino/Lern-Periode-3/assets/111046353/aeed55be-dd48-4a3d-9983-94648adde0d8)

Gewisse Ideen für Spiele.

## 12.1.2024

Heute habe ich mich damit beschäftigt was ich in diesen wenigen Wochen machen möchte. Ich habe mich dazu entschlossen ein Tetris in WinForms zu programmieren. Die nächsten Wochen will ich also damit beginnen das Tetris zu programmieren und danach noch visuell darzustellen.

## 19.1.2024

- [X] Tetris "grid erstellen"
- [X] Tetris "Formen erstellen"
- [ ] Formen die "Icon's" zuordnen
- [X] Die Tetris Formen mit den Pfeiltasten steuerbar machen.

| Testfall-Nummer | Ausgangslage (Given) | Eingabe (When) | Ausgabe (Then) | Erfüllt? |
| --- | --- | --- | --- | --- |
| 1   | Projekt erstellt | Programm gestartet | Tetris "grid" vorhanden. |Erfüllt|
| 2   | Grid erstellt | Programm gestartet | Es sind grobe formen vorhanden. |Erfüllt|
| 3   | Grobe Formen zugeordnet | Programm gestartet | Die Formen verfügen nun über Icon's/Bilder. |Nicht erfüllt|
| 4   | Icon's/Bilder sind eingefügt | Programm gestartet | Die vorhanden Formen lassen sich per Pfeiltasten steuern. |Erfüllt|

Heute am 19.01.2024 habe ich damit begonnen das Tetris-Spiel begonnen. Ich habe als erstes damit angefangen das Spielfeld (Grid) zu erstellen. Dies war glückglicherweise noch keine grosse herausforderung, jedoch als es danach darum geht die Formen zu erstellen habe ich grössere Probleme gehabt. Irgendwie hab ich schlussendlich mithilfe des Internets und AI's einen Code erschaffen bzw. gefunden welcher hoffentlich funktionert. Da ich jedoch seitem schon zu langsam war habe ich mich dafür entschieden das ich das mit den Icons überspringe und direkt zu den Pfeiltasten gehe da dies meiner Meinung nach einen grösseren einfluss auf das spiel hat.


In diesem Code unten habe ich zuerst das Spielfeld erstellt und danach jeder Form ihre Farbe zugeordnet.
``` C#
    public class Tetris : Form
    {
        // Spielfeld, mit grössen
        private const int GridWidth = 10;
        private const int GridHeight = 20;

        // Einzelne Feldergrösse
        private const int CellSize = 20;

        // Farben
        private static readonly Color[] Colors = new Color[]
        {
            Color.Cyan, // I
            Color.Blue, // J
            Color.Orange, // L
            Color.Yellow, // O
            Color.Lime, // S
            Color.Purple, // T
            Color.Red, // Z
        };

```
Im nächsten Code-Beispiel habe ich die einzelnen Formen in ein zweidimensonales Feld eingefügt. Dies hat so funktioniert das ich bei der Form I beispielsweise ein 4x4 Feld mit Booleans Arrays erstellt habe. Dann konnte ich einfach einer Linie den Wert "true" geben und dem rest den "false" Wert. Somit erkennt das Programm wo sich die Form in welcher Rotations befindet. Das ganze habe ich mit alles 7 Formen gemacht. Da es jedoch repetetiv ist habe ich hier nur 1 Form als beispiel eingefügt. (Die "Abschlussklammer" am ende habe ich zu verständlichkeit eingefügt und ist im eigentlichen Programm nicht vorhanden, da schliesslich weitere Zeilen folgen.)

``` C#
        // Booleans für einzelne Formen
        private static readonly bool[][][] Shapes = new bool[][][]
        {
            new bool[][] // I
            {
                new bool[] { true, true, true, true },
                new bool[] { false, false, false, false },
                new bool[] { false, false, false, false },
                new bool[] { false, false, false, false },
            }
        };

```

Um die Formen nun noch mit den Pfeiltasten steuern zu können und mit der Leertaste dirkte nach unter "fallen" lassen zu können habe ich nun ein "Switch-Case" erstellt. Dabei habe ich die einzelnen möglichen Tasteneingaben als einzelnen Case verwendet. So wird wenn man nun die Rechte oder Linke Pfeiltaste verwendet wird die Form eine Zelle nach Rechts oder nach links verschoben. Bei der Unteren Pfeiltaste wird die Form um eine Zelle nach unten verschoben und bei der Oberen Pfeiltaste wird die Form rotiert. Schliesslich kann man mit der Leertaste die Form noch auf den Boden "fallen" lassen.

``` C#
     
        private void Tetris_KeyDown(object sender, KeyEventArgs e)
        {
            // Erstellen des Switch-Case
            switch (e.KeyCode)
            {
                case Keys.Left: // Nach Links verschieben
                    if (CanMove(shapeX - 1, shapeY, shapeRotation))
                    {
                        shapeX--;
                    }
                    break;
                case Keys.Right: // Nach Rechts verschieben
                    if (CanMove(shapeX + 1, shapeY, shapeRotation))
                    {
                        shapeX++;
                    }
                    break;
                case Keys.Down: // Eine Zelle nach unten verschieben
                    if (CanMove(shapeX, shapeY + 1, shapeRotation))
                    {
                        shapeY++;
                    }
                    break;
                case Keys.Up: // Form rotieren
                    if (CanMove(shapeX, shapeY, (shapeRotation + 1) % 4))
                    {
                        shapeRotation = (shapeRotation + 1) % 4;
                    }
                    break;
                case Keys.Space: // Form sofort nach unten "fallen" lassen
                    while (CanMove(shapeX, shapeY + 1, shapeRotation))
                    {
                        shapeY++;
                    }
                    break;
            }
        }

```

## 26.1.2024

- [ ] Die Formen fallen langsam nach unten (1 Block/sek oder 2 Blöcke/sek)
  
- [ ] Die einzelnen Formen landen aufeinander und können nicht in eine andere hinein.
  
- [ ] Sobald eine Reihe voll ist wird diese gelöscht plus ein Counter zählt 1 hoch.
  
- [ ] Wenn eine Reihe gelöscht wird fallen die oberen nach Unten nach.
  

| Testfall-Nummer | Ausgangslage (Given) | Eingabe (When) | Ausgabe (Then) | Erfüllt? |
| --- | --- | --- | --- | --- |
| 5   | Formen sind steuerbar | Spiel wird gestartet | Die Formen generieren und fallen langsam nach unten |Nein|
| 6   | Die Formen fallen nach unten. | Spiel wird gestartet, Form kommt unten an | Sie stapelt sich und fällt auf andere Formen drauf und nicht rein. |Nein|
| 7   | Formen stapeln sich | eine Reihe wird gefüllt | Reihe wird gelöscht, Counter + 1 |Nein|
| 8   | Formen sind stabelbar und steuerbar. | Reihe ist voll und wird gelöscht. | Falls es obere Reihen gibt werden diese nach unten verschoben. |Nein|

Am heutigen Tag konnte ich leider nicht meine geplanten Ziele umsetzen. Dafür gibt es mehrere Gründe. Der absolut grösste Punkt war definitiv das Fehlerbeheben. Da ich leider im Programm, welches ich letzte Woche erschaffen hatte, noch einige Fehler hatte, habe ich die meiste Zeit des Nachmittags damit verbracht, möglichst alle Fehler zu beheben und neuen Code zu implementieren, welcher die Fehler beheben könnte. Als der Nachmittag langsam endete und ich mit Herrn Colic's Hilfe nun endlich ein Programm hatte, welches sich problemlos starten liess, war die Zeit schon zu knapp, um die restlich geplanten Punkte umzusetzen. Dann habe ich mich dazu entschieden, dass ich mich lieber damit beschäftige bzw. mich darüber informiere, wie ich das Tetris am besten visuell darstellen kann. Infolgedessen bin ich dann auf die sogenannten "Bitmaps" gestossen. Diese dienen dazu, eine digitale visuelle Darstellung eines Bildes zu erstellen. Wenn die Informationen, die ich gefunden habe, richtig waren, sollte es mir so möglich sein, das Spiel als "Bild" darzustellen, jedes Mal, wenn nun etwas verändert wurde, wechselt das "Bild".   (171 Wörter)

Um einige der Fehler zu behebem musste ich die "CanMove-Funktion" definieren. Dies habe ich mit folgendem bool gemacht. Der Bool ist jedoch noch nicht mit bedingungen gefüllt und gibt deshalb immer den wert "True" aus. In diesem Bool müsste man nun noch eine IF-Schleife erstellen in welcher jede einzelne "Zelle" des Spielfeldes abgefragt wird ob diese bereits gefüllt ist oder nicht. Falls nicht steht der verschiebung der Form nichts im wege.

``` C#
        bool CanMove(int shapeX, int shapeY, int shapeRotation) => true;
```

## 16.2.2024

Heute habe ich zuerst damit angefangen, meinen Code, welchen ich hier erklärt und visualisiert habe, noch mal durchzuschauen und allfällige Korrekturen vorgenommen. Schlussendlich sollte mein Code nun vollständig herausgeputzt sein. Danach habe ich mich meiner GitHub-Startseite zugewandt und diese nebst dem, dass ich diese aufgeräumt habe, noch visuell ansprechender gestaltet. (51)

## Reflexion

In der Lern-Periode 3 muss ich ehrlich gestehen, ich habe trotz der kurzen Dauer am meisten Spass gehabt. Dies liegt zum einen daran, dass ich in dieser Lern-Periode grossen Spass am GitHub hatte und mir somit immer schon mit Vorfreude auf den Abschluss der einzelnen Tage gewartet habe, um endlich das GitHub machen zu können. Andererseits machte mir das kleine Projekt sehr viel Spass, was aber unter anderem auch dem Erklären des Codes im GitHubs zuzuführen ist. 

(VBV): In der nächsten Lern-Periode möchte ich wie in dieser Lern-Periode den ganzen Code möglichst verständlich im GitHub darstellen und erklären.

(102)
