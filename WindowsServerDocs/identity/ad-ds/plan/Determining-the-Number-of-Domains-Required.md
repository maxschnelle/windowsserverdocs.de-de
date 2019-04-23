---
ms.assetid: 87bca912-b912-4bbe-9533-2c34a7abc52d
title: Bestimmen der Anzahl der erforderlichen Domänen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e5d6369ca91c1d48375c22238d1e706576df7fbf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843521"
---
# <a name="determining-the-number-of-domains-required"></a>Bestimmen der Anzahl der erforderlichen Domänen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Jede Gesamtstruktur, die mit einer einzelnen Domäne wird gestartet. Die maximale Anzahl von Benutzern, die eine einzelnen Domänengesamtstruktur darf basiert auf den Link am langsamsten, die aufnehmen müssen die Replikation zwischen Domänencontrollern und die verfügbare Bandbreite, die auf Active Directory Domain Services (AD DS) zugeordnet werden soll. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine Domäne enthalten kann, die basierend auf einer einzelnen Domänengesamtstruktur, der die Geschwindigkeit des langsamsten links und den Prozentsatz der Bandbreite, die Sie reservieren, für die Replikation möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten, und, die über eine Konnektivität von 28,8 Kilobit pro Sekunde (Kbit/s) oder höher verfügen. Empfehlungen für Gesamtstrukturen, die mehr als 100.000 Benutzern oder Verbindungen von weniger als bei 28,8 Kbit/s enthalten, erhalten Sie einen erfahrenen Designer für die Active Directory. Die Werte in der folgenden Tabelle basieren auf den Replikationsdatenverkehr generiert in einer Umgebung mit den folgenden Eigenschaften:  
  
- Neue Benutzer treten die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.  
- Benutzer lassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.  
- Jeder Benutzer ist Mitglied der fünf globale Gruppen und fünf universelle Gruppen.  
- Das Verhältnis von Benutzern zu Computern ist es sich um 1:1.  
- Active Directory-integrierte System DNS (Domain Name) wird verwendet.  
- DNS-Aufräumvorgänge wird verwendet.  

> [!NOTE]  
> Die Abbildungen in der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge von Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen, die in das Verzeichnis in einem bestimmten Zeitraum. Vergewissern Sie sich, dass Ihr Netzwerk Ihre Replikationsdatenverkehr aufnehmen kann, durch die geschätzte Menge und die Rate der Änderungen auf Ihr Design in einer testumgebung vor der Bereitstellung Ihrer Domänen testen.  
  
|Langsamste Verbindung mit einem Domänencontroller (Kbit/s)|Maximale Anzahl von Benutzern, wenn 1 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 5 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 10 Prozent Bandbreite verfügbar ist|  
| --- | --- | --- | --- |  
|28.8|10,000|25,000|40,000|  
|32|10,000|25,000|50,000|  
|56|10,000|50,000|100,000|  
|64|10,000|50,000|100,000|  
|128|25,000|100,000|100,000|  
|256|50,000|100,000|100,000|  
|512|80,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  

So verwenden Sie diese Tabelle:  

1. In der **langsamste einen Domänencontroller für die Verknüpfung** Spalte suchen Sie den Wert, der die Geschwindigkeit des langsamsten links entspricht, über die AD DS in Ihrer Domäne repliziert werden.  

2. Suchen Sie in der Zeile, die Ihre langsamste verbindungsgeschwindigkeit entspricht, die die Spalte, die von Bandbreite Prozentsatz darstellt, die in AD DS zugeordnet werden soll. Der Wert an dieser Stelle ist die maximale Anzahl von Benutzern, die die Domäne in einer einzelnen Domänengesamtstruktur enthalten kann.  

