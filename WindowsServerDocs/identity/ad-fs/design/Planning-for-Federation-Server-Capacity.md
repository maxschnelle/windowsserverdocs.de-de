---
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: Planen der Verbundserverkapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 569bea74fe7750eaf2b410a552876e0862b1e24b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191093"
---
# <a name="planning-for-federation-server-capacity"></a>Planen der Verbundserverkapazität

Planen der Kapazität für Verbundserver können Sie besser einschätzen:  
  
-   Welche Faktoren wachsen die Größe der AD FS-Konfigurationsdatenbank.  
  
-   Die entsprechenden hardwareanforderungen für jeden Verbundserver.  
  
-   Die Anzahl der Verbundserver in jeder Organisation platziert werden soll.  
  
Verbundserver Ausgeben von Sicherheitstoken für Benutzer. Diese Token werden an einen Identitätsempfänger für die Nutzung angezeigt. Verbundserver ausstellen Sicherheitstoken, nach der Authentifizierung eines Benutzers oder nach dem Empfang von einem Sicherheitstoken, das zuvor von einem Partner Verbunddienst ausgegeben wurde. Ein Sicherheitstoken wird von einem Verbunddienst angefordert, wenn Benutzer zunächst auf verbundanwendungen anmelden oder ihre Sicherheitstoken abläuft, während sie auf verbundanwendungen zugreifen.  
  
Verbundserver hohe aufnehmen sollen\-farmkonfigurationen Verfügbarkeit-Server an, die Microsoft-Netzwerklastenausgleich verwenden \(NLB\) Technologie. Verbundserver in einer Farmkonfiguration können Anforderungen unabhängig voneinander und bedienen, ohne den Zugriff auf alle allgemeinen Farmkomponenten für jede Anforderung. Aus diesem Grund ist nur wenig Aufwand beteiligt Horizontales Skalieren eine Verbund-serverbereitstellung.  
  
**Empfehlungen:**  
  
-   Für unternehmenskritische\-kritisch oder hohe\-Verfügbarkeit Bereitstellungen, es wird empfohlen, eine kleine Verbundserverfarm zu, in jeder Partnerorganisation, mit mindestens zwei Verbundserver pro Farm vorhanden sind erstellen, um Fehlertoleranz bereitzustellen.  
  
-   Für hohe Verfügbarkeit und die Einfachheit der Verbundserver Horizontales Skalieren müssen ist horizontales hochskalieren die empfohlene Methode zum Umgang mit hohen Anzahl von Anforderungen pro Sekunde für einen bestimmten Verbunddienst aus. Skalieren über die grundlegende Konfiguration in dieser Anleitung ist es unwahrscheinlich, dass erhebliche Kapazität, die Behandlung der Gewinne erzeugen.  
  
## <a name="ad-fs-configuration-database-size-and-growth"></a>AD FS-Konfiguration-Datenbankgröße und-Wachstum  
Die Größe der AD FS-Konfigurationsdatenbank gilt im Allgemeinen klein sein, und Größe der Datenbank ist nicht tendenziell eine wichtige Überlegung für AD FS-Bereitstellungen.  Die genaue Größe der AD FS-Konfigurationsdatenbank kann hängen größtenteils davon die Anzahl von Vertrauensstellungen und die zugehörigen Vertrauensstellung\-bezogenen Metadaten – z. B. Ansprüche, die Anspruchsregeln und Überwachen von Einstellungen, die für jede Vertrauensstellung konfiguriert. Wenn die Anzahl der Trust-Einträge in der Konfigurationsdatenbank zunimmt, steigt auch die Notwendigkeit von mehr Speicherplatz.  
  
Weitere Informationen zur Bereitstellung über die AD FS-Konfigurationsdatenbank finden Sie unter [Überlegungen zur Topologie der AD FS-Bereitstellung](AD-FS-Deployment-Topology-Considerations.md).  
  
