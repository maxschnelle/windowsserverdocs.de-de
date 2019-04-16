---
ms.assetid: 87bca912-b912-4bbe-9533-2c34a7abc52d
title: "Bestimmen der Anzahl der erforderlichen Domänen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b65c792929a29c959244d1da83b4882f15fa2935
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="determining-the-number-of-domains-required"></a>Bestimmen der Anzahl der erforderlichen Domänen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Jede Gesamtstruktur beginnt mit einer einzelnen Domäne. Die maximale Anzahl von Benutzern, die eine Gesamtstruktur mit einer Domäne enthalten kann basiert auf den Link, der langsamste, die aufnehmen muss die Replikation zwischen Domänencontrollern und die verfügbare Bandbreite, die auf Active Directory-Domänendienste (AD DS) zugeordnet werden soll. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine Domäne enthalten kann, basierend auf einer Gesamtstruktur mit einer Domäne, die Geschwindigkeit der langsamste Verbindung, und der Prozentsatz an Bandbreite, die Sie für die Replikation reservieren möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten, und, die über eine Verbindung von 28,8 Kbit pro Sekunde (KBit/s) oder höher verfügen. Empfehlungen, die zu Gesamtstrukturen gelten, die mehr als 100.000 Benutzer oder der Konnektivität von weniger als 28,8 KBit/s enthalten, wenden Sie sich an einen erfahrenen Active Directory-Designer. Die Werte in der folgenden Tabelle basieren auf die Replikationsaktivitäten generiert, in einer Umgebung mit den folgenden Eigenschaften:  
  
-   Neue Benutzer treten der Gesamtstruktur mit einer Rate von 20Prozent pro Jahr.  
  
-   Benutzer verlassen der Gesamtstruktur mit einer Rate von 15Prozent pro Jahr.  
  
-   Jeder Benutzer ist ein Mitglied von fünf globalen Gruppen und fünf universellen Gruppen.  
  
-   Das Verhältnis von Benutzern zu Computern ist 1:1.  
  
-   Active Directory-integrierte DNS Domain Name System () wird verwendet.  
  
-   DNS-Aufräumvorgänge werden verwendet.  
  
> [!NOTE]  
> Die Abbildungenin der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge der Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen in das Verzeichnis in einem bestimmten Zeitraum ab. Vergewissern Sie sich, dass Ihr Netzwerk der Replikationsdatenverkehr aufnehmen kann, testen Sie die geschätzte Menge und die Rate der Änderungen auf Ihrem Entwurf in einem Labor vor der Bereitstellung Ihrer Domänen.  
  
|Langsamste Verbindung mit einem Domänencontroller (KBit/s)|Maximale Anzahl von Benutzern bei 1Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 5Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 10Prozent Bandbreite verfügbar ist|  
|--------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------|-----------------------------------------------------------------|  
|28.8|10,000|25,000|40,000|  
|32|10,000|25,000|50,000|  
|56|10,000|50,000|100,000|  
|64|10,000|50,000|100,000|  
|128|25,000|100,000|100,000|  
|256|50,000|100,000|100,000|  
|512|80,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  
  
In dieser Tabelle zu verwenden:  
  
1.  In der **langsamste verknüpfen, verbinden einen Domänencontroller** Spalte, suchen Sie den Wert, der die Geschwindigkeit der langsamste Verbindung entspricht, über die AD DS werden in der Domäne repliziert.  
  
2.  Suchen Sie in der Zeile, die der langsamste verbindungsgeschwindigkeit entspricht in der Spalte, die die Bandbreite Prozentsatz darstellt, die in AD DS zugeordnet werden soll. Der Wert an dieser Stelle ist die maximale Anzahl von Benutzern, die die Domäne in einer Gesamtstruktur mit einer Domäne enthalten kann.  
  
Wenn Sie feststellen, dass die Gesamtanzahl der Benutzer in der Gesamtstruktur ist kleiner als die maximale Anzahl von Benutzern, die Ihre Domäne enthalten kann, können Sie eine einzelne Domäne. Achten Sie darauf, dass für geplante zukünftiges Wachstum zu berücksichtigen, wenn Sie dies vornehmen. Wenn Sie feststellen, dass die Gesamtanzahl der Benutzer in der Gesamtstruktur größer als die maximale Anzahl von Benutzern, die Ihre Domäne enthalten kann, müssen Sie einen höheren Prozentsatz an Bandbreite für die Replikation zu reservieren Erhöhen der Geschwindigkeit der Verknüpfung oder Teilen Ihrer Organisation Regionaldomänen.  
  
## <a name="dividing-the-organization-into-regional-domains"></a>Aufteilen der Organisation in Regionaldomänen  
Wenn Sie alle Benutzer in einer einzelnen Domäne aufnehmen können, müssen Sie die regionales Domänenmodell auswählen. Teilen Sie Ihre Organisation in Regionen in einer Weise, die für Ihre Organisation und Ihr vorhandenes Netzwerk sinnvoll ist. Beispielsweise können Sie basierte auf den continental Grenzen Regionen erstellen.  
  
