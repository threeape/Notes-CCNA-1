
# Kapitel 3: Protokolle und Netzwerkkommunikation

## Struktur einer Kommunikation

Jede Kommunikation kann durch 5 Hauptelemente dargestellt werden und die Kommunikation zwischen Computern ist keine Ausnahme:

* Die Quelle der zu sendenden Nachricht (Die Quellmaschine)
* Der Signalsender (die Quellnetzwerkkarte)
* Das Übertragungsmedium (Kupfer, Luft oder Glasfaser)
* Nachrichtenempfänger (Zielnetzwerkkarte)
* Nachrichtenempfänger (Zielmaschine)

Um richtig zu kommunizieren, müssen sich Maschinen auf eine gemeinsame Kommunikationssprache einigen. Dies wird *Protokoll* genannt. Es gibt eine große Anzahl von ihnen, die standardisiert sind, um eine korrekte Kommunikation zu ermöglichen. Dieses Protokoll definiert die Informationen, die der Quellcomputer bereitstellen muss, um vom Netzwerk verstanden zu werden.

Um die Nachricht korrekt zu übertragen, verwenden die Maschinen nicht ein einziges Protokoll, sondern eine Reihe von Protokollen, die jedem von ihnen neue Informationen hinzufügen, damit die Nachricht übertragen werden kann. Diese Organisation wird als *Suite of Protocols* bezeichnet. Somit wird die zu sendende Nachricht von jedem der Protokolle eingekapselt, die ihre Übertragung ermöglichen.

### Codierung

Für die Übertragung müssen die zu versendenden Daten einer Transformation unterzogen werden, um sie mit dem verwendeten Übertragungsmedium und dem verwendeten Protokoll kompatibel zu machen. Diese Operation wird *Codierung* genannt

> Beispiel: Bei einem Telefongespräch wird jeder empfangene Ton in Form eines Bits kodiert und an den Empfänger gesendet, der den Ton aus den erhaltenen Informationen rekonstruiert.

### Verpackung

Die Rohnachricht, auch verschlüsselt, kann nicht so wie sie im Netz ist versendet werden, sie muss mit weiteren Informationen wie dem Empfänger des Briefes oder dem Absender versehen werden. Diese Informationen werden am Anfang oder am Ende der zu sendenden Nachricht hinzugefügt. Die Kapselung besteht dann aus dem Hinzufügen von Informationen zur Rohnachricht gemäß den vom Netzwerk benötigten Informationen. Die gesamte eingekapselte Nachricht wird *Frame* genannt und kann über das Netzwerk gesendet werden. Es kann mehrere Kapselungsphasen einer Nachricht geben.

Bei einem HTTP-Frame wird beispielsweise der Inhalt der anzuzeigenden Seite in den Benutzerdaten gefunden, dann fügt eine Kapselungsserie Informationen zum Frame hinzu, um sein Ziel, die Version der verwendeten Protokolle und viele andere anzugeben .'anderes Zeug.

![Une trame HTTP](img/tramehttp.png)


### Schneiden

Um das für die Übertragung verwendete Protokoll zu respektieren, kann die Nachricht in mehrere *Frames* unterteilt werden, wodurch das Netzwerk nicht verstopft wird.

### Frame-Synchronisation und -Verwaltung

Wenn zwei Hosts gleichzeitig einen Frame im Netzwerk senden, kommt es zu einer *Kollision*. Um so etwas zu vermeiden, muss das Protokoll eine *Zugriffsmethode* definieren, die definiert, wann die Hosts sprechen sollen und was im Fehlerfall zu tun ist.

Um eine Verstopfung des Netzwerks zu vermeiden, muss das Protokoll auch ein Schema zur *Flusskontrolle* angeben, um jedem Host die Möglichkeit zu geben, Daten über das Netzwerk zu senden.

Schließlich muss das Protokoll auch ein *Timeout* definieren, dessen Überschreitung es dem sendenden Host ohne Antwort ermöglicht, davon auszugehen, dass keine Antwort gegeben wurde.