## <a name="memory-cpu-and-disk-space-requirements"></a>Anforderungen an den Arbeitsspeicher, CPU und Datenträger  
Zum Glück, Arbeitsspeicher, CPU und Speicherplatz für Verbundserver sind geringfügige, und sie sind nicht wahrscheinlich eine treibende Faktor Hardware Entscheidungen. Weitere Informationen zu den hardwareanforderungen finden Sie unter [Anhang A: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md).  
  
> [!NOTE]  
> Neigten Tests, die vom AD FS-Produktteam mit einer Verbundserverfarm konfiguriert mit einem dedizierten SQL Server zum Speichern der AD FS-Konfigurationsdatenbank ausgeführt wurden, die Gesamtlast auf dem SQL Server niedrig ist. In einem test mit einer vier\-Verbund\--Serverfarm, die Verwendung einer einzelnen SQL Server, CPU-Auslastung konfiguriert wurde nicht überstiegen 10 % trotz Tests, die von den Verbundservern zu zielauslastung wiederhergestellt.  
  
## <a name="bk_estimatefs"></a>Schätzen Sie die Anzahl der Verbundserver für Ihre Organisation  
Das AD FS-Produktteam entwickelt gerne den Planungsprozess für Verbundserver Hardware zu optimieren der AD FS-Kapazität dem Arbeitsblatt zur Dimensionierung. Diese Excel-Tabelle enthält die Rechner\-wie Funktionen, mit denen erwartete Nutzung von Daten, die gelangen Sie über die Benutzer in Ihrer Organisation bereitstellen und eine empfohlene optimale Anzahl der Verbundserver für Ihre AD FS-produktionsumgebung zurückgeben .  
  
> [!NOTE]  
> Die Anzahl der Verbundserver, die in dieser Tabelle wird empfohlen, wird basiert auf den Hardware- und Netzwerk-Spezifikationen, die das AD FS-Produktteam während der Tests verwendet. Aus diesem Grund muss die Anzahl der Verbundserver, die die Tabelle wird empfohlen, wird in diesem Kontext verstanden werden.  Weitere Informationen zu den Spezifikationen, die während der Tests verwendet, finden Sie unter dem Thema [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md).  
  
### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>Verwenden die AD FS-Kapazitätsplanung  
Wenn Sie diese Tabelle verwenden, müssen Sie einen Wert aus \(entweder **40 %** , **60 %** , oder **80 %** \) am besten den Prozentsatz der dar Gesamtanzahl der Benutzer, die Sie erwarten, dass authentifizierungsanforderungen auf Ihren Verbundserver während Spitzenzeiten gesendet wird.  
  
Anschließend müssen Sie einen Wert aus \(entweder **1 Minute**, **15 Minuten**, oder **1 Stunde** \) , dass am besten die Zeitspanne darstellt, erwarten Sie, dass, Der maximale Nutzung Zeitraum bis zum letzten. Sie können z. B. 40 % als Wert für die Gesamtzahl der Benutzer schätzen, werden, die die Anmeldung innerhalb eines Zeitraums von 15 Minuten oder 60 % der Benutzer wird innerhalb eines Zeitraums von einer Stunde anmelden. Zusammen definieren diese Werte die maximale Lastprofil, die mit dem Ihre Empfehlung Größe berechnet werden sollen.  
  
Als Nächstes müssen Sie die Gesamtzahl der Benutzer angeben, die einmalige Anmelden müssen\-für den Zugriff auf die Ziel-Ansprüche\-Anwendung unterstützt, basierend auf der gibt an, ob die Benutzer sind:  
  
-   Protokollierung in Active Directory von einem lokalen Computer, die physisch mit dem Unternehmensnetzwerk verbunden ist \(über die integrierte Windows-Authentifizierung\)  
  
-   Protokollierung in Active Directory Remote auf einem Computer, die nicht physisch mit dem Unternehmensnetzwerk verbunden ist \(über Windows integrierte Authentifizierung oder Benutzername und Kennwort\)  
  
-   Versuchen Sie von einer anderen Organisation und sind auf die Ziel-Ansprüche\-unterstützende Anwendung, die von einem vertrauenswürdigen Partner  
  
-   Aus einer SAML 2.0-Identitätsanbieter und sind es wird versucht, auf die Ziel-Ansprüche\-fähigen Anwendung  
  