Beachten Sie, dass, da Sie Active Directory-Domäne für jede Region erstellen, die Sie einrichten müssen, empfiehlt es sich, dass Sie die Anzahl der Bereiche minimieren, die Sie für AD DS zu definieren. Obwohl es möglich, eine unbegrenzte Anzahl von Domänen in einer Gesamtstruktur enthalten ist, sollten für die Verwaltung eine Gesamtstruktur nicht mehr als 10 Domänen enthalten. Sie müssen die ausgewogenes Verhältnis zwischen der Optimierung der Bandbreite für die Replikation und minimieren die Verwaltungskomplexität beim Ihrer Organisation Regionaldomänen Dividieren einrichten.  
  
Ermitteln Sie zunächst die maximale Anzahl von Benutzern, die die Gesamtstruktur hosten können. Orientieren Sie sich dies an den langsamsten Link in der Gesamtstruktur in der, die Domäne Domänencontroller repliziert werden, und die durchschnittliche Menge an Bandbreite, die Sie für Active Directory-Replikation zuweisen möchten. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine Gesamtstruktur enthalten kann. Dies basiert auf der Geschwindigkeit der langsamste Link und der Prozentsatz-Bandbreite, die Sie für die Replikation reservieren möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten und über eine Konnektivität 28,8 KBit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf folgenden Annahmen:  
  
-   Alle Domänencontroller sind globale Katalogserver.  
  
-   Neue Benutzer treten der Gesamtstruktur mit einer Rate von 20Prozent pro Jahr.  
  
-   Benutzer verlassen der Gesamtstruktur mit einer Rate von 15Prozent pro Jahr.  
  
-   Benutzer sind Mitglieder von fünf globalen Gruppen und fünf universellen Gruppen.  
  
-   Das Verhältnis von Benutzern zu Computern ist 1:1.  
  
-   Active Directory-integrierte DNS wird verwendet.  
  
-   DNS-Aufräumvorgänge werden verwendet.  
  
> [!NOTE]  
> Die Abbildungenin der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge der Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen in das Verzeichnis in einem bestimmten Zeitraum ab. Vergewissern Sie sich, dass Ihr Netzwerk der Replikationsdatenverkehr aufnehmen kann, testen Sie die geschätzte Menge und die Rate der Änderungen auf Ihrem Entwurf in einem Labor vor der Bereitstellung Ihrer Domänen.  
  
|Langsamste Verbindung mit einem Domänencontroller (KBit/s)|Maximale Anzahl von Benutzern bei 1Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 5Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 10Prozent Bandbreite verfügbar ist|  
|--------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------|-----------------------------------------------------------------|  
|28.8|10,000|50,000|75,000|  
|32|10,000|50,000|75,000|  
|56|10,000|75,000|100,000|  
|64|25,000|75,000|100,000|  
|128|50,000|100,000|100,000|  
|256|75,000|100,000|100,000|  
|512|100,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  
  
In dieser Tabelle zu verwenden:  
  
1.  In der **langsamste verknüpfen, verbinden einen Domänencontroller** Spalte, suchen Sie den Wert, der die Geschwindigkeit der langsamste Verbindung entspricht, über die AD DS werden in der Gesamtstruktur repliziert.  
  
2.  Suchen Sie in der Zeile, die der langsamste verbindungsgeschwindigkeit entspricht, die Spalte, die in Prozent Bandbreite darstellt, die in AD DS zugeordnet werden soll. Der Wert an dieser Stelle ist die maximale Anzahl von Benutzern, die die Gesamtstruktur hosten können.  
  
Ist die maximale Anzahl von Benutzern, die die Gesamtstruktur hosten können größer als die Anzahl der Benutzer, die Sie hosten möchten, funktionieren für den Entwurf eine einzelne Gesamtstruktur. Sie ggf. mehr Benutzer als die maximale Anzahl zu hosten, die Sie identifiziert benötigen Sie, erhöhen Sie die minimale Übertragungsrate, reservieren einen höheren Prozentsatz der Bandbreite für AD DS, oder Bereitstellen zusätzliche Gesamtstrukturen.  
  
Wenn Sie feststellen, dass eine einzelne Gesamtstruktur die Anzahl der Benutzer berücksichtigen, die Sie zum Hosten benötigen, besteht der nächste Schrittbestimmen, ob die maximale Anzahl von Benutzern, die jede Region unterstützen kann je nach den langsamsten Link in dieser Region. Teilen Sie der Gesamtstruktur in Regionen, die Ihnen sinnvoll. Stellen Sie sicher, dass Sie bei der Entscheidung über etwas basieren, die nicht geändert wird. Verwenden Sie z.B. Kontinenten anstelle sales Regionen. Diese Bereiche werden die Grundlage für Ihre Domänenstruktur, wenn Sie die maximale Anzahl von Benutzern identifiziert haben.  
  