### Sendemethode

Das Senden eines Frames kann auf 3 verschiedene Arten erfolgen:

* **Unicast** Wir senden den Frame an einen einzigen Host
* **Multicast** Wir senden den Frame an eine Gruppe von Hosts
* **Broadcast** Wir senden den Frame an alle Hosts im Netzwerk

Jeder der Rahmen kann eine Bestätigung erfordern oder nicht.

## Netzwerkprotokoll

Die Protokolle, die die Netzwerke regeln, sind definierte, präzise und von allen Maschinen akzeptierte Protokolle, die sie verwenden. Es gibt viele Protokolle und diese Protokolle sind in *Protokollsuiten* organisiert, um eine gute Kommunikation zu ermöglichen.

Ein Protokoll kann sein:

* **Offen** Es wird dann von einem Standardisierungsgremium standardisiert und kann überall und von allen verwendet werden
* **Eigentümer** Es wird dann von der Firma, die es erstellt hat, standardisiert und kann nur von dieser gleichen Firma verwendet werden.

Es gibt viele Arten von Protokollen, aber hier sind einige Beispiele

![Quelques piles de protocoles](img/protocoles.png)

Die TCP/IP-Protokollfamilie besteht heute aus vielen der in der folgenden Abbildung angegebenen Protokolle.

![Suite de protocoles TCP/IP](img/protocolsEnCouches.png)


Protokolle werden in Schichten gestapelt. Um ein Anwendungsprotokoll zu verwenden, müssen wir dann ein oder mehrere Protokolle pro unterer Schicht verwenden und die Kapselung durchführen.

### Anwendungsprotokolle

* **DNS** Für Domain Name System, übersetzt Domänennamen in IP-Adressen
* **BOOTP** Vorgänger von DHCP, ermöglicht es einem Rechner, seine IP im Netzwerk zu kennen
* **DHCP** Für die dynamische Hostkonfiguration weist Clients IP-Adressen dynamisch zu und ermöglicht die Wiederverwendung nicht verwendeter IP-Adressen.
* **SMTP** Für Simple Mail Transfer Protocol, ermöglicht es dem Client, eine E-Mail an einen Mailserver zu senden, und dem Server, diese E-Mail an andere Server zu senden
* **POP** Für Post Office Protocol, ermöglicht Ihnen das Abrufen von E-Mails von einem Mailserver, diese E-Mails werden vom Server auf den Desktop heruntergeladen
* **IMAP** Für Internet Message Access Protocol, ermöglicht den Zugriff auf E-Mails von einem Mailserver und speichert diese E-Mails remote
* **FTP** Definiert für File Transfer Protocol die Regeln, die es dem Benutzer eines Hosts ermöglichen, auf Dateien auf einem anderen Host im Netzwerk zuzugreifen und Dateien an diesen Remote-Host zu übertragen
* **TFTP** Für Trivial File Transfer Protocol, ermöglicht die Übertragung einfacher Dateien ohne Verbindung und ohne Empfangsbestätigung
* **HTTP** Für Hypertext Transfer Protocol, ermöglicht Ihnen die Übertragung von Medien, Text und Grafiken im Internet.

### Transportprotokolle

* **UDP** Für User Datagram Protocol, ermöglicht die Übertragung von Paketen von einem Host zum anderen ohne Empfangsbestätigung.
* **TCP** Für Transmission Control Protocol, ermöglicht eine zuverlässige Kommunikation zwischen den Prozessen zweier entfernter Hosts mit Bestätigung

### Internetprotokolle

