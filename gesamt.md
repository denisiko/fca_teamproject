Bericht Teamprojekt
===================

Einführungsteil
---------------

### A multilingual Dictionary of Ophthalmology (Aufbau und Umfang des Dictionarys, was bisher daran gemacht wurde)
### Ideen und Zielsetzung (SimuLLda, FCA, lexical gap)
### Erste Überlegungen zur Umsetzung

FCA-Teil
--------

### Einführung (z.B. Kreuztabellen, Merkmalexploration)

### (Hasse-)Diagramme

### Grenzen (keine direkte Hierarchie möglich, nur binäre Zuweisungen von Merkmalen möglich)

### Chancen (einfache Struktur, Exploration des Begriffsverbandes)

Berichtsteil
------------

### Automatisierter Aufbau einer Wissensdatenbank (Extraktion allgemein)

Der erste Schritt vor der Durchführung von Formaler Begriffsanalyse ist im Fall des Augenheilkundewörterbuchs der Erschließungsprozess der zu analysierenden Begriffe, also der Synsets. Ein Begriffsverband als Ergebnis der FCA stellt die Menge an Begriffen in Bezug zu einer vordefinierten Menge an Merkmalen. Die Ausgangslage des Projekts gab jedoch keine Merkmale vor, die man zur FCA heranziehen konnte. Stattdessen warten annähernd 2500 Synsets, die sich auf ca. 20000 Einträge des Wörterbuchs verteilen darauf, inhaltlich erschlossen und anschließend analysiert zu werden.

Eine derart große Menge an Konzepten lässt sich nur schwer durch intellektuellen Aufwand erschließen, zumal hierzu ein hohes Maß an vertieftem Domänenwissen innerhalb des Bereichs der Augenheilkunde nötig wäre. Aus diesem Grund erschien die Automatisierung dieses Schrittes als die einzig vielversprechende Methode, Merkmale für formale Begriffsverbände aus den Synsets des Wörterbuchs zu generieren, weshalb diese auch eine der ersten Zielsetzungen für das Projekt darstellt. Gerade im Hinblick auf zukünftige Projekte, die sich mit der Anwendung Formaler Begriffsanalyse auf große Mengen von Wissen beschäftigen, sind die Erkenntnisse, die aus der Merkmalsgenerierung gezogen werden, als wertvoll einzuschätzen.

Essentiell ist hierbei die Wahl geeigneter Wissensquellen, aus denen die Merkmale gewonnen werden, und die Herangehensweise bei der Verwertung der Quellen, also der Art und Weise, wie Merkmale extrahiert werden. Doch stellt sich hierbei zunächst die Frage, welche Eigenschaften ein Wissensbestand aufweisen sollte, damit er als Quelle für die Merkmalsextraktion in Betracht gezogen werden kann. Darauf wird in diesem Kapitel bezüglich der konkret in Betracht gezogenen Quellen eingegangen.

Für einen kompletten formalen Kontext, wie ihn die FCA beschreibt, sind eine Menge an Begriffen und eine Menge an Merkmalen aber nicht ausreichend: der Bezug der Elemente der einen Menge zu den Elementen der anderen fehlt. In der formalen Begriffsanalyse wird dieser durch eine Relation mit binärem Wertebereich, der Merkmalszuweisung, angegeben. Binär heißt, dass ein Merkmal einem Begriff entweder zugewiesen werden kann (Wert=1) oder nicht (Wert=0). Diese Beziehung zwischen den beiden Mengen macht einen formalen Kontext erst verwertbar und bildet die Grundlage der Analyse.

Die Merkmalszuweisung wird im Zuge der automatisierten Merkmalsextraktion automatisch vollzogen, da die untersuchten Synsets ausschließlich auf Eigenschaften untersucht werden, die auf zutreffende Merkmale schließen lassen, also auf solche, die für das untersuchte Synset mit dem Wert 1 versehen werden können. Diese Methode erschien am leichtesten umsetzbar und ist vergleichbar mit dem automatischem Tagging, bei dem wissensrelevanten Elementen entsprechende Keywords zugewiesen werden, die dieses Element beschreiben.

Ein formaler Kontext für eine gegebene Menge an Synsets entsteht dementsprechend aus der Menge dieser Synsets, der Vereinigungsmenge der zugewiesenen Merkmale aller betrachteten Synsets, sowie die daraus resultierende Zuweisungsrelation zwischen beiden Mengen (ist ein Merkmal aus der Menge einem Synset nicht zugewiesen, so hat das Synset für dieses Merkmal den Wert 0, ansonsten 1). Die Menge an Merkmalen ergibt sich nach dieser Methode also nicht aus vordefinierten Überlegungen, wonach ein formaler Kontext analysiert werden soll, sondern aus der Semantik jedes einzelnen Synsets, das in den formalen Kontext mit aufgenommen wird. Somit existiert in einem formalen Kontext kein einziges Merkmal, das keinem der betrachteten Synsets zugewiesen wurde.

### ICD-10 als Wissensquelle

Das digitale Wörterbuch der Augenheilkunde deckt Begriffe einer großen Bandbreite von semantischen Bereichen der Medizin ab. Wir konnten während unserer Arbeit am Wörterbuch folgende Kategorien identifizieren:

a) Anatomie (Aufbau des Auges)
b) Pathologie (Erkrankungen des Auges)
c) externe Schädigungen des Auges
d) Behandlungs- und diagnostische Verfahren
e) Instrumente und Apparate in der Augenheilkunde
f) Arzneimittel

