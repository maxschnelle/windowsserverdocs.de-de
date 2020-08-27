---
ms.assetid: 87bca912-b912-4bbe-9533-2c34a7abc52d
title: Bestimmen der Anzahl der erforderlichen Domänen
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: 8fe9e6d50bef530d50ba8e7a33432fe2613b871b
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939350"
---
# <a name="determining-the-number-of-domains-required"></a>Bestimmen der Anzahl der erforderlichen Domänen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Jede Gesamtstruktur beginnt mit einer einzelnen Domäne. Die maximale Anzahl von Benutzern, die eine einzelne Domänen Gesamtstruktur enthalten kann, basiert auf der langsamsten Verknüpfung, die die Replikation zwischen Domänen Controllern und der verfügbaren Bandbreite, die Sie Active Directory Domain Services (AD DS) zuweisen möchten, unterstützen muss. In der folgenden Tabelle ist die maximale Anzahl empfohlener Benutzer aufgeführt, die eine Domäne basierend auf einer einzelnen Domänen Gesamtstruktur, der Geschwindigkeit der langsamsten Verbindung und dem Prozentsatz der Bandbreite, die Sie für die Replikation reservieren möchten, enthalten kann. Diese Informationen gelten für Gesamtstrukturen, die maximal 100.000 Benutzer enthalten und über eine Konnektivität von 28,8 kbit pro Sekunde (Kbit/s) oder höher verfügen. Empfehlungen, die für Gesamtstrukturen gelten, die mehr als 100.000 Benutzer oder Verbindungen mit weniger als 28,8 Kbit/s enthalten, finden Sie in einem erfahrenen Active Directory-Designer. Die Werte in der folgenden Tabelle basieren auf dem Replikations Datenverkehr, der in einer Umgebung mit den folgenden Merkmalen generiert wird:

- Neue Benutzer verknüpfen die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.
- Benutzer verlassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.
- Jeder Benutzer ist Mitglied von fünf globalen Gruppen und fünf universellen Gruppen.
- Das Verhältnis zwischen Benutzern und Computern ist 1:1.
- Active Directory integrierte Domain Name System (DNS) wird verwendet.
- DNS-Bereinigung verwendet.

> [!NOTE]
> Die in der folgenden Tabelle aufgeführten Abbildungen sind Näherungs Werte. Die Menge des Replikations Datenverkehrs hängt größtenteils von der Anzahl von Änderungen ab, die innerhalb eines bestimmten Zeitraums an dem Verzeichnis vorgenommen wurden. Vergewissern Sie sich, dass Ihr Netzwerk Ihren Replikations Datenverkehr unterstützen kann, indem Sie die geschätzte Menge und Geschwindigkeit der Änderungen in einem Lab testen, bevor Sie Ihre Domänen bereitstellen.

|Langsamster Link zum Verbinden eines Domänen Controllers (Kbit/s)|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 1 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 5 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 10 Prozent verfügbar ist|
| --- | --- | --- | --- |
|28.8|10.000|25.000|40.000|
|32|10.000|25.000|50.000|
|56|10.000|50.000|100.000|
|64|10.000|50.000|100.000|
|128|25.000|100.000|100.000|
|256|50.000|100.000|100.000|
|512|80.000|100.000|100.000|
|1\.500|100.000|100.000|100.000|

So verwenden Sie die folgende Tabelle:

1. Suchen Sie im **langsamsten Link verbinden einer Domänen Controller** Spalte den Wert, der der Geschwindigkeit des langsamsten Links entspricht, über den AD DS in Ihrer Domäne repliziert werden.

2. Suchen Sie in der Zeile, die der langsamsten Verbindungsgeschwindigkeit entspricht, die Spalte, die die Prozentsatz Bandbreite darstellt, die Sie AD DS zuordnen möchten. Der Wert an diesem Speicherort ist die maximale Anzahl von Benutzern, die die Domäne in einer einzelnen Domänen Gesamtstruktur enthalten kann.