Wenn Sie feststellen, dass die Gesamtzahl der Benutzer in Ihrer Gesamtstruktur ist kleiner als die maximale Anzahl von Benutzern, die die Domäne enthalten kann, können Sie eine einzelne Domäne. Achten Sie darauf, dass Sie für geplante zukünftiges Wachstum zu ermöglichen, wenn Sie diese Entscheidung zu treffen. Wenn Sie feststellen, dass die Gesamtzahl der Benutzer in Ihrer Gesamtstruktur größer als die maximale Anzahl von Benutzern, die die Domäne enthalten kann, benötigen Sie, reservieren einen höheren Prozentsatz der Bandbreite für die Replikation Ihrer verbindungsgeschwindigkeit zu erhöhen, oder Teilen Ihrer Organisation in Regionaldomänen.  
  
## <a name="dividing-the-organization-into-regional-domains"></a>Unterteilen die Organisation in Regionaldomänen

Wenn Sie alle Benutzer in einer einzelnen Domäne aufnehmen können, müssen Sie die regionales Domänenmodell auswählen. Teilen Sie Ihre Organisation in Regionen in einer Weise, die für Ihre Organisation und Ihr vorhandenes Netzwerk sinnvoll ist. Sie können z. B. Bereiche auf Grundlage der kontinentalen Grenzen erstellen.  
  
Beachten Sie, da Sie Active Directory-Domäne für jede Region zu erstellen, die Sie einrichten müssen, es wird empfohlen, dass Sie die Anzahl der Bereiche minimieren, die Sie für AD DS zu definieren. Obwohl es möglich, eine unbegrenzte Anzahl von Domänen in einer Gesamtstruktur enthalten ist, sollten zu Zwecken der Verwaltbarkeit eine Gesamtstruktur nicht mehr als 10 Domänen enthalten. Sie müssen das angemessene Verhältnis zwischen Ihrer Bandbreite optimieren und Ihre Verwaltung zu komplizieren minimieren, wenn Ihre Organisation in Regionaldomänen Division einrichten.  
  
Bestimmen Sie zunächst die maximale Anzahl von Benutzern, die von die Gesamtstruktur gehostet werden kann. Als Grundlage für diese den langsamsten Link in der Gesamtstruktur für die Domänencontroller repliziert werden sollen und die durchschnittliche Menge an Bandbreite, die Sie Active Directory-Replikation zuweisen möchten. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine Gesamtstruktur enthalten kann. Dies hängt von der Geschwindigkeit des langsamsten Links sowie den Prozentsatz Bandbreite, die Sie für die Replikation reservieren möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten, und, die über eine Konnektivität von 28,8 Kbit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf folgenden Annahmen:  

- Alle Domänencontroller sind globale Katalogserver zu erhalten.  
- Neue Benutzer treten die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.  
- Benutzer lassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.  
- Benutzer sind Mitglieder der fünf globale Gruppen und fünf universelle Gruppen.  
- Das Verhältnis von Benutzern zu Computern ist es sich um 1:1.  
- Active Directory-integrierte DNS wird verwendet.  
- DNS-Aufräumvorgänge wird verwendet.  

> [!NOTE]  
> Die Abbildungen in der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge von Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen, die in das Verzeichnis in einem bestimmten Zeitraum. Vergewissern Sie sich, dass Ihr Netzwerk Ihre Replikationsdatenverkehr aufnehmen kann, durch die geschätzte Menge und die Rate der Änderungen auf Ihr Design in einer testumgebung vor der Bereitstellung Ihrer Domänen testen.  
  
|Langsamste Verbindung mit einem Domänencontroller (Kbit/s)|Maximale Anzahl von Benutzern, wenn 1 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 5 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 10 Prozent Bandbreite verfügbar ist|  
| --- | --- | --- | --- |  
|28.8|10,000|50,000|75,000|  
|32|10,000|50,000|75,000|  
|56|10,000|75,000|100,000|  
|64|25,000|75,000|100,000|  
|128|50,000|100,000|100,000|  
|256|75,000|100,000|100,000|  
|512|100,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  

