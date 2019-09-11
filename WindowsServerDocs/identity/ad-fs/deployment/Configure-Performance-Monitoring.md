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
ms.openlocfilehash: 82added5018d83aeb9fe7d8033204a0d19bd047a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868098"
---
# <a name="configure-performance-monitoring"></a>Konfigurieren der Leistungsüberwachung
  
## <a name="bkmk_ConfigurePerfMon"></a>  
AD FS umfasst eigene dedizierte Leistungsindikatoren, die Sie beim Überwachen der Leistung von Verbund Servern und Verbund Server Proxy-Computern unterstützen. Wenn Sie die Leistung Ihrer AD FS Server mithilfe des System Monitors überwachen möchten, ist es sinnvoll, einen neuen Datensammler Satz zu erstellen und die AD FS Zähler dieser Ansicht hinzuzufügen. Im folgenden Verfahren wird beschrieben, wie Sie die Leistungsüberwachung für AD FS konfigurieren.  
  
#### <a name="to-configure-performance-monitoring-for-ad-fs-using-performance-monitor"></a>So konfigurieren Sie die Leistungsüberwachung für AD FS mithilfe des System Monitors  
  
1. Geben Sie auf dem **Start** Bildschirm System **Monitor**ein, und drücken Sie dann die EINGABETASTE.  
  
2. Erweitern Sie in der Konsolen Struktur **Datensammler Sätze**, klicken\-Sie mit der rechten Maustaste auf **Benutzer definiert**, zeigen Sie auf **neu**, und klicken Sie dann auf **Datensammler Satz**.  
  
   Der Assistent zum Erstellen eines neuen Datensammler Satzes wird angezeigt.  
  
3. Geben Sie unter **neuen Datensammler Satz erstellen**unter **Name** einen Namen für den neuen Datensammler Satz \(ein, z. b.\)"AD FS Leistung", klicken Sie auf  **\(manuell\)erweitert erstellen**, und klicken Sie dann auf  **Als nächstes**.  
  
4. Vergewissern Sie sich, dass **Datenprotokolle erstellen** ausgewählt ist, und aktivieren Sie dann die Kontrollkästchen für die folgenden Datentypen: **Leistungs**Wert, **Ereignis Ablauf Verfolgungs Daten**, **System Konfigurationsinformationen**.  
  
5. Erweitern Sie für Leistungsindikatoren in der Liste **Verfügbare** Leistungsindikatoren den Eintrag **AD FS** , und klicken Sie dann auf **Hinzufügen**.  
  
   Die AD FS Leistungsindikatoren sollten in der Liste **hinzugefügte Zähler** angezeigt werden.  
  
6. Wenn Sie zum Hinzufügen von Ereignis Ablauf Verfolgungs Anbietern aufgefordert werden, klicken Sie auf **Hinzufügen**, **AD FS** und wählen Sie in der Liste der Anbieter die **AD FS** Ereignisse aus.  
  
7. Wenn Sie zum Hinzufügen von Registrierungs Schlüsseln zur Überwachung aufgefordert werden, klicken Sie auf **weiter**.  
  
8. Wenn Sie zum Angeben des Speicher Orts für die Leistungsdaten aufgefordert werden, können Sie den Standard Speicherort \( **% System Drive%\\Perflogs\\admin\\** _< Data\_Collector akzeptieren. legen\_Sie > fest_, und klicken Sie dann auf **weiter**.  
  
9. Wenn Sie zum Erstellen des Datensammler Satzes aufgefordert werden, wählen Sie **Speichern und schließen**aus, und klicken Sie dann auf **Fertig**stellen.  
  
    Der neue Datensammler Satz wird in der Konsolen Struktur unter dem **benutzerdefinierten** Knoten angezeigt.  
  
10. Verwenden Sie die folgenden Schritte, um mit den AD FS Leistungsindikatoren zu arbeiten:  
  
    -   Klicken Sie\-mit der rechten\-Maustaste auf den Datensammler Satz, den Sie hinzugefügt \(haben, z. b. "AD FS\)Leistung", und klicken Sie dann auf **starten**, um die Leistungsüberwachung mithilfe AD FS  
  
    -   Um einen Bericht zum Anzeigen der Ergebnisse der Leistungsüberwachung zu erstellen\-, klicken Sie mit der rechten Maustaste auf \(den hinzugefügten Datensammler\)Satz, z. b. "AD FS Leistung", und klicken Sie dann auf **neuester Bericht**  
  
    -   Um die Erfassung von Leistungsdaten zu beenden, sodass Sie den aktuellen Bericht anzeigen können,\-klicken Sie mit der rechten Maustaste auf den \(hinzugefügten Datensammler Satz\), z. b. "AD FS Leistung", und klicken Sie dann auf **Beenden**.  
  
    Der aktuelle Bericht wird \(automatisch hinzugefügt und nummeriert, beginnend bei 000001\) unter dem **benutzerdefinierten\\** <em>\\Bericht < Daten\_\_Sammler Satz ></em> Knoten in die Konsolen Struktur.  
  
## <a name="ad-fs-performance-counters"></a>AD FS Leistungsindikatoren  
In der folgenden Tabelle sind die AD FS Leistungsindikatoren aufgelistet. Außerdem wird beschrieben, wie Sie für die Überwachung von Aktivitäten nützlich sind, die entweder mit einem Verbund Server oder einem Verbund Server Proxy verknüpft sind.  
  
|Indikator|Beschreibung|Kann für Folgendes verwendet werden: 
|-----------|---------------|------------------- 
|Tokenanforderungen|Überwacht die Anzahl der Tokenanforderungen, die an den Verbund Server gesendet wurden, einschließlich ssoauth-Tokenanforderungen.|Verbundserver 
|Tokenanforderungen\/Sek.|Überwacht die Anzahl der Tokenanforderungen, die an den Verbund Server gesendet werden, einschließlich ssoauth-Tokenanforderungen pro Sekunde.|Verbundserver  
|Verbundmetadatenanforderungen|Überwacht die Anzahl der eingehenden Verbund Metadatenanforderungen, die an den Verbund Server gesendet werden.|Verbundserver  
|Verbundmetadatenanforderungen\/Sek.|Überwacht die Anzahl eingehender Verbund Metadatenanforderungen, die pro Sekunde an den Verbund Server gesendet werden.|Verbundserver  
|Artefaktauflösungsanforderungen|Überwacht die Anzahl eingehender Verbund Metadatenanforderungen, die pro Sekunde an den Verbund Server gesendet werden.|Verbundserver  
|Artefaktauflösungs\/Anforderungen Sek.|Überwacht die Anzahl der Anforderungen an den artefaktauflösungs-Endpunkt pro Sekunde, die an den Verbund Server gesendet werden.|Verbundserver  
|Proxy Anforderungen|Überwacht die Anzahl der eingehenden Anforderungen, die an den Verbund Server Proxy gesendet werden.|Verbund Server Proxys  
|Proxy Anforderungen\/Sek.|Überwacht die Anzahl der pro Sekunde eingehenden Anforderungen, die an den Verbund Server Proxy gesendet werden.|Verbund Server Proxys  
|Proxy-MEX-Anforderungen|Überwacht die Anzahl eingehender WS\--Metadatenaustausch\) \(-MEX-Anforderungen, die an den Verbund Server Proxy gesendet werden.|Verbund Server Proxys 
|Proxy-MEX\/-Anforderungen Sek.|Überwacht die Anzahl eingehender MEX-Anforderungen pro Sekunde, die an den Verbund Server Proxy gesendet werden.|Verbund Server Proxys  
  