Da vor allem Erkrankungen des Auges einen Großteil der Synsets ausmachen lag der Fokus auf potentiellen Wissensdomänen, die diesen Bereich der Augenheilkunde gut abdecken. Ausgehend von dieser Überlegung wurde die deutsche Ausgabe der ICD-10 - die internationale Standard-Klassifikation der Krankheiten - in der Version des Jahres 2011 zur Merkmalsextraktion herangezogen. Die Tatsache, dass die komplette Klassifikation online in HTML-Form zugänglich ist und Einträge der Klassifikation hierarchisch nach anatomischer Lage geordnet sind, lässt die ICD-10 als ideale Wissensquelle für unsere Zwecke erscheinen, jedoch taten sich Probleme auf, die im Folgenden erläutert werden sollen.

Die automatisierte Merkmalsextraktion setzt am Aufbau der ICD-Notationen an. Diese sind nach einem strikten hierarchischen Klassensystem aufgebaut, wie man es von Notationen aus einer Klassifikation kennt. So steht z.B. die Klasse H40 für ein Glaukom, während H40.1 konkret für ein primäres Weitwinkelglaukom steht. Die Idee besteht nun darin, die Synsets des Wörterbuchs auf die Einträge in der ICD-10 mittels Zeichenkettenvergleich abzubilden (mittels Abgleich von Wörterbuchsynonym und Überschrift des ICD-10-Eintrags), die Klassen der Notation zu identifizieren und diese wiederum auf entsprechende Merkmale abzubilden, wie z.B. Glaukom für H40. Identifiziert werden einzelne Einträge der Klassifikation, inklusive Überschrift und Notation, mit regulären Ausdrücken, die einzelne Abschnitte der ICD-10 automatisch erkennen und extrahieren.

Mithilfe der offen gestaltenen Notation soll dann anschließend jedem Synset, dem eine spezifische Notation zugeteilt wurde, zusätzlich alle Merkmale zugewiesen werden, die auch dem Synset der Oberklasse zugeteilt wurden. Beispielsweise sollen dem Synset für primäres Weitwinkelglaukom (H40.1) alle Merkmale des Synsets Glaukom (H40), sowie das Merkmal Glaukom selbst zugewiesen werden, ausgehend von der Notation. Zusätzlich kann jedem Synset, dem eine Notation als Merkmal zugeordnet wurde, auch das Merkmal Krankheit zugewiesen werden.

In der Praxis scheiterte dieser Ansatz beim Vergleich der Titel der ICD-10-Einträge mit den Benamungen der Wörterbucheinträge. Obwohl den Synsets häufig mehrere synonyme Bezeichnungen vergeben wurden, auch z.B. unterschiedliche Schreibweisen, konnten lediglich 43 Synsets aus dem Wörterbuch automatisiert ICD-10-Notationen zugeordnet werden und nur ca. 50 Merkmale (bzw. Notationen) erkannt und vergeben werden, von denen die meisten nur ein einziges Mal vergeben wurden. Konkrete Hauptgründe sind die Zusatzinformationen, die bei vielen Krankheiten im Titel standen und ohne manuelles Eingreifen nur schwer zu identifizieren sind, sowie unterschiedliche Wortstellungen bei komplexeren Begriffen. Die niedrige Zahl der Merkmalszuweisungen ergibt sich aus der hierarchischen Struktur der ICD-10, da durch die Einteilung in Klassen Überlappungen von Informationen vermieden werden. Folglich ist dieses Ergebnis als Grundlage für aussagekräftige formale Verbände in keiner Weise hinreichend und der Ansatz der automatisierten Verarbeitung der ICD-10-Klassifikation wurde nicht weiter verfolgt.

### Wortmuster als Merkmalsidentifizierer

Als sehr effizient erwies sich die Durchführung einer (semi-)automatisierten Merkmalsextraktion bzw. -zuweisung anhand von Wortteilmustern und ihrer Bedeutung als Affix, Wortwurzel bzw. Teil eines Kompositums oder Derivats. Diese kommen nämlich gehäuft in den verschiedenen medizinischen Fachbegriffen vor - aufgrund der konstanten sprachlichen Struktur, die auf dem Einfluss des Lateinischen und dem Altgriechischen beruht. Immer wieder auftretende Affixe des Lateinischen und des Griechischen (z.B. das Suffix "oplasty" = rekonstruktiver Eingriff) deuten meist auf ein so eindeutig gekennzeichnetes semantisches Konzept hin, dass dieses 1:1 auf entsprechend äquivalente Merkmale übertragen werden kann. Semi-automatisiert bedeutet hier, dass die Merkmalsfindung manuell im Gegensatz zur Merkmalszuweisung stattfindet.

Einen großen Mehrwert erhält man zudem durch Berücksichtigung der semantischen Beziehungen zwischen den zugewiesenen Merkmalen. Beispielsweise kann jedem Synset, dem das Merkmal Entzündung zugewiesen wurde, auch das Merkmal Krankheit als Oberbegriff zugewiesen werden. Neben Hyperonymen kann dieser Folgerungsschritt auch auf Meronyme angewendet werden. So kann einem Synset, dem das Merkmal Macula anhand des Teilmusters -macul- zugewiesen wurde, auch das Merkmal Retina zugewiesen werden, da die Macula auf der Netzhaut liegt.

