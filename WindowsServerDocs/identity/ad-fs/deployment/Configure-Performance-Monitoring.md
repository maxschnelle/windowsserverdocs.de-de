---
ms.assetid: 67d8a8d7-2fbd-4ed7-bb41-75769f942024
title: "Konfigurieren der Leistungsüberwachung"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6a7602cddcaee274d42213cd9365f6d1722dab79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-performance-monitoring"></a>Konfigurieren der Leistungsüberwachung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
## <a name="bkmk_ConfigurePerfMon"></a>  
AD FS beinhaltet eigene dedizierte Leistungsindikatoren, um die Leistung der Verbundserver und Verbundserverproxy-Computer zu überwachen. Um Performance Monitor verwenden, um die Leistung Ihrer AD FS-Server überwachen, ist es hilfreich, einen neuen datensammlersatz erstellen und die Ansicht die AD FS-Indikatoren hinzufügen. Das folgende Verfahren beschreibt die Vorgehensweise beim Konfigurieren der Leistungsüberwachung für AD FS.  
  
#### <a name="to-configure-performance-monitoring-for-ad-fs-using-performance-monitor"></a>Zum Konfigurieren der Leistungsüberwachung für AD FS mithilfe des Systemmonitors  
  
1.  Auf der **starten** geben **Systemmonitor**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie in der Konsolenstruktur **Datensammlersätze**, klicken Sie auf **Benutzerdefiniert**, zeigen Sie auf **neu**, und klicken Sie dann auf **Datensammlersatz**.  
  
    Erstellen Sie Data Collector festlegen-Assistenten für neue angezeigt wird.  
  
3.  In **erstellen neue Datensammlersatz**, für **Namen** Geben Sie einen Namen für den neuen datensammlersatz \ (z. B. "AD FS-Leistung" \), klicken Sie auf **\(Advanced\) manuell erstellen**, und klicken Sie dann auf **Weiter**.  
  
4.  Für den Typ der Daten enthalten, überprüfen Sie, ob **Daten Protokolle erstellen** ausgewählt ist, und klicken Sie dann auf die Kontrollkästchen für die folgenden Daten: **Leistungsindikator**, **Ereignisablaufverfolgungsdaten**, **Systemkonfigurationsinformationen**.  
  
5.  Erweitern Sie für die Leistungsindikatoren, **AD FS** in der **Verfügbare Leistungsindikatoren** aus, und klicken Sie dann auf **hinzufügen**.  
  
    Die AD FS-Leistungsindikatoren sollte angezeigt werden, der **Leistungsindikatoren hinzugefügt** Liste.  
  
6.  Wenn Sie aufgefordert werden, Ereignisablaufverfolgungsanbieter hinzuzufügen, klicken Sie auf **hinzufügen**Option **Ereignisse für AD FS** und **AD FS-Ablaufverfolgung** aus der Liste der Anbieter.  
  
7.  Wenn Sie aufgefordert werden, Hinzufügen von Registrierungsschlüsseln zu überwachen, klicken Sie auf **Weiter**.  
  
8.  Wenn Sie aufgefordert werden, geben Sie den Speicherort für die Performance-Daten speichern, können Sie den Standardspeicherort akzeptieren \ (**%systemdrive%\\PerfLogs\\Admin\\***< Data\_collector\_set >*, und klicken Sie dann auf **Weiter**.  
  
9. Wenn Sie aufgefordert werden, den datensammlersatz erstellen, wählen Sie **speichern und schließen Sie**, und klicken Sie dann auf **Fertig stellen**.  
  
    Die neuen datensammlersatz angezeigt wird, in der Konsolenstruktur unter dem **Benutzerdefiniert** Knoten.  
  
10. Verwenden Sie die folgenden Schritte aus, um Arbeiten mit der AD FS-Leistungsindikatoren:  
  
    -   Leistung überwachen mithilfe von Leistungsindikatoren im Zusammenhang mit AD FS\ zunächst mit der rechten Maustaste auf die Sammlung festlegen, dass Sie hinzugefügt \ (z. B. "AD FS-Leistung" \), und klicken Sie dann auf **starten**.  
  
    -   Um einen Bericht zum Anzeigen der Ergebnisse der Systemmonitor erstellen, mit der rechten Maustaste auf die Sammlung festlegen, dass Sie hinzugefügt \ (z. B. "AD FS-Leistung" \), und klicken Sie dann auf **neuesten Bericht**.  
  
    -   Um eine Sammlung von Leistungsdaten zu beenden, damit Sie den neuesten Bericht anzeigen können, klicken Sie auf die Sammlung festlegen, dass Sie hinzugefügt \ (z. B. "AD FS-Leistung" \), und klicken Sie dann auf **beenden**.  
  
    Der neueste Bericht hinzugefügt und automatisch nummeriert \(starting at 000001\) unter der **Report\\User definiert***\\ < Data\_collector\_set >* Knoten in der Konsolenstruktur.  
  
## <a name="ad-fs-performance-counters"></a>AD FS-Leistungsindikatoren  
In der folgende Tabelle werden die AD FS-Leistungsindikatoren aufgeführt und beschrieben, wie sie eignen sich für die Überwachung der Aktivitäten, die auf einem Verbundserver oder Verbundserverproxy bezieht.  
  
|Leistungsindikator|Beschreibung|Kann auf verwendet werden: 
|-----------|---------------|------------------- 
|Tokenanforderungen|Überwacht die Anzahl der token-Anfragen an den Verbundserver einschließlich SSOAuth tokenanforderungen gesendet.|Verbundserver 
|Token Requests\/s|Überwacht die Anzahl der token-Anfragen an den Verbundserver, einschließlich der SSOAuth token Anforderungen pro Sekunde gesendet.|Verbundserver  
|Verbund-Metadaten-Anforderungen|Überwacht die Anzahl der eingehenden Federation Metadatenanforderungen an den Verbundserver gesendet.|Verbundserver  
|Verbund Metadaten Requests\/s|Überwacht die Anzahl der eingehenden Federation Metadaten Anfragen pro Sekunde, die an den Verbundserver gesendet werden.|Verbundserver  
|Artefakt Auflösung Anforderungen|Überwacht die Anzahl der eingehenden Federation Metadaten Anfragen pro Sekunde, die an den Verbundserver gesendet werden.|Verbundserver  
|Artefakt Auflösung Requests\/s|Überwacht die Anzahl der Anfragen an den Artefakt Auflösung Endpunkt pro Sekunde, die an den Verbundserver gesendet werden.|Verbundserver  
|Proxy-Anfragen|Überwacht die Anzahl der eingehenden Anfragen an der Verbundserverproxy gesendet.|Verbundserverproxys  
|Proxy Requests\/s|Überwacht die Anzahl der eingehenden Anfragen pro Sekunde, die an der Verbundserverproxy gesendet werden.|Verbundserverproxys  
|MEX Proxyanforderungen|Überwacht die Anzahl der eingehenden \(MEX\) WS-Metadaten-Anforderungen, die an der Verbundserverproxy gesendet werden.|Verbundserverproxys 
|Proxy MEX Requests\/s|Überwacht die Anzahl der eingehenden MEX-Anforderungen pro Sekunde, die an der Verbundserverproxy gesendet werden.|Verbundserverproxys  
  