Wenn Sie feststellen, dass die Gesamtzahl der Benutzer in Ihrer Gesamtstruktur kleiner ist als die maximale Anzahl von Benutzern, die Ihre Domäne enthalten kann, können Sie eine einzelne Domäne verwenden. Stellen Sie sicher, dass Sie bei dieser Bestimmung für ein geplantes zukünftiges Wachstum sorgen. Wenn Sie feststellen, dass die Gesamtzahl der Benutzer in Ihrer Gesamtstruktur größer ist als die maximale Anzahl der Benutzer, die Ihre Domäne enthalten kann, müssen Sie einen höheren Prozentsatz an Bandbreite für die Replikation reservieren, die Verbindungsgeschwindigkeit erhöhen oder Ihre Organisation in regionale Domänen aufteilen.

## <a name="dividing-the-organization-into-regional-domains"></a>Aufteilen der Organisation in regionale Domänen

Wenn Sie nicht alle Benutzer in einer einzelnen Domäne aufnehmen können, müssen Sie das regionale Domänen Modell auswählen. Unterteilen Sie Ihre Organisation in eine Weise, die für Ihre Organisation und Ihr vorhandenes Netzwerk sinnvoll ist. Beispielsweise können Sie Regionen auf der Grundlage von kontinentalen Grenzen erstellen.

Da Sie für jede Region, die Sie einrichten, eine Active Directory Domäne erstellen müssen, empfiehlt es sich, die Anzahl der Regionen zu minimieren, die Sie für AD DS definieren. Obwohl es möglich ist, eine unbegrenzte Anzahl von Domänen in eine Gesamtstruktur einzubinden, wird für die Verwaltbarkeit empfohlen, dass eine Gesamtstruktur nicht mehr als 10 Domänen umfasst. Sie müssen ein geeignetes Gleichgewicht zwischen der Optimierung der Replikations Bandbreite und der Minimierung der administrativen Komplexität erzielen, wenn Sie Ihre Organisation in regionale Domänen aufteilen.

Bestimmen Sie zunächst die maximale Anzahl von Benutzern, die von der Gesamtstruktur gehostet werden können. Verwenden Sie hierfür die langsamste Verknüpfung in der Gesamtstruktur, in der die Domänen Controller repliziert werden, und die durchschnittliche Bandbreiten Menge, die Sie Active Directory Replikation zuordnen möchten. In der folgenden Tabelle ist die maximale Anzahl von Benutzern, die in einer Gesamtstruktur enthalten sein können, aufgeführt. Dies basiert auf der Geschwindigkeit der langsamsten Verknüpfung und der prozentualen Bandbreite, die für die Replikation reserviert werden soll. Diese Informationen gelten für Gesamtstrukturen, die maximal 100.000 Benutzer enthalten und über eine Konnektivität von 28,8 Kbit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf den folgenden Annahmen:

- Alle Domänen Controller sind globale Katalogserver.
- Neue Benutzer verknüpfen die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.
- Benutzer verlassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.
- Benutzer sind Mitglieder von fünf globalen Gruppen und fünf universellen Gruppen.
- Das Verhältnis zwischen Benutzern und Computern ist 1:1.
- Active Directory integrierte DNS wird verwendet.
- DNS-Bereinigung verwendet.

> [!NOTE]
> Die in der folgenden Tabelle aufgeführten Abbildungen sind Näherungs Werte. Die Menge des Replikations Datenverkehrs hängt größtenteils von der Anzahl von Änderungen ab, die innerhalb eines bestimmten Zeitraums an dem Verzeichnis vorgenommen wurden. Vergewissern Sie sich, dass Ihr Netzwerk Ihren Replikations Datenverkehr unterstützen kann, indem Sie die geschätzte Menge und Geschwindigkeit der Änderungen in einem Lab testen, bevor Sie Ihre Domänen bereitstellen.

