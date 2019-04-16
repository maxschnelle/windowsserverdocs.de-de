---
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: "Planen der Verbundserverkapazität"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 618dc9419be965dedaaf7dc946da436a5001f121
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-federation-server-capacity"></a>Planen der Verbundserverkapazität

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Kapazitätsplanung für Verbundserver können Sie die schätzen:  
  
-   Welche Faktoren wächst die Größe der AD FS-Konfigurationsdatenbank.  
  
-   Die entsprechenden Hardwareanforderungen für jeden Verbundserver.  
  
-   Die Anzahl der Verbundserver in jeder Organisation platzieren.  
  
Verbundserver Ausstellung von Sicherheitstoken für Benutzer. Diese Token werden für eine vertrauende Seite für die Nutzung von angezeigt. Verbundserver Ausstellung von Sicherheitstoken, nach der Authentifizierung eines Benutzers oder nach dem Empfang ein Sicherheitstoken, die zuvor von einem Partner Verbunddienst ausgegeben wurde. Ein Sicherheitstoken wird vom Verbunddienst angefordert, wenn Benutzer zunächst auf verbundanwendungen anmelden oder ihre Sicherheitstoken abläuft, während sie auf verbundanwendungen zugreifen.  
  
Verbundserver dienen zur Farm-Serverkonfigurationen Hochverfügbarkeitsszenarien sein, die Microsoft-Netzwerklastenausgleich \(NLB\)-Technologie verwenden. Verbundserver in einer Farmkonfiguration können unabhängig voneinander Clientanforderungen verarbeiten, ohne den Zugriff auf eine beliebige allgemeine Farmkomponenten für jede Anforderung. Daher ist wenig Aufwand bei der Skalierung einer Federation Server-Bereitstellung.  
  
**Empfehlungen:**  
  
-   Für wichtige Mission\ oder Hochverfügbarkeitsszenarien Bereitstellungen, empfehlen wir die Erstellung einer kleinen Verbundserverfarm in jeder Partnerorganisation, mit mindestens zwei Verbundserver pro Farm, um Fehlertoleranz bereitzustellen.  
  
-   Gegen die Notwendigkeit für hohe Verfügbarkeit und die einfache Skalierung von Verbundservern ist Horizontales Skalieren die empfohlene Methode für die Behandlung von eine hohe Anzahl von Anforderungen pro Sekunde für einen bestimmten Verbunddienst aus. Skalierung von außerhalb der Basiskonfiguration in diesem Handbuch ist unwahrscheinlich erhebliche Kapazität behandeln Gewinne zu erstellen.  
  
## <a name="ad-fs-configuration-database-size-and-growth"></a>AD FS-Konfiguration Datenbankgröße und -Wachstum  
Die Größe der AD FS-Konfigurationsdatenbank werden in der Regel als kleine betrachtet und Größe der Datenbank ist nicht in der Regel ein wichtiger Aspekt in AD FS-Bereitstellungen werden.  Die genaue Größe der AD FS-Konfigurationsdatenbank kann hängen größtenteils die Anzahl der Vertrauensstellungen und die zugehörigen Metadaten im Zusammenhang mit Trust\ – z.B. Ansprüche, Anspruchsregeln und Überwachungseinstellungen für jede Vertrauensstellung konfiguriert. Die Anzahl der Vertrauensstellung Einträge in der Konfigurationsdatenbank wächst, wächst die Notwendigkeit mehr Speicherplatz.  
  
Weitere Informationen zur Bereitstellung über die AD FS-Konfigurationsdatenbank finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md).  
  
## <a name="memory-cpu-and-disk-space-requirements"></a>Arbeitsspeicher, CPU und Speicherplatz  
Glücklicherweise Arbeitsspeicher, CPU und Speicherplatz für Verbundserver werden, und es sind keine wahrscheinlich eine treibende Kraft in Entscheidungen, die Hardware. Weitere Informationen zu den Hardwareanforderungen finden Sie unter [AnhangA: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md).  
  
> [!NOTE]  
> Tests, die vom AD FS-Produktteam mit einer Verbundserverfarm konfiguriert mit einem dedizierten SQL Server zum Speichern der AD FS-Konfigurationsdatenbank ausgeführt wurden, erweitern die Gesamtauslastung auf dem SQL Server gering. In einem Test mit einer Four\-Federation\-Server-Farm, die einem einzelnen SQL-Server konfiguriert wurde, überstiegen nicht 10% trotz Tests, die die Verbundservern Ziel Auslastung CPU-Auslastung.  
  
## <a name="bk_estimatefs"></a>Abschätzen der Anzahl der Verbundserver für Ihre Organisation  
In dem Bestreben, um die Planung für Verbundserver Hardware zu optimieren entwickelt die AD FS-Produktteams die AD FS Capacity Dimensionierung. Diese Excel-Tabelle enthält Calculator\ ähnliche Funktionen, die erwarteten Nutzungsdaten ausführt, über die Benutzer in Ihrer Organisation bereitstellen und eine empfohlene optimale Anzahl der Verbundserver für die AD FS-Produktionsumgebung.  
  
> [!NOTE]  
> Die Anzahl der Verbundserver, die diese Tabelle empfehlen wird basiert auf den Hardware- und Netzwerkkonfiguration Spezifikationen, die die AD FS-Produktteam während der Tests verwendet. Daher muss die Anzahl der Verbundserver, die die Tabelle empfehlen wird in diesem Kontext verstanden werden.  Weitere Informationen zu den Spezifikationen, die während der Tests verwendet, finden Sie unter dem Thema [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md).  
  
### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>Verwenden die AD FS-Kapazitätsplanung Dimensionierung  
Wenn Sie diese Tabelle verwenden, müssen Sie zum Auswählen eines Werts \ (entweder **40 %**, **60 %**, oder **80 %**\) dar, am besten den Prozentsatz der Gesamtanzahl der Benutzer erwartet sendet Authentifizierungsanfragen auf Ihren Verbundserver während der Spitzenzeiten.  
  
Sie müssen dann wählen Sie einen Wert \ (entweder **1 Minute**, **15 Minuten**, oder **1 Stunde**\) dar, am besten die Zeitspanne Sie davon ausgehen, die maximale Verwendungszeitraum bis zum letzten dass. Sie können z.B. 40% als Wert für die Gesamtanzahl der Benutzer schätzen, die innerhalb eines Zeitraums von 15Minuten Anmeldung wird oder 60% der Benutzer wird innerhalb eines Zeitraums von einer Stunde anmelden. Zusammen definieren diese Werte das Gipfel Load-Profil, Ihre Größe Empfehlung berechnet werden.  
  
Als Nächstes müssen Sie die Gesamtanzahl der Benutzer angeben, die eine einzelne Standardparameter-Zugriff auf die Claims\ unterstützende Zielanwendung, basierend auf, ob der Benutzer sind erfordern:  
  
-   Anmelden bei Active Directory von einem lokalen Computer, die physisch mit dem Unternehmensnetzwerk verbunden ist \ (über die integrierte Windows-Authentication\)  
  
-   Protokollierung in Active Directory Remote von einem Computer, die nicht physisch mit dem Unternehmensnetzwerk verbunden ist \ (in Windows integrierte Authentifizierung oder Benutzernamen und Password\)  
  
-   Versuchen Sie, aus einer anderen Organisation und sind von einem vertrauenswürdigen Partner Claims\-fähige Anwendung den Zugriff auf  
  
-   Versuchen Sie, von einem SAML 2.0-Identitätsanbieter herzustellen und sind Claims\-fähige Anwendung den Zugriff auf  
  
#### <a name="how-to-use-this-spreadsheet"></a>Wie Sie dieses Arbeitsblatts  
Sie können die folgenden Schrittefür jede Instanz eines Federation Serverfarm, die Sie bereitstellen, um die empfohlene Anzahl der Verbundserver ermitteln möchten.  
  
1.  Herunterladen und öffnen Sie dann die [AD FS Capacity Planning Dimensionierung für Windows Server 2012 R2](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) oder [AD FS Capacity Planning Dimensionierung für Windows Server 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).
  
2.  In der Zelle rechts neben der **Zeitraum Nutzung Gipfel System ich davon ausgehen, dass dieser Prozentsatz der Benutzer zur Authentifizierung** Zelle, klicken Sie auf die Zelle, und klicken Sie dann die Pfeile Drop\ verwenden, um Ihre geschätzte Auslastung Systemebene, wählen Sie entweder **40 %**, **60 %** oder **80 %** für die Bereitstellung.  
  
3.  In der Zelle rechts neben der **in den folgenden Zeitraum** Zelle, klicken Sie auf die Zelle, und klicken Sie dann die Drop\ Dropdownpfeile verwenden, wählen Sie entweder **1 Minute**, **15 Minuten**, oder **1 Stunde** die Dauer der Spitzenzeiten auswählen.  
  
4.  In der Zelle rechts neben der **EINGABETASTE geschätzte Anzahl der internen Anwendungen \ (z.B. SharePoint \(2007 or 2010\) oder Ansprüche unterstützende Applications\)** Zelle, und geben Sie die Anzahl der internen Anwendungen, die Sie in Ihrer Organisation verwenden.  
  
5.  In der Zelle rechts neben der **EINGABETASTE geschätzte Anzahl der Online-Applikationen \ (z.B. Office365 Exchange Online, SharePoint Online oder Lync Online\)** Zelle, und geben Sie die Anzahl der Online-Anwendungen oder Dienste, die in Ihrer Organisation verwendet wird.  
  
6.  Unter der Zelle, die mit dem Titel **Anzahl der Benutzer**, müssen eine Zahl für jede Zeile, die für ein Beispielszenario für die Anwendung Ihre Benutzer gilt Standardparameter-Zugriff auf einzelne, geben. In dieser Spalte sollte die Anzahl der definierten Benutzer, nicht die maximale Benutzer pro Sekunde enthalten. Wenn Versuche unternommen, die Anwendung zunächst über die Seite zur startbereichsermittlung zurückkehren müssen, geben Sie **Y**. Wenn Sie diese Option nicht kennen, geben Sie **Y**.  
  
7.  Überprüfen Sie die folgenden empfohlenen Werte, die bereitgestellt werden:  
  
    1.  Die Gesamtanzahl der empfohlenen Verbundserver finden Sie in der unteren rechten Zelle, die in grau markiert ist.  
  
    2.  Die Anzahl der Server, die für jede Anwendung Beispielszenario empfohlen finden Sie in der Zelle in der Zeile, die in grau markiert ist.  
  
> [!NOTE]  
> Der Wert, der in der Zelle rechts neben der Zelle, die mit dem Titel automatisch berechnet werden **Gesamtanzahl der Verbundserver empfohlen** am unteren Rand der Tabelle enthält eine Formel einen zusätzlicher Puffer von 20% der Gesamtmenge des für alle Werte in den einzelnen von den einzelnen Zeilen vor hinzugefügt wird. Die Formel hinzugefügt, die **Gesamtanzahl der Verbundserver empfohlen** Zelle Builds in dieses Puffers zum Gesamtbetrag empfohlene Anzahl der bereitgestellten Verbundserver zu es sehr unwahrscheinlich, dass die Gesamtauslastung in der Farm jemals dessen Sättigung Punkt auftritt.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