* **IP** Für das Internetprotokoll, das verwendet wird, um Nachrichten in Paketen zu gruppieren und die Zieladresse anzugeben
* **NAT** Konvertiert lokale Adressen in globale Adressen im globalen Netzwerk
* **ICMP** Für das Internet Control Message Protocol, ermöglicht die Benachrichtigung des entfernten Hosts über Fehler, die während der Übertragung auftreten
* **OSPF** Für Open Shortest Path First, ermöglicht das Routing von Paketen in die richtige Richtung durch ein hierarchisches Design von Bereichen
* **EIGRP** Für das Enhaces Interior Gateway Routing Protocol, ein proprietäres Protokoll von Cisco, das es ermöglicht, eine geeignete Metrik entsprechend der Bandbreite anzugeben

### Netzwerkzugriffsprotokolle

* **ARP** für das Address Resolution Protocol, bietet eine dynamische Zuordnung zwischen einer IP-Adresse und einer physikalischen Adresse
* **PPP** Ermöglicht für das Piont-to-Point-Protokoll die Kapselung der Pakete, um sie über eine serielle Verbindung zu übertragen
* **Ethernet** Das lokal am häufigsten verwendete Protokoll, mit dem Verkabelungs- und Signalisierungsregeln definiert werden können
* **Schnittstellentreiber** Weist den Computer an, mit seinen Netzwerkschnittstellen zu kommunizieren

## Offene Standards

Mit einem offenen Standard können Sie:

* Förderung der Produktkompatibilität
* Verhindern Sie das Monopol eines Produkts

Ein offener Standard wird von einem Standardisierungsgremium verwaltet, bei dem es sich meist um einen gemeinnützigen Verein handelt, der nicht mit Herstellern verbunden ist.

### Internet-Standardisierungsgremien

* **ISOC** Für die Internet Society, zuständig für die Förderung eines freien Internets
* **IAB** Für Internet Architecture Board, ein Komitee, das für die Verwaltung und Entwicklung von Internetstandards zuständig ist
* **IETF** Für die Internet Engineering Task Force, eine Arbeitsgruppe, die für die Entwicklung, Aktualisierung und Verwaltung von Internet- und TCP/IP-Technologien durch Standardisierungsdokumente wie RFCs verantwortlich ist
* **IRTF** Für die Internet Research Task Force, eine langjährige Internet- und TCP/IP-Forschungs-Task Force in den Bereichen Kryptografie, Anti-Spam und Peer-to-Peer
* **ICANN** For Internet Corporation for Assigned Names and Numbers, eine Vereinigung, die die Zuweisung von IP-Adressen und die Verwaltung von Domänennamen koordiniert
* **IANA** Für Internet Assigned Numbers Authority, eine Behörde, die für die Überwachung der für ICANN verwendeten IP-Adressen und Protokolle verantwortlich ist

### Elektronische Standardisierungsorganisationen und Kommunikation

* **IEEE** Für Institute of Electrical and Electronics Engineers
* **EIA** Für Electronic Industries Alliance, Handelsallianz zur Standardisierung von Kabeln und Kommunikation insbesondere in Racks
* **TIA** Für die Telecommunications Industry Association, eine Vereinigung, die für Kommunikationsstandards in vielen Bereichen verantwortlich ist
* **ITU-T** Für den Telecommunication Standardization Sector der International Telecommunication Union, eine der ältesten Standardisierungsorganisationen, die Videokomprimierungsstandards definiert.

## Schichtenmodell

Wir stellen unser Netzwerk nun in aufeinanderfolgenden Schichten dar, indem wir 2 Modelle befolgen:

* **Protokollmodell** Dieses Modell folgt einer definierten Protokollsuite, diese Funktion wird vom TCP/IP-Modell bereitgestellt
* **Referenzmodell** Stellt die allgemeine Konsistenz jeder auszuführenden Operation in jeder Schicht sicher, dieses Modell wird vom OSI-Modell bereitgestellt

![Comparaison des deux modèles](img/deuxmodèles.png)

### OSI-Modell

Das ISO-Modell besteht aus 7 aufeinanderfolgenden Schichten:

* **7.Application** Enthält Protokolle, die für die Prozess-zu-Prozess-Kommunikation verwendet werden
* **6.Präsentation** Bietet eine gemeinsame Darstellung von Daten, die zwischen Diensten der Anwendungsschicht übertragen werden
* **5.Session** Stellt Dienste für die Präsentationsschicht bereit, um ihren Dialog zu organisieren und den Datenaustausch zu verwalten
* **4.Transport** Definiert Dienste zum Segmentieren, Übertragen und Wiederzusammensetzen individueller Kommunikationsdaten zwischen Endgeräten
* **3.Netzwerk** Bietet Dienste zum Austausch einzelner Daten über das Netzwerk zwischen identifizierten Endgeräten
* **2.Data Link** Data Link beschreibt Verfahren zum Austausch von Datenrahmen zwischen Geräten über ein gemeinsames Medium
* **1.Physisch** Beschreiben Sie die mechanischen, elektrischen, funktionalen und methodischen Mittel zum Aktivieren, Verwalten und Deaktivieren physischer Verbindungen für die Übertragung von Bits zu und von einem Netzwerkgerät.

### TCP/IP-Modell

Bestehend aus nur 4 Schichten, die durch die verwendeten Protokolle definiert sind:

* **4.Anwendung** Nützliche Benutzerdaten und Dialogsteuerung
* **3.Transport** Unterstützt die Kommunikation zwischen mehreren Geräten über das Netzwerk
* **2.Internet** Ermittelt den besten Netzwerkpfad
* **1.Netzwerkzugriff** Steuert die Hardwaregeräte und Medien, aus denen das Netzwerk besteht

## Datentransfer

Die zu übertragenden Daten können nicht auf einmal gesendet werden, da dies zu Datenproblemen führen würde. Es müssen zwei Systeme berücksichtigt werden, die es ermöglichen, den Datenfluss zu optimieren und allen die Möglichkeit zur Kommunikation zu geben

### Segmentierung

Um die zu übertragende Datenmenge zu reduzieren, werden die Daten in mehrere unterschiedliche Frames aufgeteilt.

### Multiplexing

Um jedem Host die Möglichkeit zu geben, zu kommunizieren, werden die Daten jedes Hosts gemischt, wodurch die übertragenen Pakete gemischt werden können.

### Frames umwandeln

Während der Übertragung von Daten durch eine Anwendung durchlaufen die Daten den Stapel von Protokollen, wodurch es möglich wird, die Daten einzukapseln, um auf dem Kommunikationskanal zu landen.

1. Deals werden gemacht, um versendet zu werden
2. Daten werden in Segmente unterteilt
3. Segmente werden entsprechend dem Protokollstapel gekapselt
4. Pakete sollen über das Netzwerk gesendet werden
5. Die Bits des Frames sind auf dem physischen Medium zu sehen

![Pile d'encapsulation](img/pileproto.png)

### Entkapselung

Wenn der Frame empfangen wird, werden die Daten in der entgegengesetzten Richtung der Kapselung entkapselt.

![Desencapsulation](img/desen.png)

### Netzwerkadressen

Um zu kommunizieren, benötigen Sie ein paar Adressen.

* **Quelladresse** woher die Daten kommen
* **Zieladresse**, an die die Daten gesendet werden

Jede der Schichten hat ihre eigene Übertragungsmethode, aber die Adressen werden nur in der Vermittlungsschicht und der Datenverbindungsschicht verwendet.

* **Data Link Layer** (MAC-Adresse) Die Adresse wird für die Übertragung von Karte zu Karte im selben Netzwerk verwendet. Somit ändert sich der Rahmen dieser Schicht, sobald er über einen Router in ein anderes Netz übertragen wird.
* **Netzwerkschicht** (IP-Adresse) Die Adresse wird von der Quelle bis zum Ziel verwendet, auch wenn sie sich nicht im selben Netzwerk befinden, sie besteht aus einem Netzwerkteil und einem Hostteil

![Structure des adresses](img/adressage.png)