So verwenden Sie diese Tabelle:  

1. In der **langsamste einen Domänencontroller für die Verknüpfung** Spalte suchen Sie den Wert, der die Geschwindigkeit des langsamsten links entspricht, über die AD DS in Ihrer Gesamtstruktur repliziert wird.  

2. Suchen Sie in der Zeile, die Ihre langsamste verbindungsgeschwindigkeit entspricht, die die Spalte, die von Bandbreite Prozentsatz darstellt, die in AD DS zugeordnet werden soll. Der Wert an dieser Stelle ist die maximale Anzahl von Benutzern, die von die Gesamtstruktur gehostet werden kann.  

Ist die maximale Anzahl von Benutzern, die die Gesamtstruktur hosten kann größer als die Anzahl der Benutzer, die Sie zum Hosten benötigen, funktioniert eine einzelne Gesamtstruktur, für den Entwurf. Wenn Sie mehr Benutzer als die maximale Anzahl zu hosten, die Sie angegeben haben müssen, zum Erhöhen Sie die minimale Übertragungsrate, ordnen einen höheren Prozentsatz der Bandbreite für AD DS, oder weitere Gesamtstrukturen bereitstellen.  

Wenn Sie feststellen, dass eine einzelne Gesamtstruktur die Anzahl von Benutzern ermöglichen, die Sie zum Hosten benötigen, besteht der nächste Schritt, um zu bestimmen, dass die maximale Anzahl von Benutzern, die einzelnen Regionen unterstützen, kann auf den langsamsten-Link in dieser Region basieren. Teilen Sie der Gesamtstruktur, in Regionen, die für Sie sinnvoll. Stellen Sie sicher, dass Sie Ihre Entscheidung auf ein beliebiges Objekt basieren, die nicht geändert wird. Verwenden Sie z. B. Kontinenten anstelle Verkaufsregionen ein. Diese Regionen werden die Grundlage für Ihre Domänenstruktur, wenn Sie die maximale Anzahl von Benutzern identifiziert haben.  

Bestimmen Sie die Anzahl von Benutzern, die in jeder Region gehostet werden, und stellen Sie sicher, dass sie nicht die maximal zulässige Anzahl überschritten werden, auf der Grundlage der langsamste verbindungsgeschwindigkeit und die Bandbreite, die in AD DS in dieser Region zugeordnet. Die folgende Tabelle enthält die maximal empfohlene Anzahl von Benutzern, die eine regionale Domäne enthalten kann. Es hängt von der Geschwindigkeit des langsamsten links und den Prozentsatz der Bandbreite, die Sie für die Replikation reservieren möchten. Diese Informationen gelten für Gesamtstrukturen, die bis zu 100.000 Benutzer enthalten, und, die über eine Konnektivität von 28,8 Kbit/s oder höher verfügen. Die Werte in der folgenden Tabelle basieren auf folgenden Annahmen:  

- Alle Domänencontroller sind globale Katalogserver zu erhalten.  
- Neue Benutzer treten die Gesamtstruktur mit einer Rate von 20 Prozent pro Jahr.  
- Benutzer lassen die Gesamtstruktur mit einer Rate von 15 Prozent pro Jahr.  
- Benutzer sind Mitglieder der fünf globale Gruppen und fünf universelle Gruppen.  
- Das Verhältnis von Benutzern zu Computern ist es sich um 1:1.  
- Active Directory-integrierte DNS wird verwendet.  
- DNS-Aufräumvorgänge wird verwendet.  
  
> [!NOTE]  
> Die Abbildungen in der folgenden Tabelle aufgeführt sind Näherungswerte. Die Menge von Replikationsdatenverkehr hängt weitgehend von der Anzahl von Änderungen, die in das Verzeichnis in einem bestimmten Zeitraum. Vergewissern Sie sich, dass Ihr Netzwerk Ihre Replikationsdatenverkehr aufnehmen kann, durch die geschätzte Menge und die Rate der Änderungen auf Ihr Design in einer testumgebung vor der Bereitstellung Ihrer Domänen testen.  
  
