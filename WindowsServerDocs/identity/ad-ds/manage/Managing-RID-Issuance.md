---
ms.assetid: aac117a7-aa7a-4322-96ae-e3cc22ada036
title: Verwalten der RID-Ausstellung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f84bcc1aa32e9993903e094fc43feffcbe16a05b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="managing-rid-issuance"></a>Verwalten der RID-Ausstellung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die Änderung an der RID-master FSMO-Rolle, inklusive der neuen ausstellungs- und Überwachungsfunktionen im RID-Master und zum Analysieren und Beheben von RID-Ausstellung.  
  
-   [Verwalten der RID-Ausstellung](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Manage)  
  
-   [Problembehandlung bei der RID-Ausstellung](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Tshoot)  
  
Weitere Informationen finden Sie unter der [AskDS-Blog](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx).  
  
## <a name="BKMK_Manage"></a>Verwalten der RID-Ausstellung  
Standardmäßig verfügt über eine Domäne Kapazität für ungefähr 1 Milliarde Sicherheitsprinzipale, z. B. Benutzer, Gruppen und Computer. Es gibt natürlich keine Domänen mit so vielen aktiv genutzten Objekten. Microsoft-Kundensupport hat jedoch Fälle gefunden, in denen:  
  
-   Bereitstellen von Software oder Verwaltungsskripts versehentlich massenweise erstellt, Benutzer, Gruppen und Computer.  
  
-   Viele nicht genutzte Sicherheits- und Verteilergruppen wurden delegierte Benutzer erstellt  
  
-   Viele Domänencontroller herabgestuft, wiederhergestellt oder deren Metadaten bereinigt wurden  
  
-   Gesamtstruktur-Wiederherstellungen durchgeführt wurden  
  
-   Die InvalidateRidPool-Operation wurde häufig durchgeführt  
  
-   Der Registrierungswert RID-Blockgröße wurde falsch erhöht  
  
All diese Situationen verbrauchen RIDs unnötig, oft aus versehen. Über die Jahre einige Umgebungen die RIDs ausgegangen ausgeführt wurde und wodurch Migrieren zu einer neuen Domäne oder Wiederherstellungen der Gesamtstruktur.  
  
Windows Server 2012 Lösungen für Probleme mit der RID-Zuweisung, die nur mit dem Alter und der Allgegenwärtigkeit von Active Directory geworden sind. Dazu gehören eine bessere ereignisprotokollierung, besser geeignete Grenzen und die Möglichkeit, im Notfall -, die Gesamtgröße des RID-gesamtpoolzuweisung für eine Domäne zu verdoppeln.  
  
### <a name="periodic-consumption-warnings"></a>Regelmäßige Verbrauchswarnungen  
Windows Server 2012 hinzugefügt, dass der globales RID-Speicherplatz Ereignis nachverfolgen, die liefert frühzeitige Warnungen, wenn wichtige Meilensteine überschritten werden. Das Modell berechnet die zehn (10) Prozent Mark in den globalen Pool verwendet und protokolliert ein Ereignis, wenn erreicht. Klicken Sie dann die nächsten zehn Prozent des verbleibenden berechnet und der Ereigniszyklus wird fortgesetzt. Da der globale RID-Raum erschöpft ist, Ereignisse werden beschleunigt als zehn Prozent Cachetreffer schneller in einem abnehmenden Pool (aber Ereignisprotokoll-Dämpfung verhindert, dass mehr als einen Eintrag pro Stunde). Das Systemereignisprotokoll auf jedem Domänencontroller schreibt Verzeichnisdienste-SAM-Ereignis 16658.  
  
Sofern eine standardmäßig 30 Bit globale RID-Raum, den ersten Ereignisprotokollen beim Zuordnen des Pools die 107,374,182<sup>Nd</sup> RID. Das Ereignis beschleunigen auf natürliche Weise bis zum letzten Checkpoint von 100.000, mit 110 insgesamt generierten Ereignissen. Das Verhalten ist für eine entsperrt 31-Bit-RID-gesamtpoolzuweisung ähnlich: beginnend mit 214.748.365 und insgesamt 117 Ereignissen.  
  