|Langsamster Link zum Verbinden eines Domänen Controllers (Kbit/s)|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 1 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 5 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 10 Prozent verfügbar ist|
| --- | --- | --- | --- |
|28.8|10.000|50.000|75.000|
|32|10.000|50.000|75.000|
|56|10.000|75.000|100.000|
|64|25.000|75.000|100.000|
|128|50.000|100.000|100.000|
|256|75.000|100.000|100.000|
|512|100.000|100.000|100.000|
|1\.500|100.000|100.000|100.000|

So verwenden Sie die folgende Tabelle:

1. Suchen Sie im **langsamsten Link verbinden einer Domänen Controller** Spalte den Wert, der der Geschwindigkeit des langsamsten Links entspricht, über den AD DS in Ihrer Gesamtstruktur repliziert werden.

2. Suchen Sie in der Zeile, die der langsamsten Verbindungsgeschwindigkeit entspricht, die Spalte, die die Prozentsatz Bandbreite darstellt, die Sie AD DS zuordnen möchten. Der Wert an diesem Speicherort ist die maximale Anzahl von Benutzern, die von der Gesamtstruktur gehostet werden können.

Wenn die maximale Anzahl von Benutzern, die in der Gesamtstruktur gehostet werden können, größer ist als die Anzahl der Benutzer, die Sie hosten müssen, funktioniert eine einzelne Gesamtstruktur für den Entwurf. Wenn Sie mehr Benutzer als die von Ihnen identifizierte maximale Anzahl hosten müssen, müssen Sie die minimale Verknüpfungs Geschwindigkeit erhöhen, einen höheren Prozentsatz an Bandbreite für AD DS zuweisen oder weitere Gesamtstrukturen bereitstellen.

Wenn Sie feststellen, dass die Anzahl der Benutzer, die Sie hosten müssen, von einer einzelnen Gesamtstruktur unterstützt wird, müssen Sie im nächsten Schritt die maximale Anzahl von Benutzern ermitteln, die die einzelnen Regionen basierend auf dem langsamsten Link in dieser Region unterstützen können. Teilen Sie Ihre Gesamtstruktur in Bereiche auf, die für Sie sinnvoll sind. Stellen Sie sicher, dass Sie Ihre Entscheidung auf etwas festlegen, das sich wahrscheinlich nicht ändert. Verwenden Sie z. b. Kontinente anstelle von Vertriebsregionen. Diese Bereiche sind die Grundlage für Ihre Domänen Struktur, wenn Sie die maximale Anzahl von Benutzern identifiziert haben.

Bestimmen Sie die Anzahl der Benutzer, die in jeder Region gehostet werden müssen, und überprüfen Sie dann, ob Sie basierend auf der langsamsten Verbindungsgeschwindigkeit und der Bandbreite, die AD DS in dieser Region zugeordnet ist, den zulässigen Höchstwert nicht überschreiten. In der folgenden Tabelle ist die maximale Anzahl von Benutzern, die in einer regionalen Domäne enthalten sein können, aufgeführt. Es basiert auf der Geschwindigkeit der langsamsten Verknüpfung und dem Prozentsatz der Bandbreite, die für die Replikation reserviert werden soll. Diese Informationen gelten für Gesamtstrukturen, die maximal 100.000 Benutzer enthalten und über eine Konnektivität von 28,8 Kbit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf den folgenden Annahmen:

- Alle Domänen Controller sind globale Katalogserver.
- Neue Benutzer verknüpfen die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.
- Benutzer verlassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.
- Benutzer sind Mitglieder von fünf globalen Gruppen und fünf universellen Gruppen.
- Das Verhältnis zwischen Benutzern und Computern ist 1:1.
- Active Directory integrierte DNS wird verwendet.
- DNS-Bereinigung verwendet.

> [!NOTE]
> Die in der folgenden Tabelle aufgeführten Abbildungen sind Näherungs Werte. Die Menge des Replikations Datenverkehrs hängt größtenteils von der Anzahl von Änderungen ab, die innerhalb eines bestimmten Zeitraums an dem Verzeichnis vorgenommen wurden. Vergewissern Sie sich, dass Ihr Netzwerk Ihren Replikations Datenverkehr unterstützen kann, indem Sie die geschätzte Menge und Geschwindigkeit der Änderungen in einem Lab testen, bevor Sie Ihre Domänen bereitstellen.