|Langsamste Verbindung mit einem Domänencontroller (Kbit/s)|Maximale Anzahl von Benutzern, wenn 1 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 5 Prozent Bandbreite verfügbar ist|Maximale Anzahl von Benutzern, wenn 10 Prozent Bandbreite verfügbar ist|  
| --- | --- | --- | --- |  
|28.8|10,000|18,000|40,000|  
|32|10,000|20,000|50,000|  
|56|10,000|40,000|100,000|  
|64|10,000|50,000|100,000|  
|128|15,000|100,000|100,000|  
|256|30,000|100,000|100,000|  
|512|80,000|100,000|100,000|  
|1,500|100,000|100,000|100,000|  

So verwenden Sie diese Tabelle:  

1. In der **langsamste einen Domänencontroller für die Verknüpfung** Spalte suchen Sie den Wert, der die Geschwindigkeit des langsamsten links entspricht, über die AD DS in Ihrer Region repliziert wird.  

2. Suchen Sie in der Zeile, die Ihre langsamste verbindungsgeschwindigkeit entspricht, die die Spalte, die von Bandbreite Prozentsatz darstellt, die in AD DS zugeordnet werden soll. Dieser Wert stellt dar, die maximale Anzahl von Benutzern, die die Region gehostet werden kann.  

Bewerten Sie jede vorgeschlagenen Region aus, und ermitteln Sie, ob die maximale Anzahl von Benutzern in jeder Region ist kleiner als die empfohlene maximale Anzahl von Benutzern, die eine Domäne enthalten kann. Wenn Sie feststellen, dass die Region die Anzahl der Benutzer gehostet werden kann, die Sie benötigen, können Sie eine Domäne für diese Region erstellen. Wenn Sie feststellen, dass, die Sie hosten, können nicht viele Benutzer sollten Sie Ihren Entwurf in kleinere Bereiche unterteilen und Neuberechnen die maximale Anzahl von Benutzern, die in jeder Region gehostet werden können. Die andere Alternativen sind zum Reservieren von mehr Bandbreite oder zum Erhöhen Ihrer verbindungsgeschwindigkeit.  

Obwohl die Gesamtzahl der Benutzer, die Sie in einer Domäne in einer Gesamtstruktur mit mehreren Domänen aufnehmen können kleiner als die Anzahl von Benutzern in der Domäne in einer Gesamtstruktur mit einer Domäne ist, kann die Anzahl der Benutzer in der Gesamtstruktur mit mehreren Domänen höher sein. Die kleinere Zahl von Benutzern pro Domäne in einer Gesamtstruktur mit mehreren Domänen gilt für die zusätzliche Replikation Mehraufwands, der durch den globalen Katalog in dieser Umgebung zu verwalten. Empfehlungen für Gesamtstrukturen, die mehr als 100.000 Benutzern oder Verbindungen von weniger als bei 28,8 Kbit/s enthalten, erhalten Sie einen erfahrenen Designer für die Active Directory.  
  
## <a name="documenting-the-regions-identified"></a>Dokumentieren die Regionen identifiziert

Nach dem Dividieren Sie Ihrer Organisation in Regionaldomänen, Dokument, das die gewünschten Regionen dargestellt und die Anzahl der Benutzer, die in jeder Region vorhanden sind. Beachten Sie auch die Geschwindigkeit des langsamsten Links in jeder Region, die Sie für die Active Directory-Replikation verwenden. Diese Informationen werden verwendet, um festzustellen, ob zusätzliche Domänen oder Gesamtstrukturen erforderlich sind.  

Bei einem Arbeitsblatt zur Unterstützung beim Dokumentieren der Regions, die Sie angegeben haben, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) , und öffnen Sie " Identifizieren die Regionen"(DSSLOGI_4.doc).  