> [!IMPORTANT]  
> Dieses Ereignis wird nicht erwartet. Untersuchen Sie die Benutzer, Computer und Gruppe Erstellung Prozesse in der Domäne unverzüglich. Erstellen von mehr als 100 Millionen AD DS-Objekte ist sehr ungewöhnlich.  
  
![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_EventWaypoints2.png)  
  
### <a name="rid-pool-invalidation-events"></a>RID-Pool-Ungültigmachung  
Es sind neue darauf hin, dass ein lokaler Domänencontroller RID-Pool verworfen wurde. Diese Informationscharakter und sind möglicherweise zu erwarten, insbesondere aufgrund der neuen VDC-Funktionen. Finden Sie die folgende Ereignisliste enthält weitere Details auf das Ereignis.  
  
### <a name="BKMK_RIDBlockMaxSize"></a>RID-Blockgröße  
Normalerweise fordert ein Domänencontroller auf einmal RID-Zuweisungen in Blöcken von 500 RIDs an. Sie können diesen Standardwert über den folgenden REG_DWORD-Registrierungswert auf einem Domänencontroller überschreiben:  
  
```  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\RID Values  
RID Block Size  
  
```  
  
Vor Windows Server 2012 gab es keine maximale Wert in diesem Registrierungsschlüssel, mit Ausnahme der impliziten DWORD-Obergrenze (mit einem Wert von 0xffffffff oder 4294967295) erzwungen. Dieser Wert ist wesentlich kleiner als der gesamten globalen RID-Raum. Administratoren konfiguriert manchmal nicht ordnungsgemäß oder versehentlich RID-Blockgröße mit Werten, die die globalen RID rasant erschöpft.  
  
In Windows Server 2012 kann nicht diesen Registrierungswert höher als 15.000 dezimal (0x3A98 hexadezimal) festlegen. Dies verhindert, dass massive unbeabsichtigte RID-Zuweisung.  
  
Wenn Sie den Wert festlegen *höhere* als 15.000 setzen, wird der Wert als 15.000 behandelt, und der Domänencontroller protokolliert das Ereignis 16653 im den Verzeichnisdienst-Ereignisprotokoll bei jedem Neustart, bis der Wert korrigiert wird.  
  
### <a name="BKMK_GlobalRidSpaceUnlock"></a>Freischalten des globalen RID-Speicherplatz  
Vor Windows Server 2012 war der globale RID-Raum auf 2 begrenzt<sup>30</sup> (bzw. 1.073.741.823) RIDs insgesamt. Erreichen, dürfen nur eine Domäne Migration oder Gesamtstruktur Wiederherstellung auf einem älteren Zeitrahmen Erstellen von neuen SIDs - Wiederherstellung von Maßnahmen. Ab Windows Server 2012, das 2<sup>31</sup> Bit freigeschaltet werden, um den globalen Pool auf 2.147.483.648 RIDs zu vergrößern.  
  
AD DS speichert diese Einstellung in einem versteckten Attribut mit dem Namen **SidCompatibilityVersion** im RootDSE-Kontext aller Domänencontroller. Dieses Attribut ist nicht lesbar mit ADSIEdit, LDP oder anderen Tools. Um eine Erhöhung der globale RID-Raum angezeigt wird, überprüfen Sie das Systemereignisprotokoll nach dem Warnungsereignis 16655 von Verzeichnisdienste-SAM oder verwenden Sie den folgenden Dcdiag-Befehl:  
  
```  
Dcdiag.exe /TEST:RidManager /v | find /i "Available RID Pool for the Domain"  
  
```  
  
Wenn Sie den globalen RID-Pool vergrößern, wird der verfügbaren auf 2.147.483.647 vom Standardwert 1.073.741.823 ändern. Zum Beispiel:  
  
![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_Dcdiag.png)  
  