Diesem Prinzip folgend wurden initial zunächst ca. 20 Wortteilmuster manuell aus der Menge an Begriffen im Wörterbuch identifiziert, die sehr frequent auftraten und eine eindeutige Semantik als Morphem aufweisen. Beispiele hierfür sind -itis- für Entzündung, -graphy- für bildgebende Verfahren und -retin- für Retina oder Netzhaut. Da keine externen Informationsquellen für diesen Prozess benötigt werden können die Merkmalszuweisungen direkt auf Datenbankebene per SQL-Befehl ausgeführt werden. Durch automatischen Abgleich der Synonyme in der Datenbank mit den erkannten Teilmustern wurden so über 1000 Merkmalszuweisungen vorgenommen, die etwas mehr als 20% aller Synsets des Wörterbuchs abdecken.

Einsatz einer N-Gramm-Frequenzliste
-----------------------------------

Die Wahl geeigneter Wortmuster durch manuelle Untersuchung der englischen Begriffsliste ist als zu unvollständig einzustufen, da u.U. Wortmuster übersehen werden, die für die erwähnte Methode gute Resultate erzielen können. Eine Abdeckung von 20% der Menge an Synsets gilt zudem immer noch nicht als ausreichend für den Aufbau eines formalen Kontextes. Es wurde daraufhin darüber nachgedacht, wie weitere Wortteilmuster, die sich für die Merkmalszuweisung qualifizieren, automatisch identifiziert werden können, anhand der Anzahl ihres Vorkommens.

Aus dieser Überlegung entstand die Idee, die Wahl solcher Muster nicht dem Zufall zu überlassen, sonderm im Vorhinein eine Frequenzliste aller existierenden n-Gramme aus der Menge an Begriffsbenamungen der Synsets zu generieren, anhand derer geeignete Wortmuster mit semantischem Inhalt gewählt und dann für die angewandte Methode der Merkmalsextraktion berücksichtigt werden.

Hierfür musste zunächst eine nach Häufigkeit sortierte Frequenzliste aller n-Gramme automatisiert erstellt werden. Als untere Grenze der Zeichenlänge wurde hier die Schranke n>3 gewählt, d.h. Gramme der Länge 3 und kleiner wurden nicht erstellt. Grund hierfür sind Ergebnisse manuellen Herantastens, bei dem bei einer Grammlänge von n=3 kaum signifikante Wortteilmuster erkannt werden konnten, die eindeutig oder ergiebig genug wären. Im späteren Verlauf wurden diese 3-Gramme der Vollständigkeit halber trotzdem mit ausgewertet (vier an der Zahl). Anschließend wurde die Liste ausgehend vom am häufigsten vorkommenden n-Gramm bis zu einer vorher festgelegten Grenze (in diesem Fall bis zu einer Grammhäufigkeit von 6) manuell abgearbeitet und jedes Gramm jeweils nach semantischem Inhalt sowie semantischer Eindeutigkeit überprüft.

Ausgesuchte Gramme qualifizieren sich als Wortteilmuster und werden mit den zugehörigen Merkmalen, die sich aus der Semantik des Musters ergeben, gekennzeichnet. Dies muss manuell geschehen, da hierbei Domänenwissen absolut notwendig ist. Ursprung dieses Wissens sind fachbezogene Quellen und die Wikipedia-Enzyklopädie, aber insbesondere der englische Wikipedia-Artikel zu "list of medical roots, suffixes and prefixes". Synsets, die eine oder mehrere Synonymbezeichnungen besitzen, welche das gekennzeichnete n-Gramm als Teilzeichenkette enthalten, werden mit den zugewiesenen Merkmalen versehen (Bsp.: das Muster -itis- wird mit den Merkmalen "inflammation" und "disease" gekennzeichnet -> Begriffe, die -itis- als Teilmuster enthalten, bekommen diese zwei Merkmale automatisch zugewiesen).

Das finale Ergebnis dieser Extraktionsmethode ist ein aussagekräftiger formaler Kontext aus 119 Merkmalen, die 4467 Mal zugewiesen wurden. Gut die Hälfte aller Synsets aus dem Wörterbuch wurden mithilfe dieser Methode mit Merkmalen versehen. Besonders positiv sind dabei der hohe Grad der Qualität an Merkmalen und Zuweisungen aufgrund der eindeutigen Beziehung zwischen Wortbestandteil und Semantik, sowie die hohe Vernetzung der Synsets untereinander durch Merkmale, die im Allgemeinen sehr häufig mehreren verschiedenen Synsets zugewiesen werden konnten.

### Wikipedia als Wissensquelle

Die Kategorie-Tags in der Wikipedia
-----------------------------------

### Vorüberlegungen

Wie bereits erwähnt wurde, war aus unserer Sicht insbesondere die Beschränkung auf Krankheiten das Hauptproblem, weshalb kaum Merkmalszuweisungen gelangen. Ein etwas subtileres Problem ist aber auch die Art der Information.
In der ICD-10 ist die Bezeichnung einer Klasse keine Erklärung (also ein in den Kontext anderer vorhandener Klassen setzen) und auch keine Umschreibung (also ein Ausdruck einer gegebenen Klasse in termini ihrer Ober- oder Unterklassen).
Selbst eine einfache Verschlagwortung mittels eines kontrollierten Vokabulars erzeugt dabei mehr Querverweise, die für den Aufbau einer Merkmalsmenge nützlich sein können (der Grund dafür ist, wie bereits erwähnt, dass das genau der Zweck der Klassifikation ist: möglichst wenig Kongruenz im Begriffsumfang mit benachbarten, vor allem aber Ober- und Unterbegriffen zu haben).

