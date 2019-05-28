---
ms.assetid: 67d8a8d7-2fbd-4ed7-bb41-75769f942024
title: Konfigurieren der Leistungsüberwachung
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5426ea929037e59d2105fb2b3b06d4ebfdb7a577
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192287"
---
# <a name="configure-performance-monitoring"></a>Konfigurieren der Leistungsüberwachung
  
## <a name="bkmk_ConfigurePerfMon"></a>  
AD FS umfasst eine eigene dedizierte Leistungsindikatoren, um die Leistung der Verbundserver und Verbundserverproxy-Computer zu überwachen. Um Systemmonitor zur Überwachung der Leistung von AD FS-Server zu verwenden, ist es nützlich, um einen neuen datensammlersatz erstellen und diese Ansicht die AD FS-Leistungsindikatoren hinzugefügt. Das folgende Verfahren beschreibt das Konfigurieren der Leistungsüberwachung für AD FS.  
  
#### <a name="to-configure-performance-monitoring-for-ad-fs-using-performance-monitor"></a>Zum Konfigurieren der Leistungsüberwachung für AD FS mit dem Systemmonitor  
  
1.  Auf der **starten** geben **Systemmonitor**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie in der Konsolenstruktur **Data Collector Sets**mit der rechten Maustaste\-klicken Sie auf **benutzerdefinierte**, zeigen Sie auf **neu**, und klicken Sie dann auf **Data Collector Set** .  
  
    Die Assistenten Erstellen einer neuen Data Collector festgelegt wird.  
  
3.  In **Erstellen neuer Data Collector Set**, für die **Namen** Geben Sie einen Namen für den neuen datensammlersatz \(wie z. B. "AD FS-Leistung"\), klicken Sie auf **manuell erstellen \( Erweiterte\)** , und klicken Sie dann auf **Weiter**.  
  
4.  Überprüfen Sie für den Typ der Daten eingeschlossen werden sollen, ob **erstellen Datenprotokolle** ausgewählt ist, und klicken Sie dann auf die Kontrollkästchen für die folgenden Datentypen: **Leistungsindikator**, **Ereignisablaufverfolgungsdaten**, **Informationen zur Betriebssystemkonfiguration**.  
  
5.  Erweitern Sie für die Leistungsindikatoren, **AD FS** in die **Verfügbare Leistungsindikatoren** aus, und klicken Sie dann auf **hinzufügen**.  
  
    Die AD FS-Leistungsindikatoren angezeigt werden soll die **Leistungsindikatoren hinzugefügt** Liste.  
  
6.  Wenn Sie aufgefordert werden, Ereignisablaufverfolgungsanbieter hinzuzufügen, klicken Sie auf **hinzufügen**Option **AD FS-Ereignisse** und **AD FS-Ablaufverfolgung** aus der Liste der Anbieter.  
  
7.  Wenn Sie gefragt werden zum Hinzufügen von Registrierungsschlüsseln, um zu überwachen, klicken Sie auf **Weiter**.  
  
8.  Wenn Sie aufgefordert werden, um den Speicherort zum Speichern der Daten anzugeben, können Sie den Standardspeicherort übernehmen \( * *%SystemDrive%\\PerfLogs\\Admin\\*** < Daten\_Collector\_festgelegt >* , und klicken Sie dann auf **Weiter**.  
  
9. Wenn Sie aufgefordert werden, um den Sammlungssatz zu erstellen, wählen Sie **speichern und schließen Sie**, und klicken Sie dann auf **Fertig stellen**.  
  
    Der neue Sammlungssatz wird angezeigt, in der Konsolenstruktur unter den **benutzerdefinierte** Knoten.  
  
10. Verwenden Sie die folgenden Schritte aus, um die Arbeit mit den AD FS-Leistungsindikatoren:  
  
    -   Um zu beginnen, Überwachung der Anwendungsleistung mithilfe von AD FS\-bezogene Indikatoren, die direkt\-klicken Sie auf den datensammlersatz, den Sie hinzugefügt \(wie z. B. "AD FS-Leistung"\), und klicken Sie dann auf **starten**.  
  
    -   Zum Erstellen eines Berichts zum Anzeigen der Ergebnisse für die Leistungsüberwachung rechten\-klicken Sie auf den datensammlersatz, den Sie hinzugefügt \(wie z. B. "AD FS-Leistung"\), und klicken Sie dann auf **des neuesten Berichts**.  
  
    -   Um eine Erfassung von Leistungsdaten zu beenden, damit Sie den aktuellen Bericht anzeigen können, nach rechts\-klicken Sie auf den datensammlersatz, den Sie hinzugefügt \(wie z. B. "AD FS-Leistung"\), und klicken Sie dann auf **beenden**.  
  
    Der aktuelle Bericht hinzugefügt und automatisch nummerierten \(000001 beginnend\) unter den **Bericht\\Benutzer benutzerdefinierte ***\\< Daten\_Collector\_festgelegt >* Knoten in der Konsolenstruktur.  
  
## <a name="ad-fs-performance-counters"></a>AD FS-Leistungsindikatoren  
In der folgende Tabelle werden die AD FS-Leistungsindikatoren aufgeführt und beschrieben, wie sie sind hilfreich für die Überwachung der Aktivität, die auf einem Verbundserver oder Verbundserverproxy bezieht.  
  
|Leistungsindikator|Beschreibung|Auf die Option kann verwendet werden: 
|-----------|---------------|------------------- 
|Tokenanforderungen|Überwacht die Anzahl der token an den Verbundserver, einschließlich SSOAuth tokenanforderungen gesendeten Anforderungen.|Verbundserver 
|Tokenanforderungen\/Sek.|Überwacht die Anzahl der token an den Verbundserver, einschließlich SSOAuth tokenanforderungen pro Sekunde gesendeten Anforderungen.|Verbundserver  
|Verbundmetadatenanforderungen|Überwacht die Anzahl von eingehenden Anforderungen des Verbund-Metadaten an den Verbundserver gesendet.|Verbundserver  
|Verbund-Metadatenanforderungen\/Sek.|Überwacht die Anzahl der Verbund-Metadaten pro Sekunde eingehende Anforderungen, die an den Verbundserver gesendet werden.|Verbundserver  
|Artefaktauflösungsanforderungen|Überwacht die Anzahl der Verbund-Metadaten pro Sekunde eingehende Anforderungen, die an den Verbundserver gesendet werden.|Verbundserver  
|Artefakt-Namensauflösungsanforderungen\/Sek.|Überwacht die Anzahl der Anforderungen an den Artefakt-Auflösung-Endpunkt pro Sekunde, die an den Verbundserver gesendet werden.|Verbundserver  
|Proxy für Anforderungen|Überwacht die Anzahl von eingehenden Anforderungen an den Verbundserverproxy gesendet.|Verbundserverproxys  
|Fordert der Reverseproxy\/Sek.|Überwacht die Anzahl der pro Sekunde eingehende Anforderungen, die auf dem Verbundserverproxy gesendet werden.|Verbundserverproxys  
|Proxy-MEX-Anforderungen|Überwacht die Anzahl der eingehenden WS\-Metadatenaustausch \(MEX\) Anforderungen, die an den Verbundserverproxy gesendet werden.|Verbundserverproxys 
|MEX-Proxyanforderungen\/Sek.|Überwacht die Anzahl der pro Sekunde eingehende MEX-Anforderungen, die auf dem Verbundserverproxy gesendet werden.|Verbundserverproxys  
  

