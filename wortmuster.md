Wortmuster als Merkmalsidentifizierer
=====================================

Als sehr effizient erwies sich die Durchführung einer (semi-)automatisierten Merkmalsextraktion bzw. -zuweisung anhand von Wortteilmustern und ihrer Bedeutung als Affix, Wortwurzel bzw. Teil eines Kompositums oder Derivats. 
Diese kommen nämlich gehäuft in den verschiedenen medizinischen Fachbegriffen vor - aufgrund der konstanten sprachlichen Struktur, die auf dem Einfluss des Lateinischen und dem Altgriechischen beruht. 
Immer wieder auftretende Affixe des Lateinischen und des Griechischen (z.B. das Suffix "oplasty" = rekonstruktiver Eingriff) deuten meist auf ein so eindeutig gekennzeichnetes semantisches Konzept hin, dass dieses 1:1 auf entsprechend äquivalente Merkmale übertragen werden kann. 
Semi-automatisiert bedeutet hier, dass die Merkmalsfindung manuell im Gegensatz zur Merkmalszuweisung stattfindet.

Einen großen Mehrwert erhält man zudem durch Berücksichtigung der semantischen Beziehungen zwischen den zugewiesenen Merkmalen. 
Beispielsweise kann jedem Synset, dem das Merkmal Entzündung zugewiesen wurde, auch das Merkmal Krankheit als Oberbegriff zugewiesen werden. 
Neben Hyperonymen kann dieser Folgerungsschritt auch auf Meronyme angewendet werden. 
So kann einem Synset, dem das Merkmal Macula anhand des Teilmusters -macul- zugewiesen wurde, auch das Merkmal Retina zugewiesen werden, da die Macula auf der Netzhaut liegt.

Diesem Prinzip folgend wurden initial zunächst ca. 20 Wortteilmuster manuell aus der Menge an Begriffen im Wörterbuch identifiziert, die sehr frequent auftraten und eine eindeutige Semantik als Morphem aufweisen. 
Beispiele hierfür sind -itis- für Entzündung, -graphy- für bildgebende Verfahren und -retin- für Retina oder Netzhaut. 
Da keine externen Informationsquellen für diesen Prozess benötigt werden können die Merkmalszuweisungen direkt auf Datenbankebene per SQL-Befehl ausgeführt werden. 
Durch automatischen Abgleich der Synonyme in der Datenbank mit den erkannten Teilmustern wurden so über 1000 Merkmalszuweisungen vorgenommen, die etwas mehr als 20% aller Synsets des Wörterbuchs abdecken.

Einsatz einer N-Gramm-Frequenzliste
-----------------------------------

Die Wahl geeigneter Wortmuster durch manuelle Untersuchung der englischen Begriffsliste ist als zu unvollständig einzustufen, da unter Umständen Wortmuster übersehen werden, die für die erwähnte Methode gute Resultate erzielen können. 
Eine Abdeckung von 20% der Menge an Synsets gilt zudem immer noch nicht als ausreichend für den Aufbau eines formalen Kontextes. 
Es wurde daraufhin darüber nachgedacht, wie weitere Wortteilmuster, die sich für die Merkmalszuweisung qualifizieren, automatisch identifiziert werden können, anhand der Anzahl ihres Vorkommens.

Aus dieser Überlegung entstand die Idee, die Wahl solcher Muster nicht dem Zufall zu überlassen, sonderm im Vorhinein eine Frequenzliste aller existierenden n-Gramme aus der Menge an Begriffsbenamungen der Synsets zu generieren, anhand derer geeignete Wortmuster mit semantischem Inhalt gewählt und dann für die angewandte Methode der Merkmalsextraktion berücksichtigt werden.

Hierfür musste zunächst eine nach Häufigkeit sortierte Frequenzliste aller n-Gramme automatisiert erstellt werden. 
Als untere Grenze der Zeichenlänge wurde hier die Schranke n>3 gewählt, das heißt Gramme der Länge 3 und kleiner wurden nicht erstellt. 
Grund hierfür sind Ergebnisse manuellen Herantastens, bei dem bei einer Grammlänge von n=3 kaum signifikante Wortteilmuster erkannt werden konnten, die eindeutig oder ergiebig genug wären. 
Im späteren Verlauf wurden diese 3-Gramme der Vollständigkeit halber trotzdem mit ausgewertet (vier an der Zahl). 
Anschließend wurde die Liste ausgehend vom am häufigsten vorkommenden n-Gramm bis zu einer vorher festgelegten Grenze (in diesem Fall bis zu einer Grammhäufigkeit von 6) manuell abgearbeitet und jedes Gramm jeweils nach semantischem Inhalt sowie semantischer Eindeutigkeit überprüft.

Ausgesuchte Gramme qualifizieren sich als Wortteilmuster und werden mit den zugehörigen Merkmalen, die sich aus der Semantik des Musters ergeben, gekennzeichnet. 
Dies muss manuell geschehen, da hierbei Domänenwissen absolut notwendig ist. 
Ursprung dieses Wissens sind fachbezogene Quellen und die Wikipedia-Enzyklopädie, aber insbesondere der englische Wikipedia-Artikel zu "list of medical roots, suffixes and prefixes". 
Synsets, die eine oder mehrere Synonymbezeichnungen besitzen, welche das gekennzeichnete n-Gramm als Teilzeichenkette enthalten, werden mit den zugewiesenen Merkmalen versehen (Bsp.: das Muster -itis- wird mit den Merkmalen "inflammation" und "disease" gekennzeichnet -> Begriffe, die -itis- als Teilmuster enthalten, bekommen diese zwei Merkmale automatisch zugewiesen).

Das finale Ergebnis dieser Extraktionsmethode ist ein aussagekräftiger formaler Kontext aus 119 Merkmalen, die 4467 Mal zugewiesen wurden. 
Gut die Hälfte aller Synsets aus dem Wörterbuch wurden mithilfe dieser Methode mit Merkmalen versehen. 
Besonders positiv sind dabei der hohe Grad der Qualität an Merkmalen und Zuweisungen aufgrund der eindeutigen Beziehung zwischen Wortbestandteil und Semantik, sowie die hohe Vernetzung der Synsets untereinander durch Merkmale, die im Allgemeinen sehr häufig mehreren verschiedenen Synsets zugewiesen werden konnten.