In der Wikipedia wird durch Zuweisung eines Artikels einer oder mehreren Kategorien eine Klassifikation erzeugt.
In erster Linie dient dies dazu, thematische Bereiche zu erstellen und weniger eine Begriffsordnung zu schaffen. Daher gibt es, neben einer Begriffsordnung eher zurechenbaren Kategorien wie 'Medizin', 'Medizinisches Fachgebiet', 'Augenheilkunde', Sammelkategorien wie 'Liste Nationalparks'.
Die Wikipedia hat damit Eigenschaften einer hierarchischen Klassifikation und solche einer Facettenklassifikation.

Die Wahl eines geeigneten Kategoriebegriffs für einen Artikel ist dem jeweiligen Autor freigestellt, er kann auch einen neuen Kategoriebegriff wählen.
In der Praxis gibt es aber Empfehlungen für die Eigenschaften und die korrekte Wahl eines geeigneten Kategoriebegriffs und über die Zeit bildet sich dadurch eine brauchbare (das heißt: nicht zu diverse) Begriffsordnung heraus, weil darauf geachtet wird, dass es beispielsweise nur eine Kategorie 'Liste Nationalparks' gibt, und nicht zusätzlich noch 'Liste der Nationalparks', 'Liste aller Nationalparks' und ähnlichen Abweichungen.
Eines der Probleme dabei ist, dass nicht sichergestellt ist, dass eine Seite nicht einer Kategorie und einer Oberkategorie dieser Kategorie gleichzeitig eingeordnet wird.
Dadurch wird es für die automatische Erschließung eines Kategoriebaums allerdings erforderlich, auf diese Weise doppelt gesammelte Artikel zu eliminieren.
Insbesondere ist darauf zu achten, wenn den Kategorien-Tags automatisiert gefolgt wird um weitere Artikel zu erschließen, bereits besuchte Kategorien zu ignorieren, um Schleifenbildung zu vermeiden.
Dies berücksichtigend schien es aber vielversprechend den Bereich Augenheilkunde sowohl der englischen wie der deutschen Wikipedia bezüglich der vergebenen Kategorien zu untersuchen.

Zu diesem Zweck wurde von beiden der Volltext-Dump der Wikipedia Abstracts als XML formatierte Datei heruntergeladen und innerhalb der title-Tags nach Übereinstimmungen mit Begriffen oder Phrasen aus dem Wörterbuch der Augenheilkunde gesucht.
Die Abstracts sind automatisch erstellte Kurzfassungen der entsprechenden Artikel und bestehen, wie sich herausstellte, im Wesentlichen aus dem ersten Absatz, oder, falls eine bestimmte, nicht exakt erkennbare, Untergrenze an Wörtern nicht überschritten wurde, aus den ersten Absätzen. Weiterhin sind die Kategorien vermerkt, denen der Artikel angehört.
Die Abstracts werden aus dem Quelltext gewonnen und der Text ist mit dem Markup der Wikipedia ausgezeichnet.
Da es unterschiedliche Konventionen bezüglich der Formatierung im Quelltext gibt, sind einige Abstracts unbrauchbar gewesen, da sie im Wesentlichen aus dem Markup einer dem Artikel vorangestellten Infobox (ein Beispiel einer solchen Infobox kann man auf der Seite jedes chemischen Elements betrachten) bestanden und keinerlei Fließtext mehr enthielten.
Aus der deutschen Wikipedia konnten auf diese Weise 433 Artikel für die weitere Verwendung extrahiert werden und aus der englischen Wikipedia 731 Artikel, die Mitglieder der Kategorie selbst oder einer Unterkategorie von *Augenheilkunde*  oder *Ophthalmology* waren.

### Vorgehensweise

Das Vorgehen hierzu umfasste zahlreiche nur manuell durchzuführende Schritte, um die Ergebnismenge möglichst frei von Artikeln oder Kategorien zu halten, die nicht zur eigentlichen Fragestellung zählten. Die Vorgehensweise war wie folgt:

1. Download des Abstract-Dumps, für die deutsche Wikipedia 1.19 GB und für die englische Wikipedia 3.15 GB Dateigröße.
2. Ermitteln der Artikelnamen in den Unterkategorien der Kategorien 'Augenheilkunde' bzw. 'Ophthalmology'.
Dieser Schritt wurde noch manuell unter Verwendung des Kategorie-Browsers auf der Wikipedia-Hauptseite durchgeführt.
3. Extraktion der Abstracts durch Suche nach den Artikelnamen.
Da es sich um ein XML-Dokument handelt wurde versucht mittels XSLT (Extensible Stylesheet Language Transformation, einer Sprache u.a. zur Extraktion von Teilbäumen eines XML-Dokuments) und regulären Ausdrücken, die Abstracts zu gewinnen.
Verwendet wurde dazu das Kommandozeilenprogramm 'xsltproc'.
Der Aufwand damit eine fehlerfreie Menge an Abstracts zu extrahieren zeigte sich aber als zu groß, insbesondere aufgrund der spärlichen Dokumentation (abgesehen von der technischen Dokumentation des W3C).
Daher wurde die Extraktion mit den üblichen dafür geeigneten Programmen der Unix-Shell (grep, sed, awk) und etwas Perl bewerkstelligt.
Für wiederholte Aufgaben dieser Art, ist eine Einarbeitung in XSLT aber zu empfehlen weil die Verarbeitung sehr großer Dateien, selbst im Vergleich zu den eben genannten Programmen, noch einmal erheblich schneller ist und auch dem eigentlichen Zweck der Verwendung von XML zur Textauszeichnung entspricht.
4. In den Abstracts befinden sich die Kategorie-Tags, die wiederum dem Artikelnamen zugewiesen werden.
Allerdings fanden sich auch mehrere hundert Kategorien, die lediglich der Verwaltung der Wikipedia dienen, und die vorher nicht aufgefallen waren, weil sie bei der Anzeige im Browser unterdrückt werden.
Ein allgemeines Beispiel dafür ist die Kategorie 'Articles needing attention', die selbst wiederum mehrere hundert Unterkategorien enthält (unter anderem zu der Zeit 'Medical Articles needing attention').
Außerdem gibt es Sammelkategorien der Art 'Accuracy disputes from August 2009'.
Je nachdem wie lange der Dissens bezüglich eines Themas schwelt, sind genau so viele Kategorien dieses Typs einem Artikel zugewiesen, wie Monate vergangen sind.
Obwohl vieler dieser Kategorien, einmal identifiziert, durch reguläre Ausdrücke gut zu filtern waren, war es doch ein erheblicher manueller Aufwand.

### Ergebnisse

Die so ermittelten Kategorien wurden als Schlagwörter der dazugehörigen Artikel betrachtet und versucht mit den Begriffen aus dem Wörterbuch der Augenheilkunde in Verbindung zu bringen.
Die resultierenden Merkmalszuweisungen blieben aber hinter den Erwartungen zurück.
Viele Kategorien gehören nur der Ausgangskategorie ('Augenheilkunde', 'ophthalmology') an.
Aufgrund der Mischung von hierarchischer Ordnung und Facettenordnung ist mindestens die Menge der Kategoriebegriffe zu klein um eine erkennbare Vererbung der Kategoriebegriffe auszunutzen; wahrscheinlich ist aber, dass selbst bei einer wesentlich größeren Zahl an Kategorien in der selben Domäne keine wirklich Verbesserung der Situtation einträte, weil dann immer noch vererbte Eigenschaften mit assoziierten Eigenschaften der Kategorie vermischt wären.
Der wesentliche Grund für die geringen Zuweisungen, ist daher die geringe Menge an Überlappungen der Kategorien gewesen.
Im Grunde handelt es sich hierbei um das selbe Problem, wie bei dem Versuch mit der IDC-10 und scheiterte aus dem selben Grund: der Zweck der Klassifikation ist ja die Elimination der Überlappung der Begriffsumfänge und Einordnung in hierarchische Strukturen unter Ausnutzung der Vererbung von Merkmalen.
Der Facettenaspekt in der Klassifikation der Wikipedia-Kategorien brachte hier also kaum Verbesserung.

Die Volltext-Abstracts aus der Wikipedia
----------------------------------------

### Vorüberlegungen

Das Wesen des Lexikonartikels ist, den behandelten Begriff zu beschreiben und zu erklären. Daher findet sich zu Beginn jedes Artikels eine Einordnung des Begriffs in seiner Grundbedeutung.
In der Wikipedia gibt es sehr umfangreiche und präzise Anleitungen, wie der Aufbau eines Artikels zu sein hat.
Insbesondere für Artikel, die schon etwas älter sind und die viele Bearbeiter, insbesondere Domänenspezialisten, hatten, ist die Wahrung der Formvorgaben mit hoher Sicherheit als gegeben zu betrachten.
Gerade der erste Satz folgt damit so gut wie immer dem Schema, welches exemplarisch am nachfolgenden Exzerpt aus der Wikipedia veranschaulicht werden soll:

Augenheilkunde
 :    Die Augenheilkunde (Augenmedizin, fachsprachl.: Ophthalmologie, Ophthalmiatrie; von gr. XXXXXXX ‚Auge‘) ist die Lehre von den Erkrankungen und Funktionsstörungen des Sehorgans, deren Anhangsorgane, sowie des Sehsinnes und deren medizinischer Behandlung.

Die Überlegungen zur Erzeugung von Merkmalszuweisungen wurden daher darauf konzentriert, aus den ersten beiden Sätzen des Abstracts eine Zerlegung in Wort-n-Gramme der Längen 2 und 3 zu erstellen und zu versuchen diese mit den entsprechenden n-Grammen, die aus den Einträgen des Wörterbuchs der Augenheilkunde erzeugt wurden, in Verbindung zu setzen.
Der Grund aus dem die ersten beiden Sätze und nicht nur der erste Satz herangezogen wurden ist, dass bei manchen Artikeln der erste Satz nur aus einer etymologischen Einordnung besteht ohne weitere Erklärung des Begriffs.
Die Zerlegung in Wort-n-Gramme, im Unterschied zu Zeichen-n-Grammen, befreit allerdings nicht von typischen Problemen bei dieser Art Aufgabe, die entstehen durch Unterschiede in Genus, Numerus, Kasus, Tempus usw. bei gleichem Wortstamm.
Aus diesem Grund wurden die Abstracts vorher mit Stemming auf ihren Wortstamm zurückgeführt (im Rahmen der Möglichkeiten des verwendeten Stemmers).
Hierzu wurde die ANSI-C-Implementation des Porter-Stemmers verwendet, jeweils in Standardeinstellung für die englische Sprache und mit angepassten Mustern für die deutsche Sprache (die angepassten Muster sind Teil des Programms).
Die resultierende Liste von n-Grammen je Artikel, wurde zusammen mit dem Artikelnamen in einer Pseudo-XML-Notation (die n-Gramme wurden in Tags namens <bigram></bigram> und <trigram></trigram> gespeichert ohne sich weiter mit einer geeigneten Document Type Definition aufzuhalten. Die Ketten sollten aus der Datei nur gut extrahierbar sein) gespeichert.