#### <a name="how-to-use-this-spreadsheet"></a>Gewusst wie: Verwenden Sie diese Tabelle  
Sie können die folgenden Schritte für jede Verbund-Server-farmverwaltungsdatenbank-Instanz verwenden, die Sie zum Ermitteln der empfohlenen Anzahl der Verbundserver bereitstellen möchten.  
  
1.  Herunterladen und öffnen Sie dann die [AD FS Capacity Planning dem Arbeitsblatt zur Dimensionierung für WindowsServer 2012 R2](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) oder [AD FS Capacity Planning dem Arbeitsblatt zur Dimensionierung für WindowsServer 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).
  
2.  In der Zelle rechts neben der **während der spitzenauslastungszeit System Nutzung, erwartet dieser Prozentsatz des für meine Benutzer authentifizieren** Zelle, auf die Zelle, und klicken Sie dann mithilfe der Dropdownliste\-nach-unten-Pfeile, um Ihre geschätzte Systemverwendung auswählen Ebene, entweder **40 %** , **60 %** oder **80 %** für die Bereitstellung.  
  
3.  In der Zelle rechts neben der **in den folgenden Zeitraum** Zelle, auf die Zelle, und klicken Sie dann mithilfe der Dropdownliste\-unten weisenden Pfeil, wählen Sie entweder **1 Minute**, **15 Minuten**, oder **1 Stunde** , wählen Sie die Dauer der Spitzenlast.  
  
4.  In der Zelle rechts neben der **Geben Sie die geschätzte Anzahl von internen Anwendungen \(z. B. SharePoint \(2007 oder 2010\) oder Ansprüche unterstützende Anwendungen\)**  Zelle, geben Sie die Anzahl Interner Anwendungen verwenden Sie in Ihrer Organisation.  
  
5.  In der Zelle rechts neben der **Geben Sie die geschätzte Anzahl von onlineanwendungen \(z. B. Office 365 Exchange Online, SharePoint Online oder Lync Online\)**  Zelle, und geben Sie die Anzahl der online-Anwendungen oder Dienste, die Sie in Ihrer Organisation verwendet.  
  
6.  Unter der Zelle, die mit dem Titel **Anzahl Benutzer**, geben Sie eine Zahl für jede Zeile, die für ein Beispielszenario für die Anwendung Ihre Benutzer gilt wird einmaliges Anmelden müssen\-für den Zugriff auf. Diese Spalte muss die Anzahl der definierten Benutzer, nicht den Spitzenzeiten von Benutzern pro Sekunde enthalten. Wenn der Zugriff bei Zugriffsversuchen auf die Anwendung zunächst über die Seite zur startbereichsermittlung zurückkehren müssen, geben Sie **Y**. Wenn Sie diese Auswahl nicht sicher sind, geben Sie **Y**.  
  
7.  Überprüfen Sie die folgenden empfohlenen Werte, die bereitgestellt werden:  
  
    1.  Die Gesamtanzahl der empfohlenen Verbundserver finden Sie in der unteren rechten Zelle, die in grau markiert ist.  
  
    2.  Die Anzahl von Servern, die für jede Anwendung Beispielszenario empfohlen finden Sie in der Zelle in der Zeile, die in grau markiert ist.  
  
> [!NOTE]  
> Der Wert, der in der Zelle rechts neben der Zelle, die mit der Bezeichnung automatisch berechnet wird **Gesamtanzahl von Verbundservern, die empfohlen** am unteren Rand der Tabelle enthält eine Formel, die einen zusätzlicher Puffer von 20 % auf Hinzufügen, wird die die Gesamtsumme aller Werte in den einzelnen von den einzelnen Zeilen vorangeht. Der Formel hinzugefügt, die **Gesamtanzahl von Verbundservern empfohlen** Zelle erstellt, in diesen Puffer für Ihre gesamten empfohlene Anzahl von bereitgestellten Verbundserver soll sehr unwahrscheinlich, dass die Gesamtlast auf der Farm jemals erreicht wird die Sättigung-Punkt.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