> [!WARNING]  
> Diese freischaltung dient *nur* Erschöpfung der RIDS zu verhindern und verwendet werden soll *nur* in Verbindung mit RID-Obergrenzenerzwingung (siehe nächster Abschnitt). Führen Sie nicht "vorsorglich" dies in Umgebungen mit Millionen freier RIDs und geringem Wachstum, wie App-Kompatibilitätsprobleme mit aus dem freigeschalteten RID-Pool potenziell vorhanden sind.  
>   
> Diese freischaltung kann nicht zurückgesetzt werden oder entfernt, es sei denn, eine komplette Wiederherstellung der Gesamtstruktur auf einen früheren Zeitpunkt.  
  
#### <a name="important-caveats"></a>Wichtigen Einschränkungen  
Windows Server 2003 und Windows Server 2008-Domänencontroller können keine ausstellen RIDs, wenn der globale RID-pool 31<sup>St</sup> Bit entsperrt ist. Windows Server 2008 R2-Domänencontrollern *können* verwenden 31<sup>St</sup> bit RIDs *jedoch nur, wenn* haben sie Hotfix [KB 2642658](https://support.microsoft.com/kb/2642658) installiert. Nicht unterstützte und nicht gepatchte Domänencontroller behandeln den globalen RID-Pool als erschöpft, wenn dieser freigeschaltet wurde.  
  
Dieses Feature ist nicht von keiner Domänenfunktionsebene erzwungen. Achten Sie, die nur für Windows Server 2012 oder aktualisierten Windows Server 2008 R2-Domänencontroller vorhanden sind in der Domäne.  
  
#### <a name="implementing-unlocked-global-rid-space"></a>Implementieren von freigeschalteten globalen RID-Raums  
Zum Entsperren des RID-Pools und die 31<sup>St</sup> Bit nach dem Empfang der RID-grenzwertwarnung (siehe unten) die folgenden Schritte ausführen:  
  
1.  Stellen Sie sicher, dass der RID-Master-Rolle auf einem Windows Server 2012-Domänencontroller ausgeführt wird. Wenn dies nicht der Fall ist, auf einem Windows Server 2012-Domänencontroller übertragen.  
  
2.  Führen Sie LDP.exe  
  
3.  Klicken Sie auf die **Verbindung** und dann auf **verbinden** für Windows Server 2012 RID-Master auf port 389 und klicken Sie dann auf **binden** als Domänenadministrator an.  
  
4.  Klicken Sie auf die **Durchsuchen** und dann auf **ändern**.  
  
5.  Stellen Sie sicher, dass **DN** ist leer.  
  
6.  In **Attributeingabe bearbeiten**, Typ:  
  
    ```  
    SidCompatibilityVersion  
    ```  
  
7.  In **Werte**, Typ:  
  
    ```  
    1  
    ```  
  
8.  Stellen Sie sicher, dass **hinzufügen** ausgewählt ist **Vorgang** , und klicken Sie auf **EINGABETASTE**. Aktualisiert die **Eingabeliste**.  
  
9. Wählen Sie die **synchron** und **Extended** Optionen, klicken Sie dann auf **ausführen**.  
  
    ![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModify.png)  
  
10. Wenn dies erfolgreich war, im LDP-Ausgabefenster angezeigt:  
  
    ```  
    ***Call Modify...  
     ldap_modify_ext_s(Id, '(null)',[1] attrs, SvrCtrls, ClntCtrls);  
    modified "".  
  
    ```  
  
    ![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModifySuccess.png)  
  
11. Den globale RID-Pool vergrößert das Systemereignisprotokoll auf diesem Domänencontroller für Verzeichnisdienste-SAM-Informationsereignis 16655 zu bestätigen.  
  
### <a name="rid-ceiling-enforcement"></a>RID-Obergrenzenerzwingung  
Zum Schutz leisten und erhöhte Rechte für Administratoren Awareness, führt Windows Server 2012 eine künstliche Obergrenze für den globalen RID-Raum bei zehn (10) Prozent der verbleibenden RIDs im globalen Raum. Wenn in einem (1) Prozent der künstlichen Obergrenze verbleiben, Schreiben Domänencontroller RID-Pools Verzeichnisdienste-SAM-Warnungsereignis 16656 in deren Systemereignisprotokoll. Beim Erreichen der Obergrenze zehn Prozent der RID-Master-FSMO, schreibt Verzeichnisdienste-SAM-Ereignis 16657 in dessen Systemereignisprotokoll und wird nicht reserviert werden weitere RID-Pools bis die Obergrenze überschreiben. Dies zwingt Sie den Zustand des RID-Masters in der Domäne und potenzielle Limit für RID-Zuweisung zu beheben. Dies wird auch verhindert, dass Domänen Überbeanspruchung den gesamten RID-Raum.  
  
Dieser Grenzwert ist hartcodiert bei verbleibenden zehn Prozent des verfügbaren RID-Speichers. Das heißt, aktiviert die Obergrenze der RID-Master einen Pool zuweist, der die neunzig (90) Prozent des globalen RID-Speichers für RID enthält.  
  
-   Für Standarddomänen, ist der erste Auslöser Punkt 2<sup>30</sup>-1 * 0,90 = 966.367.640 (bzw. 107.374.183 verbleibenden RIDs).  
  
-   Für Domänen mit einer entsperrt 31-Bit-RID-Raum liegt der Auslöser 2<sup>31</sup>-1 * 0,90 = 1.932.735.282 (bzw. 214.748.365 verbleibenden RIDs).  
  
Wenn ausgelöst wird, legt der RID-Master Active Directory-Attribut **MsDS-RIDPoolAllocationEnabled** (common Name **setzt**) für das Objekt auf FALSE:  
  
CN = RID Manager$, CN = System, DC =*<domain>*  
  
Dieses Ereignis 16657 wird geschrieben und verhindert die weitere Ausstellung von RID-Blocks auf allen Domänencontrollern. Domänencontroller weiterhin alle ausstehenden ausgestellten RID-Pools nutzen.  
  
Um den Block zu entfernen, und ermöglichen RID-Pool-Zuweisung, um den Vorgang fortzusetzen, setzen Sie diesen Wert auf "true" fest. Auf der nächsten RID-Zuweisung durch den RID-Master wird das Attribut auf den Standardwert NOT SET zurück. Danach sind keine weiteren Obergrenzen und zu einem späteren Zeitpunkt im globale RID-Raum wird, die Gesamtstruktur-Wiederherstellung oder Domänenmigration erfordern.  
  
#### <a name="removing-the-ceiling-block"></a>Entfernen der Obergrenzensperre  
Führen Sie die folgenden Schritte aus, um den Block nach dem Erreichen der künstlichen Obergrenze zu entfernen:  
  
1.  Stellen Sie sicher, dass der RID-Master-Rolle auf einem Windows Server 2012-Domänencontroller ausgeführt wird. Wenn dies nicht der Fall ist, auf einem Windows Server 2012-Domänencontroller übertragen.  
  
2.  Führen Sie LDP.exe.  
  
3.  Klicken Sie auf die **Verbindung** und dann auf *verbinden* für Windows Server 2012 RID-Master auf port 389 und klicken Sie dann auf **binden** als Domänenadministrator an.  
  
4.  Klicken Sie auf die **Ansicht** und dann auf **Struktur**, klicken Sie dann für die **Basis-DN** wählen Sie die Domänen-Namenskontext des RID-Masters. Klicken Sie auf **Ok**.  
  
5.  Klicken Sie im Navigationsbereich einen Drilldown in die **CN = System** Container, und klicken Sie auf die **CN = RID Manager$** Objekt. Rechts klicken Sie darauf, und klicken Sie auf **ändern**.  
  
6.  Geben Sie im Attributeingabe bearbeiten:  
  
    ```  
    MsDS-RidPoolAllocationEnabled  
    ```  
  
7.  In **Werte**, Folgendes ein (in Großbuchstaben):  
  
    ```  
    TRUE  
    ```  
  
8.  Wählen Sie **ersetzen** in **Vorgang** , und klicken Sie auf **EINGABETASTE**. Aktualisiert die **Eingabeliste**.  
  
9. Aktivieren der **synchron** und **Extended** Optionen, klicken Sie dann auf **ausführen**:  
  
    ![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeiling.png)  
  
10. Wenn dies erfolgreich war, im LDP-Ausgabefenster angezeigt:  
  
    ```  
    ***Call Modify...  
    ldap_modify_ext_s(ld, 'CN=RID Manager$,CN=System,DC=<domain>',[1] attrs, SvrCtrls, ClntCtrls);  
    Modified "CN=RID Manager$,CN=System,DC=<domain>".  
  
    ```  
  
    ![RID-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeilingSuccess.png)  
  
### <a name="other-rid-fixes"></a>Sonstige RID-Korrekturen  
Frühere Windows Server-Betriebssysteme musste einen RID-Pool, wenn das rIDSetReferences-Attribut. Zum Beheben dieses Problems auf den Domänencontrollern, auf denen Windows Server 2008 R2 ausgeführt wird, installieren Sie den Hotfix aus [KB 2618669](https://support.microsoft.com/kb/2618669).  
  
### <a name="unfixed-rid-issues"></a>Nicht korrigierte RID-Probleme  
In der Vergangenheit wurde ein Speicherverlust RID auf Fehler beim Erstellen des Kontos; Wenn Sie ein Konto zu erstellen, ist Fehler weiterhin vom eine RID verbraucht. Ein gängiges Beispiel ist einen Benutzer mit einem Kennwort zu erstellen, die komplexitätsanforderungen nicht erfüllt.  
  
### <a name="rid-fixes-for-earlier-versions-of-windows-server"></a>RID-Korrekturen für ältere Versionen von Windows Server  
Alle Korrekturen und Änderungen, die oben genannten besitzen existieren Hotfixes für Windows Server 2008 R2. Es sind zurzeit keine Windows Server 2008-Hotfixes geplant oder in Arbeit.  
  
## <a name="BKMK_Tshoot"></a>Problembehandlung bei der RID-Ausstellung  
  
### <a name="introduction-to-troubleshooting"></a>Einführung in die Problembehandlung  
Problembehandlung bei der RID-Ausstellung erfordert ein logisches und lineares vorgehen. Es sei denn, Sie die Ereignisprotokolle sorgfältig auf RID-bezogene Warnungen und Fehler überwachen, werden als Erstes ein Problem wahrscheinlich Fehler bei der kontoerstellung bemerken. Die Taste, um die Problembehandlung bei der RID-Ausstellung ist, zu verstehen, wenn das Symptom oder nicht erwartet wird. Viele RID-Ausstellung Probleme möglicherweise wirken sich nur einen Domänencontroller und haben nichts mit zu tun. Diese einfache Diagramm erleichtert Ihnen, diese Entscheidungen:  
  
![RID-Ausstellung](media/Managing-RID-Issuance/adds_rid_issuance_troubleshooting.png)  
  
### <a name="troubleshooting-options"></a>Optionen für die Problembehandlung  
  
#### <a name="logging-options"></a>Optionen für die Protokollierung  
Alle Protokolleinträge bei der RID-Ausstellung tritt in das Systemereignisprotokoll unter Verzeichnisdienste-SAM-Quelle. Protokollierung aktiviert und standardmäßig für maximale Ausführlichkeit konfiguriert. Wenn keine Einträge für die neuen komponentenänderungen in Windows Server 2012 angemeldet sind, behandeln Sie das Problem als Klassisches (Legacy-, vor Windows Server 2012) RID-Ausstellung Problem, das in Windows 2008 R2 oder älteren Betriebssystemen.  
  
#### <a name="utilities-and-commands-for-troubleshooting"></a>Hilfsprogramme und Befehle für die Problembehandlung  
Verwenden Sie zum Beheben von Problemen, die nicht durch Protokolle erklärt werden oben genannten - insbesondere ältere RID-Ausstellung Probleme – die folgende Liste der Tools als Ausgangspunkt verwendet:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Netzwerkmonitor 3.4  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>Allgemeine Methodik zur Problembehandlung bei der Konfiguration des Domänencontrollers  
  
1.  Ist der Fehler durch eine einfache Berechtigungen oder Domain Controller Verfügbarkeitsproblem?  
  
    1.  Versuchen Sie, ein Sicherheitsprinzipal ohne die erforderlichen Berechtigungen erstellen? Überprüfen Sie die Ausgabe für den Zugriff verweigert.  
  
    2.  Ist ein Domänencontroller verfügbar? Überprüfen Sie die zurückgegebenen Fehler sowie LDAP- und Domänencontroller-verfügbarkeitsnachrichten.  
  
2.  Ist der zurückgegebene Fehler einzelne RIDs und ist spezifisch genug, um Sie als Richtschnur verwenden? Wenn dies der Fall ist, folgen Sie den Anweisungen.  
  
3.  RIDs der zurückgegebene Fehler einzelne, aber ist ansonsten unspezifisch? Z. B. "kann Windows das Objekt erstellen, da der Verzeichnisdienst kann keinen relativen Bezeichner zuweisen."  
  
    1.  Überprüfen Sie das Systemereignisprotokoll auf dem Domänencontroller "Legacy-" (vor Windows Server 2012) RID-Ereignisse in beschriebenen [RID-Pool-Anfrage](https://technet.microsoft.com/en-us/library/ee406152(WS.10).aspx) (16642, 16643, 16644, 16645, 16656).  
  
    2.  Untersuchen Sie das Systemereignis auf dem Domänencontroller und RID-Master für den neuen Block beschriebenen Ereignisse unten in diesem Thema (16655, 16656, 16657).  
  
    3.  Überprüfen von Active Directory-Replikationsintegrität mit Repadmin.exe und RID-Master-Verfügbarkeit mit **Dcdiag.exe/Test: RidManager/v**. Aktivieren Sie doppelte netzwerkerfassungen zwischen Domänencontroller und der RID-Master, wenn diese Tests nicht eindeutig sind.  
  
### <a name="troubleshooting-specific-problems"></a>Problembehandlung bei bestimmten Problemen  
Die folgenden neuen Nachrichten melden Sie sich das Systemereignisprotokoll auf Windows Server 2012-Domänencontrollern. Automatische sollten AD tracking-Systeme, z. B. System Center Operations Manager für diese Ereignisse überwachen; alle wesentlichen sind, und einige Indikatoren für kritische domänenbezogene Probleme sind.  
  
|||  
|-|-|  
|Ereignis-ID|16653|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Warnung|  
|Nachricht|Eine Poolgröße für Kontobezeichner (RIDs), die von einem Administrator konfiguriert wurde, ist größer als das unterstützte Maximum. Wenn der Domänencontroller der RID-Master ist, wird der maximale Wert für %1 verwendet werden.<br /><br />Weitere Informationen finden Sie unter [RID-Blockgröße](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_RIDBlockMaxSize).|  
|Hinweise und Lösungen|Der maximale Wert für die RID-Blockgröße ist nun 15.000 dezimal (3A98 hexadezimal). Ein Domänencontroller kann nicht mehr als 15.000 RIDs anfordern. Dieses Ereignis protokolliert bei jedem Neustart, bis der Wert festgelegt wird, auf einen Wert auf das Maximum oder darunter.|  
  
|||  
|-|-|  
|Ereignis-ID|16654|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Information|  
|Nachricht|Ein Pool aus kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in den folgenden zu erwartenden Fällen auftreten:<br /><br />1. ein Domänencontroller ist von einer Sicherung wiederhergestellt.<br /><br />2. ein Domänencontroller, die auf einem virtuellen Computer wird aus einer Momentaufnahme wiederhergestellt.<br /><br />3. ein Administrator hat den Pool manuell ungültig gemacht.<br /><br />Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=226247 Weitere Informationen.|  
|Hinweise und Lösungen|Wenn dieses Ereignis unerwartet ist, wenden Sie sich an alle Domänenadministratoren und bestimmen Sie, welche die Aktion ausgeführt. Das Verzeichnisdienst-Ereignisprotokoll enthält auch weitere Informationen auf, wenn einer der folgenden Schritte ausgeführt wurde.|  
  
|||  
|-|-|  
|Ereignis-ID|16655|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Information|  
|Nachricht|Das globale Maximum für Kontobezeichner (RIDs) wurde auf %1 erhöht.|  
|Hinweise und Lösungen|Wenn dieses Ereignis unerwartet ist, wenden Sie sich an alle Domänenadministratoren und bestimmen Sie, welche die Aktion ausgeführt. Dieses Ereignis deutet auf die Erhöhung der die RID-pool jenseits der Standardgrenze von 2<sup>30</sup>und tritt nicht automatisch; nur durch eine Verwaltungsaktion.|  
  
|||  
|-|-|  
|Ereignis-ID|16656|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Warnung|  
|Nachricht|Das globale Maximum für Kontobezeichner (RIDs) wurde auf %1 erhöht.|  
|Hinweise und Lösungen|Aktion erforderlich! Ein Kontenidentifizierungspool (RIDS) wurde auf diesen Domänencontroller zugeordnet. Der Pool gibt an, dass diese Domäne einen erheblichen Teil der insgesamt verfügbaren Konto-IDs genutzt hat.<br /><br />Ein Schutzmechanismus wird aktiviert, wenn die Domäne den insgesamt verfügbaren Kontobezeichner verbleiben folgenden Schwellenwert erreicht: %1.  Der Schutzmechanismus verhindert die kontoerstellung, bis Sie kontobezeichnern auf dem RID-master-Domänencontroller manuell erneut aktivieren.<br /><br />Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228610 Weitere Informationen.|  
  
|||  
|-|-|  
|Ereignis-ID|16657|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Fehler|  
|Nachricht|Aktion erforderlich! Diese Domäne hat einen erheblichen Teil der insgesamt verfügbaren Kontobezeichner (RIDs) verbraucht. Ein Schutzmechanismus wurde aktiviert, weil der insgesamt verfügbaren Kontobezeichner verbleiben ist weniger als: X% [künstliche Obergrenze].<br /><br />Der Schutzmechanismus verhindert die kontoerstellung, bis Sie kontobezeichnern auf dem RID-master-Domänencontroller manuell erneut aktivieren.<br /><br />Es ist äußerst wichtig, dass bestimmte Diagnosemaßnahmen durchgeführt werden, vor der erneuten Aktivierung Konto erstellen, um sicherzustellen, dass diese Domäne nicht nur eine ungewöhnlich hohe Geschwindigkeit in Anspruch nimmt. Alle identifizierten Probleme sollten vor der erneuten Aktivierung der kontoerstellung behoben werden.<br /><br />Fehler beim Diagnostizieren und beheben ein Verbrauch der RIDs führen kann zu Erschöpfung der RIDs der Domäne führen nach der kontoerstellung dauerhaft in dieser Domäne deaktiviert ist.<br /><br />Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228610 Weitere Informationen.|  
|Hinweise und Lösungen|Kontaktieren Sie alle Domänenadministratoren und informiert, dass keine weiteren Sicherheitsprinzipale in dieser Domäne erstellt werden können, bis dieser Schutz außer Kraft gesetzt wird. Weitere Informationen zum Außerkraftsetzen des Schutzes und zur Vergrößerung der gesamten RID-pool, finden Sie unter [globalen RID-Speicherplatz freischalten](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_GlobalRidSpaceUnlock).|  
  
|||  
|-|-|  
|Ereignis-ID|16658|  
|Quelle|Verzeichnisdienste-SAM|  
|Schweregrad|Warnung|  
|Nachricht|Dieses Ereignis ist eine regelmäßige Aktualisierung der Anzahl von verbliebenen verfügbaren Kontobezeichner (RIDs). Die Anzahl von verbliebenen kontobezeichnern beträgt ungefähr: %1.<br /><br />Konto-IDs werden verwendet, wenn Konten erstellt werden, wenn sie leer ist, keine neuen Konten in der Domäne erstellt werden können.<br /><br />Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228745 Weitere Informationen.|  
|Hinweise und Lösungen|Kontaktieren Sie alle Domänenadministratoren und informiert, dass der RID-Verbrauch einen wichtigen Meilenstein überschritten hat. Bestimmen Sie, wenn dieses Verhalten zu erwarten ist oder nicht anhand der Sicherheit Vertrauensnehmer Erstellung Muster. Um dieses Ereignis ist sehr ungewöhnlich, da bedeutet dies, dass die mindestens ~ 100 Millionen RIDs verbraucht wurden.|  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten der RID-Ausstellung in WindowsServer 2012](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)  
  