### Vorgehensweise

1. Shell-Skripte (grep, sed, awk et al.) zur Extraktion der ersten beiden Sätze.
Da sowohl das Wiki-Markup, als auch Schriftzeichen anderer Sprachen (insbesondere Altgriechisch, Arabisch und Indisch) herausgefiltert werden mussten, zum Teil mit manuellem Eingriff und Korrektur
(auch hier gilt, was an anderer Stelle schon bemerkt wurde: manche der manuell ausgeführten Arbeiten sind prinzipiell automatisierbar, allerdings erschien zum relevanten Zeitpunkt der Aufwand dafür, gegeben dass es sich um eine einmalige Aufgabe handelte, als nicht geboten. In jedem Fall wurde aber darauf geachtet, die Schritte so zu wählen, dass sie automatisierbar sein können).
2. Shell-Skript für den Einsatz des Porter-Stemmers und anschließendes Speichern. Dieser Schritt geht vollautomatisch und ohne Bedarf weiterer Überprüfung oder Korrektur.
3. PHP-Skripte für den Import der XML-Daten in die Datenbank.
4. Zuweisung der Merkmale, sowie Matching der Artikeltitel und der Synsetbezeichnungen via SQL.

### Ergebnisse

Das Ergebnis zeigte sich bezüglich der Ausbeute an Merkmalen und der Anzahl an Zuweisungen je Begriff als unbefriedigend. Zwar wurden insgesamt ca. 5000 Merkmale produziert, jedoch befindet sich darunter jede Menge Ballast in Form von irrelevanten oder aus dem Kontext heraus falsch extrahierten Daten (z.B. is_a als Merkmal, da als Wikipedia-Eintrag vorhanden). Zudem ist bei insgesamt ca. 7000 Merkmalszuweisungen jedes Merkmal im Schnitt 1,4 mal zugewiesen worden, was extrem wenig ist. Es gibt nur ca. 500 Merkmale, die öfters als 3 mal zugewiesen wurden. Auch das Matching der Artikelnamen auf die Synsets bleibt mit einem Wert von 266 erkannten Synsets bei 626 Lexikonartikeln hinter den Erwartungen zurück.

Daher wurde ein zweiter Durchlauf der selben Daten allerdings nach vorheriger Bereinigung um Stoppworte durchgeführt.
Die Quellen der verwendeten Stoppwortlisten sind im Anhang aufgeführt.

Auch hier blieb das Ergebnis hinter den Erwartungen zurück. Die Merkmalsanzahl blieb nahezu unverändert, Zuweisungen haben sich gut um 1000 reduziert. Dank großzügigerem Matching mit Nichtbeachtung von Groß- und Kleinschreibung konnten ca. 30 Synsets mehr auf Artikel abgebildet werden, aber auch das ändert die Einschätzung des Endresultates nicht. Positiv herauszustellen ist jedoch die Erzeugung eines etwas bereinigteren Begriffsverbandes, da Merkmale wie is_a nicht mehr zustande kommen aufgrund der Stoppwortfilterung.


Inhalte der Wikipedia via dem API
=================================

### Vorüberlegungen

Die Gründe aus dem der Dump der Wikipedia-Abstracts verwendet worden waren sind

* es musste kein 'Crawler' geschrieben werden, der immer wieder neu auf die Seiten losgelassen wurde
* es war anfangs auch nicht zu überblicken, ob und welche Kategorien noch hinzugenommen werden sollten
* die Hoffnung, dass der reine Text mit Wiki-Markup, statt dem daraus generierten (X)HTML der dann gecrawlten Seiten, leichter zu erschließen sein würde.

Insbesondere der letzte Punkt stellte sich als nicht zutreffend heraus.
Im Frühjahr 2012 wurde das API für Anfragen (query.php) der Wikipedia stark überarbeitet und in der Funktionalität ausgebaut.
Insbesondere die Ausgabe der Inhalte als reiner Text, frei von Wiki-Markup, stellte eine erhebliche Verbesserung der Möglichkeiten der maschinellen Weiterverarbeitung dar.
Das API bietet seitdem sogar die Möglichkeit eine beliebige Anzahl von Sätzen, gezählt von Beginn des Artikels an, auszugeben. Allerdings scheitert das gelegentlich daran, dass das Kriterium für das Ende eines Satzes allein der Punkt ist, so dass Sätze bereits nach 'Dr.', 'Prof.' und 'et al.' enden.
Für diese Fälle musste der restliche erste Satz manuell geholt werden.