|Langsamster Link zum Verbinden eines Domänen Controllers (Kbit/s)|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 1 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 5 Prozent verfügbar ist|Maximale Anzahl von Benutzern, wenn eine Bandbreite von 10 Prozent verfügbar ist|
| --- | --- | --- | --- |
|28.8|10.000|18.000|40.000|
|32|10.000|20.000|50.000|
|56|10.000|40.000|100.000|
|64|10.000|50.000|100.000|
|128|15.000|100.000|100.000|
|256|30.000|100.000|100.000|
|512|80.000|100.000|100.000|
|1\.500|100.000|100.000|100.000|

So verwenden Sie die folgende Tabelle:

1. Suchen Sie im **langsamsten Link verbinden einer Domänen Controller** Spalte den Wert, der der Geschwindigkeit des langsamsten Links entspricht, über den AD DS in Ihrer Region repliziert werden.

2. Suchen Sie in der Zeile, die der langsamsten Verbindungsgeschwindigkeit entspricht, die Spalte, die die Prozentsatz Bandbreite darstellt, die Sie AD DS zuordnen möchten. Dieser Wert stellt die maximale Anzahl von Benutzern dar, die der Bereich hosten kann.

Evaluieren Sie jede vorgeschlagene Region, und stellen Sie fest, ob die maximale Anzahl der Benutzer in jeder Region kleiner ist als die empfohlene maximale Anzahl von Benutzern, die eine Domäne enthalten kann. Wenn Sie feststellen, dass die Region die Anzahl von Benutzern hosten kann, die Sie benötigen, können Sie eine Domäne für diese Region erstellen. Wenn Sie feststellen, dass Sie nicht viele Benutzer hosten können, sollten Sie den Entwurf in kleinere Regionen aufteilen und die maximale Anzahl von Benutzern neu berechnen, die in jeder Region gehostet werden können. Die anderen Alternativen sind das Zuweisen von mehr Bandbreite oder das Erhöhen der Verbindungsgeschwindigkeit.

Obwohl die Gesamtzahl der Benutzer, die Sie in einer Domäne in einer Gesamtstruktur mit mehreren Domänen platzieren können, kleiner ist als die Anzahl der Benutzer in der Domäne in einer einzelnen Domänen Gesamtstruktur, kann die Gesamtzahl der Benutzer in der Gesamtstruktur mit mehreren Domänen höher sein. Die kleinere Anzahl von Benutzern pro Domäne in einer Gesamtstruktur mit mehreren Domänen umfasst den zusätzlichen Replikations Aufwand, der durch die Verwaltung des globalen Katalogs in dieser Umgebung erstellt wurde. Empfehlungen, die für Gesamtstrukturen gelten, die mehr als 100.000 Benutzer oder Verbindungen mit weniger als 28,8 Kbit/s enthalten, finden Sie in einem erfahrenen Active Directory-Designer.

## <a name="documenting-the-regions-identified"></a>Dokumentieren der identifizierten Regionen

Nachdem Sie Ihre Organisation in regionale Domänen aufgeteilt haben, dokumentieren Sie die Regionen, die Sie darstellen möchten, sowie die Anzahl der Benutzer, die in jeder Region vorhanden sein werden. Beachten Sie außerdem die Geschwindigkeit der langsamsten Links in den einzelnen Regionen, die Sie für die Active Directory Replikation verwenden werden. Diese Informationen werden verwendet, um zu bestimmen, ob zusätzliche Domänen oder Gesamtstrukturen benötigt werden.

Für ein Arbeitsblatt, das Sie bei der Dokumentation der identifizierten Regionen unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus den [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) herunter, und öffnen Sie "Identifizierungs Regionen" (DSSLOGI_4.doc).