Bestimmen Sie die Anzahl der Benutzer, die in jeder Region gehostet werden, und stellen Sie sicher, dass nicht die maximal zulässige Anzahl übersteigt müssen auf der Grundlage der langsamste verbindungsgeschwindigkeit und die Bandbreite, die in AD DS in diesem Bereich zugeordnet. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine regionale Domäne enthalten kann. Basiert auf der Geschwindigkeit der langsamste Verbindung und der Prozentsatz der Bandbreite, die Sie für die Replikation reservieren möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten und über eine Konnektivität 28,8 KBit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf folgenden Annahmen:  
  
-   Alle Domänencontroller sind globale Katalogserver.  
  
-   Neue Benutzer treten der Gesamtstruktur mit einer Rate von 20Prozent pro Jahr.  
  
-   Benutzer verlassen der Gesamtstruktur mit einer Rate von 15Prozent pro Jahr.  
  
-   Benutzer sind Mitglieder von fünf globalen Gruppen und fünf universellen Gruppen.  
  
-   Das Verhältnis von Benutzern zu Computern ist 1:1.  
  
-   Active Directory-integrierte DNS wird verwendet.  
  
-   DNS-Aufräumvorgänge werden verwendet.  
  
> [!NOTE]  
> Die Abbildungenin der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge der Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen in das Verzeichnis in einem bestimmten Zeitraum ab. Vergewissern Sie sich, dass Ihr Netzwerk der Replikationsdatenverkehr aufnehmen kann, testen Sie die geschätzte Menge und die Rate der Änderungen auf Ihrem Entwurf in einem Labor vor der Bereitstellung Ihrer Domänen.  
  
|Langsamste Verbindung mit einem Domänencontroller (KBit/s)|Maximale Anzahl von Benutzern bei 1Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 5Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern bei 10Prozent Bandbreite verfügbar ist|  
|--------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------|-----------------------------------------------------------------|  
|28.8|10,000|18,000|40,000|  
|32|10,000|20,000|50,000|  
|56|10,000|40,000|100,000|  
|64|10,000|50,000|100,000|  
|128|15,000|100,000|100,000|  
|256|30,000|100,000|100,000|  
|512|80,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  
  
In dieser Tabelle zu verwenden:  
  
1.  In der **langsamste verknüpfen, verbinden einen Domänencontroller** Spalte, suchen Sie den Wert, der die Geschwindigkeit der langsamste Verbindung entspricht, über die repliziert AD DS in Ihrer Region.  
  
2.  Suchen Sie in der Zeile, die der langsamste verbindungsgeschwindigkeit entspricht, die Spalte, die in Prozent Bandbreite darstellt, die in AD DS zugeordnet werden soll. Dieser Wert legt die maximale Anzahl von Benutzern, die der Bereich hosten können.  
  
Bewerten Sie jede vorgeschlagenen Region, und ermitteln Sie, ob die maximale Anzahl von Benutzern in jeder Region ist kleiner als die empfohlene maximale Anzahl von Benutzern, die eine Domäne enthalten kann. Wenn Sie feststellen, dass die Region die Anzahl der Benutzer gehostet werden kann, die Sie benötigen, können Sie eine Domäne für diese Region erstellen. Wenn Sie feststellen, dass Sie hosten können nicht viele Benutzer, sollten Sie Ihr Design in kleinere Bereiche unterteilen und neu berechnet die maximale Anzahl von Benutzern, die in jeder Region gehostet werden können. Die alternativen sind mehr Bandbreite zuweisen, oder erhöhen die Geschwindigkeit der Verknüpfung.  
  
Obwohl die Gesamtanzahl der Benutzer, die in einer Domäne in einer Gesamtstruktur mit mehreren Domänen enthalten sein können kleiner als die Anzahl der Benutzer in der Domäne in einer Gesamtstruktur mit einer Domäne ist, kann die Anzahl der Benutzer in der Gesamtstruktur mit mehreren Domänen höher sein. Die kleinere Anzahl von Benutzern pro Domäne in einer Gesamtstruktur mit mehreren Domänen enthalten sind, die zusätzliche Replikation Mehraufwands durch den globalen Katalog in der Umgebung verwalten. Empfehlungen, die zu Gesamtstrukturen gelten, die mehr als 100.000 Benutzer oder der Konnektivität von weniger als 28,8 KBit/s enthalten, wenden Sie sich an einen erfahrenen Active Directory-Designer.  
  
## <a name="documenting-the-regions-identified"></a>Dokumentieren die Regionen identifiziert  
Nachdem Sie Ihrer Organisation in Regionaldomänen, Dokument, das die Bereiche, die gewünschte dargestellt und die Anzahl der Benutzer, die in jeder Region vorhanden ist teilen. Beachten Sie außerdem die Geschwindigkeit der langsamste Links in jeder Region, die Sie für die Active Directory-Replikation verwenden. Diese Informationen werden verwendet, um festzustellen, ob zusätzliche Domänen oder Gesamtstrukturen erforderlich sind.  
  
Für ein Arbeitsblatt, hilft Ihnen bei der dokumentieren die Bereiche, die Sie festgelegt haben, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip).  
  