Da die Ansätze lediglich die Kategorien und später die gestemmten, stoppwortbereinigten und zu Wort-n-Grammen reduzierten ersten Sätze zusammen mit den Kategorien zu verwenden keinen Erfolg brachten, sollte untersucht werden, ob möglicherweise schon die 'merkmalsenthaltenden' Teile des ersten Satzes genügen, um bessere Merkmale zu bekommen.
Dazu sollten Nomen und Adjektive des ersten Satzes gesammelt und als Merkmale zugewiesen werden.
Die Nomen sollten in erster Linie dazu dienen Überschneidungen mit anderen Begriffen zu begünstigen, während sich von den Adjektiven erhofft wurde kleinere Menge beschränkt zu bleiben, die zum Beispiel nur

* Lageinformation wie in der Anatomie (zum Beispiel 'vorne, hinter, über, in, teilt, beinhaltet' usw.) und
* Bezeichnungen aus dem näheren Umfeld von Krankheiten (zum Beispiel 'fiebrig, geschwollen, eiternd' usw.)

und ähnlichem umfasst. Die Erwartung war in größerer Menge die Überschneidungen in der Merkmalsmenge zu bekommen, die erforderlich sind, um überhaupt etwas analysieren zu können, mit der formalen Begriffanalyse.

Wie bereits erwähnt, ist der erste Satz eines enzyklopädischen Artikels im Grunde immer identisch aufgebaut.
Es findet sich darin der Begriff, der Gegenstand des Artikels ist, selbst, sowie adjektivische Elemente die den Begriff einordnen in den Rahmen der durch die eine hierarchische Relation implizierende Wendung 'ist ein', 'ist der/die/das' etc. gesteckt wird.
Ein Beispiel dafür ist der erste Satz des Artikels *Hornhaut*:

Hornhaut
  :    Die Hornhaut (lateinisch Cornea, eingedeutscht auch Kornea, griechisch keratos) ist der glasklare, von Tränenflüssigkeit benetzte, gewölbte vordere Teil der äußeren Augenhaut.

Da es mit einem Part-of-Speech-Tagger vergleichsweise einfach ist, die entsprechenden Teile zu extrahieren, sollte der Versuch unternommen werden dem Merkmalscharakter möglichst nahe zu kommen, indem einfach die Wörter, die unmittelbar verwendet werden, um den in Frage stehenden Begriff zu beschreiben, als Merkmale verwendet werden.
Die Wahrscheinlichkeit einerseits möglichst treffende Begriffe zu finden und andererseits nicht zu viele nicht in unmittelbaren Zusammenhang stehende Wörter zuzuweisen, schien mit dem ersten Satz eines enzyklpädischen Artikels maximal.

### Vorgehensweise

Anders als bei der Extraktion aus dem Dump wurden die Seiten von einem Shell-Skript aus mit wget geholt und sofort weiterverarbeitet.
Für das Part-of-Speech-Tagging wurde der TreeTagger von Helmut Schmid von der Universität Stuttgart verwendet.
Er enthält sogenannte 'parameter files' für eine Vielzahl von Sprachen.
Vor allem aber ist das Programm ohne große Konfiguration recht schnell und verarbeitet Standarddatenströme der Unix-Shell, so dass es sich gut in Shell-Skripten verwenden lässt. Die genaue Vorgehensweise war:

