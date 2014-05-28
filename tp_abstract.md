Abstract
================================================================================

Das Wörterbuch der Augenheilkunde ist eine online verfügbare Ressource mit 24.000+ Begriffen aus dem Bereich der Augenheilkunde verteilt auf 13 Sprachen.
<!-- The Dictionary of Ophthalmology is an online resource containing more than 24.000 terms specific to ophthalmology distributed over 13 languages. -->

Zu jedem Begriff werden neben Bildern, Abkürzungen und weiteren Informationen die verfügbaren Übersetzungen, sowie bekannte Synonyme präsentiert.
<!-- ----------------------------------------------------------------------------------------- -->
<!-- Im Konferenz-Abstract Tilburg steht '...arranged by synonymy...': wie beschreibt man das am Besten auf deutsch? -->
<!-- Vielleicht 'geordnet anhand von Synonymen'? -->
<!-- ----------------------------------------------------------------------------------------- -->
<!-- Ich muss gestehen, ich habe das nicht verstanden und daher die Formulierung '...sowie bekannte Synonyme...' gewählt. -->
<!-- ----------------------------------------------------------------------------------------- -->
<!-- ----------------------------------------------------------------------------------------- -->
<!-- Each term is presented together with its available translations and other synonyms, many are accompanied with images. -->

Ziel des Wörterbuchs ist es den Augenarzt im Umgang mit fremdsprachlichen Arztbriefen oder Berichten zu unterstützen. 
<!-- The Dictionary of Ophthalmology aims to support the practitioner in dealing with medical reports of patients written in foreign languages. -->

Die Übersetzungen können jedoch auch fehlerhaft sein (Zeitz & Petersen, 2013) und die verfügbaren Übersetzungen sind sehr ungleichmäßig über die Sprachen verteilt.
<!-- But some translations may be erroneous (Zeitz & Petersen, 2013) and the translations available in the dictionary are very unevenly distributed across the 13 languages. -->

Weiterhin existieren bestimmte Begriffe nur in manchen Sprachen als Wort oder Phrase, andere sind weiter verbreitet.
<!-- Furthermore there may be medical terms existing only in some languages as a word or phrase while other terms are commonplace in most languages. -->

Es sollen Ansätze und Methoden der Merkmalsextraktion präsentiert werden, um ein solches Wörterbuch halbautomatisch mit den fehlenden Übersetzungen zu ergänzen.
<!-- Hier habe ich noch das Problem, dass wir von Merkmalen sprechen, aber FCA und Janssen erst danach erwähnt werden. Wir müssten eigentlich explizieren welcher Art die Merkmale sind (lexikalische Merkmale, semantische Merkmale, usw.), oder diesen Satz erst später bringen. -->
<!-- Folgend habe ich dieses Problem umgangen, indem ich den Begriff descriptive keywords verwende und das Prinzip des Taggings mit reingebracht habe. -->

<!-- We will present methods for extracting descriptive keywords from various sources with which we enrich the dictionary semi-automatically by tagging relating terms with them in order to bridge missing or erroneous translations. --> 

<!-- Im folgenden Satz: welche Zuweisungen? -->
Die Zuweisungen erfolgen über die gemeinsamen Merkmale der Begriffe, um daraus schließlich einen Begriffsverband bilden zu können (Ganter & Wille, 1999).
<!-- With the resulting set of keywords and their respective term-assignments we aim to establish a Formal Concept (Ganter & Wille, 1999) in which the extracted keywords serve as features for describing formal objects that represent the dictionary's terms.

Commonly distributed subsets of features point to similar objects within the Formal Concept and shape a semantic network. -->
<!-- ANMERKUNG zu vorheriger Zeile: ich weiß nicht sicher, was Du mit 'commonly distributed' meinst. Vielleicht so etwas wie 'Subsets that share feature point [...]'? -->

Begriffsverbände eignen sich als Zwischensprache, weil angenommen wird, dass die verwendeten Merkmale als Wort in allen Sprachen existieren und mit ihnen ophthalmologische Begriffe als formale Begriffe dargestellt werden können.
<!-- A Formal Concept is suitable for describing an Interlingua, because it is assumed that lexical representations of our used features exist in all languages and can therefore be used to constitute opthalmological terms as formal objects. -->

Damit folgen wir dem Ansatz von Janssen, 2004.
<!-- By doing this we follow the approach of Janssen, 2004. -->

Die für den Aufbau der Begriffsverbände nötigen Merkmale werden aus gegebenen Klassifikationen, aus Wortteilextraktionen und aus einfacher syntaktischer Extraktion durch Wortartenerkennung gewonnen.
Hierzu wurden die Internationale Klassifikation der Krankheiten (ICD-10), die englischsprachige Wikipedia im Bereich der Augenheilkunde und andere Quellen herangezogen.
<!-- The data for the extraction of features came from the World Health Organizations International Classfication of Diseases, the english language part of Wikipedia and some additional sources. --> 
<!-- Using a part-of-speech tagger and distinct word affixes in the field of ophthalmology provided the features necessary to build formal concepts. -->
<!-- ANMERKUNG zu vorheriger Zeile: ich habe schon wieder vergessen, wie wir 'Begriffsverband/Begriffsverbände' übersetzt haben. -->

Für die Darstellung der Begriffsverbände eignen sich Ordnungsdiagramme.
<!-- The results are visualized with the help of Hasse-diagrams. -->

Mit einer auf Ordnungsdiagrammen basierenden interaktiven Nutzerschnittstelle versetzen wir Augenärzte in die Lage, weiterführende Begriffe anhand der Bedeutungsähnlichkeit bereits bekannter Begriffe zu erschließen und den kompletten Begriffsverband zu erforschen.

<!-- The nodes in the Hasse-diagrams are hyperlinks and thus provide the means for the practitioner to swiftly navigate related terms. -->
<!-- ANMERKUNG zu vorheriger Zeile (deutsch): soll man nochmal explizieren, wie die Ähnlichkeit gemessen wird? --> 

Wir diskutieren die verfolgten Ansätze, die entstandenen Probleme, sowie die Eignung der verwendeten Quellen für entsprechende Arten der Extraktion und Möglichkeiten, die Ansätze zu verbessern.

<!-- Finally we discuss the problems encountered with gathering the data and extracting the features. -->
<!-- We present the different attempts made to overcome these problems and discuss ways to improve on the methods used. -->

Schließlich präsentieren wir die Ergebnisse und die Visualisierung der auf diese Weise erstellten Begriffsverbände.
<!-- ANMERKUNG zu voheriger Zeile: das wäre dann vermutlich im Umfang ähnlich, wie am Ende des Berichts, also ein, zwei Verbände etc.? -->