1. Ausgehend von der Kategorie 'Eye' rekursiv alle ersten Sätze aller Artikel in allen Unterkategorien holen.
Bei Verwendung des API ist die Standardeinstellung, dass die oben erwähnten Verwaltungskategorien nicht beachtet werden.
Man erhält also sofort eine wesentliche fehlerfreiere Menge von Artikeln.
Auf diese Weise wurden 118 Kategorien und 2415 von 2841 möglichen Artikeln geholt.
Die Abweichung ergibt sich zu etwa zwei Dritteln aus Verbindungsabbrüchen nach fünf Versuchen.
Das Programm wget hat sehr elaborierte Möglichkeiten, um sein Retrievalverhalten wie das einer natürlichen Person, die mittels Web-Browser die Seiten besucht, aussehen zu lassen.
Das ist notwendig, weil auch die Wikipedia-Server zu hochfrequente Verbindungsanfragen drosseln (und bei drastischem Überschreiten IP-Adressen sperren), basierend auf der IP-Adresse und der absoluten Frequenz der Anfragen.
Um die Server zu schonen und die Zugriffe nicht so auffällig zu machen, wurden die Zugriffe unter anderem auf einen Zufallswert zwischen einer und 60 Sekunden eingestellt, die Download-Rate auf 5 Kb/s gedrosselt, und wie gesagt die Anzahl der Verbindungsversuche je Artikel auf fünf beschränkt.
Etwa 1300 der 2415 Artikel sind Namen natürlicher Personen.
Der Grund dafür ist, dass ein ganzer Bereich unterhalb der Kategorie 'Eye' einerseits berühmte Augenärzte und Wissenschaftler der Augenheilkunde beinhaltet [Grafik].
Dieser Teil ist vermutlich nicht unmittelbar als Ballast anzusehen.
Ein anderer Bereich hingegen gehört zu Unterkategorien der Kategorie 'blindness' und dort tauchen sämtliche Personenartikel in der Wikipedia auf, deren Gegenstand auch ein blinder Mensch ist
(diese Umfassen unter anderem Kategorien wie 'blind academics', 'fictional blind characters' oder 'sportspeople with a vision impairment'.
In letzterer Katgorie finden sich tatsächlich auch Leute, die nicht blind sind.
Formal sind diese Artikel aber alle Mitglieder der Oberkategorie 'blindness' via der Kategorie 'blind people'. Ein weiterer Hinweis auf die Probleme der Mischung aus facettierter und streng hierarchischer Klassifikation in der Wikipedia.)
2. Nach kleineren Filterschritten durch die üblichen Programme [wird ausgeführt, Hinweis auf Anhang??], musste bei 58 Artikeln manuell der erste Satz hinzugefügt werden, weil der erste Punkt im Satz der Punkt nach einer Abkürzung war.
(später ist bei genauerer Betrachtung aufgefallen, dass es Artikel gab, die trotzdem vollständig waren, obwohl vor dem Satzende ein Punkt war.
Das deutet darauf hin, dass diese Fehlerrate auch absolut höher hätte sein können und die Vorgehensweise vermutlich nicht ohne manuelle Kontrolle auskommt.
Allerdings waren die Artikel relativ leicht zu finden indem mit awk die durchschnittliche Satzlänge aller Artikel berechnet wurde und die Artikel ausgegeben wurden, deren Satzlänge $\geq 2$ Standardabweichungen vom Mittelwert abwich.
Diese Vorgehensweise ist zwar auch nicht vollständig reliabel, aber gut als Postprocessing-Schritt einzubauen.)
Die Ergebnisse wurden an TreeTagger übergeben und die Ausgabe von TreeTagger gefiltert, so dass nur die Stammformen der Nomen und Adjektive gespeichert wurden.
(TreeTagger verwendet die Nomenklatur des Penn Treebank Project.
Gespeichert wurden alle Vorkommen von JJ* (also JJ - Adjektiv, JJR - Adjektiv komparativ und JJS - Adjektiv Superlativ) und NN* (also NN - Nomen Singular, NNS - Nomen Plural, NNP und NNPS für Eigennamen respektive).
3. Nach weiteren Filterschritten [ausführen?] werden die Ergebnisse zusammen mit dem Artikelnamen und den Kategorien, die in einem separaten Schritt geholt wurden, gespeichert.
Auf das finale Speichern der Part-of-Speech-Information wurde verzichtet.

Das Ergebnis wurde wie folgt gespeichert, die Zahl am Anfang ist eine durchlaufende Nummer je Begriff, die kursiv hervorgehobenen Merkmale sind Kategorien.
Jeweils vorangestellt ist der ursprüngliche Satz.

Das erste Beispiel ist ein eher erfolgreiches Resultat des Ansatzes, das zweite Beispiel ist ein typischer Fall für die weniger brauchbaren Ergebnisse.

Keratoprosthesis
  :    is a surgical procedure where a severely damaged or diseased cornea is replaced with an artificial cornea.

    69,Keratoprosthesis,surgical
    69,Keratoprosthesis,procedure
    69,Keratoprosthesis,damaged
    69,Keratoprosthesis,diseased
    69,Keratoprosthesis,artificial
    69,Keratoprosthesis,*Ophthalmology*

Die zusätzliche Kategorie bringt hier keine besonderen Zugewinne, weil sie eine der neun unmittelbaren Unterkategorien von 'eye' ist und damit allein zu allgemein ist.

A scleral lens
  :    is a large lens that rests on the sclera and creates a tear-filled vault over the cornea.

    185,Scleral lens,large
    185,Scleral lens,vault
    185,Scleral lens,*contact lenses*
    185,Scleral lens,*corrective lenses*

Dadurch, dass bei der Verarbeitung in Schritt 3 die Bestandteile des Artikelnamens 'scleral' und 'lens' herausgefiltert werden, bleibt nicht mehr viel nützliches übrig.
Zu überlegen ist, ob man bei einer Unterschreitung einer Anzahl Ergebniszeilen, den oder die Begriffe aus denen sich der Artikel zusammensetzt, hinzunimmt.
Allerdings geben die beiden Kategorien hinreichend Information um 'scleral lens' zumindest einordnen zu können.

### Ergebnisse

Insgesamt wurden 1379 Wikipedia-Abstracts analysiert, aus denen 2439 Merkmale extrahiert werden konnten, die 9797 mal entsprechenden Artikeln zugeordnet wurden. Nach Matching der Artikelnamen auf Synsets aus dem Wörterbuch kommt man auf (nur) 335 gematchte Synsets, auf die insgesamt 931 Merkmale 2582 mal zugewiesen wurden. Im Gegensatz zu den ersten Durchläufen der Wikipedia-Extraktion ist die Ausbeute an Merkmalen damit deutlich geringer, dafür konnten aber mehr Synsets identifiziert und die Vernetzung der Merkmalszuweisungen signifikant erhöht werden (ungefähr um den Faktor 2). Zudem ist der resultierende Begriffsverband deutlich bereinigter als zuvor.

Damit kann konstantiert werden, dass diese Methode allein keinen hinreichend aussagekräftigen Begriffsverband für das Wörterbuch generiert hat, jedoch als sinnvolle Ergänzung zu den bereits angewandten Methoden gesehen werden kann.

### Bilden der Begriffsverbände und Visualisierung (unser Script)

Schlußteil
----------

### Diskussion der Ergebnisse

### Diskussion der Probleme

### Ausblick (SNOMED, Merkmalsmenge einschränken)

### Schlussbemerkungen

