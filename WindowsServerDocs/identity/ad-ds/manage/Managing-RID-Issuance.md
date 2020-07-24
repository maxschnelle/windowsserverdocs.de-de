---
ms.assetid: aac117a7-aa7a-4322-96ae-e3cc22ada036
title: Verwalten der RID-Ausstellung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 065ef1af6d125b0c78669c11ffa28d7e4c9632d8
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966332"
---
# <a name="managing-rid-issuance"></a>Verwalten der RID-Ausstellung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel behandelt die Änderungen an der RID-Master FSMO-Rolle, inklusive der neuen Ausstellungs- und Überwachungsfunktionen im RID-Master sowie Analyse und Problembehandlung bei der RID-Ausstellung.  
  
-   [Verwalten der RID-Ausstellung](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Manage)  
  
-   [Problembehandlung bei der RID-Ausstellung](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Tshoot)  
  
Weitere Informationen finden Sie im [askds-Blog](/archive/blogs/askds/managing-rid-issuance-in-windows-server-2012).  
  
## <a name="managing-rid-issuance"></a><a name="BKMK_Manage"></a>Verwalten der RID-Ausstellung  
Standardmäßig bietet eine Domäne Kapazität für ca. eine Milliarde Sicherheitsprinzipale wie z. B. Benutzer, Gruppen und Computer. Natürlich gibt es keine Domänen mit so vielen aktiv genutzten Objekten. Der Microsoft-Kundensupport hat jedoch Fälle gefunden, in denen:  
  
-   Bereitstellungs-Software oder Verwaltungsskripts versehentlich massenweise Benutzer, Gruppen und Computer erstellt haben.  
  
-   Delegierte Benutzer viele nicht genutzte Sicherheits- und Verteilergruppen erstellt haben  
  
-   Viele Domänencontroller herabgestuft, wiederhergestellt oder deren Metadaten bereinigt wurden  
  
-   Gesamtstruktur-Wiederherstellungen durchgeführt wurden  
  
-   Die InvalidateRidPool-Operation häufig durchgeführt wurde  
  
-   Der Registrierungswert für die RID-Blockgröße falsch erhöht wurde  
  
All diese Situationen verbrauchen unnötig viele RIDs, oft aus Versehen. Über die Jahre sind in einigen Umgebungen die RIDs ausgegangen, wodurch eine Migration in eine neue Domäne oder Wiederherstellungen der Gesamtstruktur erforderlich wurden.  
  
Windows Server 2012 behandelt einige Probleme mit der RID-Ausstellung, die erst mit dem Alter und der Allgegenwärtigkeit von Active Directory aufgetreten sind. Hierzu gehören bessere Ereignisprotokollierung, geeignetere Grenzwerte und die Möglichkeit, im Notfall die Gesamtgröße des globalen RID-Speicherplatzes für eine Domäne zu verdoppeln.  
  
### <a name="periodic-consumption-warnings"></a>Regelmäßige Verbrauchswarnungen  
Windows Server 2012 überwacht globale RID-Ereignisse und liefert frühzeitige Warnungen, wenn wichtige Meilensteine überschritten werden. Das Modell berechnet die Verbrauchsgrenze von zehn (10) Prozent des globalen Pools und protokolliert ein Ereignis, wenn die Grenze erreicht wird. Anschließend werden die nächsten zehn Prozent des verbleibenden Pools berechnet, und der Ereigniszyklus wird fortgesetzt. Wenn der globale RID-Raum erschöpft wird, häufen sich die Ereignisse, da die zehn Prozent in einem abnehmenden Pool schneller erreicht werden (die Ereignisprotokoll-Dämpfung verhindert jedoch mehr als einen Eintrag pro Stunde). Das Systemereignis-Protokoll auf jedem Domänencontroller schreibt ein Verzeichnisdienst-SAM-Ereignis 16658.  
  
Ausgehend von einem globalen RID-Raum mit 30 Bit wird das erste Ereignis bei der Zuweisung des Pools protokolliert, der die RID Nummer 107.374.182 enthält.<sup></sup> Die Ereignisse beschleunigen auf natürliche Weise bis zum letzten Checkpoint von 100.000, mit insgesamt 110 generierten Ereignissen. Das Verhalten für einen freigeschalteten globalen RID-Raum mit 31 Bit ist ähnlich: beginnend mit 214.748.365 und insgesamt 117 Ereignissen.  
  
> [!IMPORTANT]  
> Dieses Ereignis ist nicht zu erwarten. Prüfen Sie die Erstellungsprozesse für Benutzer, Gruppen und Computer in der Domäne unverzüglich. Es ist sehr ungewöhnlich, dass über 100 Millionen AD DS-Objekte erstellt werden.  
  
![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_EventWaypoints2.png)  
  
### <a name="rid-pool-invalidation-events"></a>RID-Pool-Ungültigmachung  
Neue Ereigniswarnungen weisen darauf hin, dass ein lokaler RID-Pool eines DC gelöscht wurde. Diese Warnungen haben Informationscharakter und sind möglicherweise zu erwarten, insbesondere aufgrund der neuen VDC-Funktionen. Die folgende Ereignisliste enthält weitere Details zum Ereignis.  
  
### <a name="rid-block-size-limit"></a><a name="BKMK_RIDBlockMaxSize"></a>Größenbeschränkungen der RID-Blockgröße  
Normalerweise fragen Domänencontroller RID-Zuweisungen in Blöcken zu jeweils 500 RIDs an. Sie können diesen Standardwert über den folgenden REG_DWORD-Wert auf einem Domänencontroller überschreiben:  
  
```  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\RID Values  
RID Block Size  
  
```  
  
Vor Windows Server 2012 gab es keine Obergrenze für diesen Registrierungsschlüssel, abgesehen von der impliziten DWORD-Obergrenze (mit einem Wert von 0xffffffff oder 4294967295). Dieser Wert liegt deutlich oberhalb des globalen RID-Gesamtraums. Manche Administratoren haben die RID-Blockgröße versehentlich oder in Unkenntnis auf Werte gesetzt, mit denen die globalen RIDs rasant erschöpft wurden.  
  
In Windows Server 2012 kann dieser Wert nicht höher als 15.000 dezimal (0x3A98 hexadezimal) gesetzt werden. Damit wird die massenhafte unbeabsichtigte RID-Zuweisung verhindert.  
  
Wenn Sie den Wert *höher* als 15.000 setzen, wird dieser als 15.000 behandelt, und der Domänencontroller protokolliert das Ereignis 16653 im Verzeichnisdienste-Ereignisprotokoll bei jedem Neustart, bis der Wert korrigiert wird.  
  
### <a name="global-rid-space-size-unlock"></a><a name="BKMK_GlobalRidSpaceUnlock"></a>Freischalten des globalen RID-Raums  
Vor Windows Server 2012 war der globale RID-Raum auf 2<sup>30</sup> (bzw. 1.073.741.823) RIDs begrenzt. Ab dem Erreichen dieses Werts konnten neue RIDs nur noch nach einer Domänenmigration oder einer Wiederherstellung der Gesamtstruktur auf einen früheren Zeitpunkt ausgegeben werden - in jedem Fall eine Notfallwiederherstellung. Ab Windows Server 2012 kann das Bit 2<sup>31</sup> freigeschaltet werden, um den globalen Pool auf 2.147.483.648 RIDs zu vergrößern.  
  
AD DS speichert diese Einstellung in einem versteckten Attribut mit dem Namen **SidCompatibilityVersion** im RootDSE-Kontext aller Domänencontroller. Dieses Attribut kann mit ADSIEdit, LDP oder anderen Tools nicht ausgelesen werden. Um den globalen RID-Raum zu vergrößern, können Sie im Systemereignisprotokoll nach dem Warnungsereignis 16655 von Verzeichnisdienst-SAM suchen oder den folgenden Dcdiag-Befehl verwenden:  
  
```  
Dcdiag.exe /TEST:RidManager /v | find /i "Available RID Pool for the Domain"  
  
```  
  
Wenn Sie den globalen RID-Pool vergrößern, wächst dieser vom Standardwert 1.073.741.823 auf 2.147.483.647. Beispiel:  
  
![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_Dcdiag.png)  
  
> [!WARNING]  
> Diese Freischaltung ist *ausschließlich* dazu gedacht, eine Erschöpfung der RIDs zu verhindern und darf *ausschließlich* in Verbindung mit RID-Obergrenzenerzwingung (siehe nächster Abschnitt) eingesetzt werden. Verwenden Sie dies niemals "vorsorglich" in Umgebungen mit Millionen freier RIDs und geringem Wachstum, da RIDs aus dem freigeschalteten RID-Pool Probleme bzgl. der Anwendungskompatibilität verursachen können.  
>   
> Diese Freischaltung kann nur durch eine komplette Wiederherstellung der Gesamtstruktur auf einen früheren Zeitpunkt rückgängig gemacht oder entfernt werden.  
  
#### <a name="important-caveats"></a>Wichtige Einschränkungen  
Domänencontroller unter Windows Server 2003 und Windows Server 2008 können keine RIDs ausstellen, wenn das 31. Bit im globalen RID-Pool freigeschaltet ist.<sup></sup> Windows Server 2008 R2-Domänen Controller *können* 31<sup>.</sup> Bit-RIDs verwenden, *aber nur, wenn* auf Ihnen Hotfix [KB 2642658](https://support.microsoft.com/kb/2642658) installiert ist. Nicht unterstützte und nicht gepatchte Domänencontroller behandeln den globalen RID-Pool als erschöpft, wenn dieser freigeschaltet wurde.  
  
Dieses Feature wird von keiner Domänenfunktionsebene erzwungen. Achten Sie unbedingt darauf, dass die Domäne nur Domänencontroller unter Windows Server 2012 oder Windows Server 2008 R2 mit Hotfix enthält.  
  
#### <a name="implementing-unlocked-global-rid-space"></a>Freischalten des globalen RID-Raums  
Führen Sie die folgenden Schritte durch, um das 31. Bit im globalen RID-Pool freizuschalten, nachdem Sie die RID-Grenzwertwarnung (siehe unten) erhalten haben:<sup></sup>  
  
1.  Stellen Sie sicher, dass die RID-Masterrolle auf einem Windows Server 2012-Domänencontroller läuft. Übertragen Sie diese Rolle andernfalls auf einen Windows Server 2012-Domänencontroller.  
  
2.  Führen Sie LDP.exe aus  
  
3.  Klicken Sie im Menü **Verbindung** auf **Verbinden** für den Windows Server 2012 RID-Master auf Port 389 und anschließend als Domänenadministrator auf **Binden**.  
  
4.  Klicken Sie im Menü **Durchsuchen** auf **Ändern**.  
  
5.  Stellen Sie sicher, dass **DN** leer ist.  
  
6.  Geben Sie unter **Attributeingabe bearbeiten** Folgendes ein:  
  
    ```  
    SidCompatibilityVersion  
    ```  
  
7.  Geben Sie unter **Werte** Folgendes ein:  
  
    ```  
    1  
    ```  
  
8.  Stellen Sie sicher, dass **Hinzufügen** unter **Operation** ausgewählt ist und klicken Sie auf **Eingabe**. Daraufhin wird die **Eintragsliste** aktualisiert.  
  
9. Wählen Sie die Optionen **Synchron** und **Erweitert** aus und klicken Sie auf **Ausführen**.  
  
    ![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModify.png)  
  
10. Im Erfolgsfall wird im LDP-Ausgabefenster Folgendes angezeigt:  
  
    ```  
    ***Call Modify...  
     ldap_modify_ext_s(Id, '(null)',[1] attrs, SvrCtrls, ClntCtrls);  
    modified "".  
  
    ```  
  
    ![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModifySuccess.png)  
  
11. Suchen Sie im Systemereignisprotokoll auf diesem Domänencontroller nach dem Verzeichnisdienste-SAM-Informationsereignis 16655, um zu bestätigen, dass der globale RID-Pool vergrößert wurde.  
  
### <a name="rid-ceiling-enforcement"></a>RID-Obergrenzenerzwingung  
Windows Server 2012 verwendet eine künstliche Obergrenze für den globalen RID-Raum bei zehn (10) Prozent der verbleibenden RIDs im globalen Raum. Dies dient als Schutzmaßnahme bei der Domänenverwaltung. Wenn nur noch ein (1) Prozent der künstlichen Obergrenze verbleiben, schreiben Domänencontroller beim Anfragen von RID-Pools ein Verzeichnisdienste-SAM-Warnungsereignis 16656 in deren Systemereignisprotokoll. Beim Erreichen der Obergrenze von zehn Prozent im RID-Master-FSMO, schreibt dieser das Verzeichnisdienste-SAM-Ereignis 16657 in dessen Systemereignisprotokoll und gibt erst wieder neue RID-Pools aus, wenn die Obergrenze außer Kraft gesetzt wurde. Dies zwingt Sie dazu, den Zustand des RID-Masters in der Domäne zu prüfen und mögliche Probleme bei der RID-Zuweisung zu beheben. Außerdem wird Ihre Domäne davor geschützt, den gesamten RID-Raum zu erschöpfen.  
  
Dieser Grenzwert ist hartcodiert bei verbleibenden zehn Prozent des verfügbaren RID-Raums. Die Obergrenze tritt also in Kraft, wenn der RID-Master einen Pool zuweist, der die RID enthält, die neunzig (90) Prozent des globalen RID-Raums entspricht.  
  
-   Für Standarddomänen liegt der erste Auslöser bei 2<sup>30</sup>-1 * 0,90 = 966.367.640 (bzw. 107.374.183 verbleibenden RIDs).  
  
-   Für Domänen mit freigeschaltetem 31-Bit-RID-Raum liegt der Auslöser bei 2<sup>31</sup>-1 * 0,90 = 1.932.735.282 (bzw. 214.748.365 verbleibenden RIDs).  
  
Beim Auslösen setzt der RID-Master das Active Directory-Attribut **msDS-RIDPoolAllocationEnabled** (allgemeiner Name **ms-DS-RID-Pool-Allocation-Enabled**) für das Objekt auf FALSE:  
  
CN = RID Manager $, CN = System, DC =*<domain>*  
  
Das Ereignis 16657 wird geschrieben und verhindert die weitere Ausstellung von RID-Blocks auf allen Domänencontrollern. Die Domänencontroller verbrauchen weiterhin alle bislang ausgestellten RID-Pools.  
  
Setzen Sie diesen Wert auf TRUE, um die Sperre zu entfernen und die Zuweisung der RID-Pools fortzusetzen. Bei der nächsten RID-Zuweisung durch den RID-Master kehrt das Attribut auf seinen Standardwert NOT SET zurück. Anschließend existieren keine weiteren Obergrenzen mehr und der globale RID-Raum wird irgendwann erschöpft, und eine Gesamtstruktur-Wiederherstellung oder Domänenmigration ist erforderlich.  
  
#### <a name="removing-the-ceiling-block"></a>Entfernen der Obergrenzensperre  
Führen Sie die folgenden Schritte durch, um die Sperre nach dem Erreichen der künstlichen Obergrenze zu entferen:  
  
1.  Stellen Sie sicher, dass die RID-Masterrolle auf einem Windows Server 2012-Domänencontroller läuft. Übertragen Sie diese Rolle andernfalls auf einen Windows Server 2012-Domänencontroller.  
  
2.  Führen Sie LDP.exe aus.  
  
3.  Klicken Sie im Menü **Verbindung** auf *Verbinden* für den Windows Server 2012 RID-Master auf Port 389 und anschließend als Domänenadministrator auf **Binden**.  
  
4.  Klicken Sie im Menü **Ansicht** auf **Gesamtstruktur**, und wählen Sie den Domänen-Namenskontext des RID-Masters für die **Basis-DN** aus. Klicken Sie auf **OK**.  
  
5.  Öffnen Sie den Container **CN=System** im Navigationsbereich und klicken Sie auf das Objekt **CN=RID Manager$**. Klicken Sie mit der rechten Maustaste auf das Objekt und klicken Sie auf **Ändern**.  
  
6.  Geben Sie unter Attributeingabe bearbeiten Folgendes ein:  
  
    ```  
    MsDS-RidPoolAllocationEnabled  
    ```  
  
7.  Geben Sie unter **Werte** Folgendes ein (in Großbuchstaben):  
  
    ```  
    TRUE  
    ```  
  
8.  Wählen Sie **Ersetzen** unter **Operation** aus und klicken Sie auf **Eingabe**. Daraufhin wird die **Eintragsliste** aktualisiert.  
  
9. Aktivieren Sie die Optionen **Synchron** und **Erweitert** und klicken Sie auf **Ausführen**:  
  
    ![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeiling.png)  
  
10. Im Erfolgsfall wird im LDP-Ausgabefenster Folgendes angezeigt:  
  
    ```  
    ***Call Modify...  
    ldap_modify_ext_s(ld, 'CN=RID Manager$,CN=System,DC=<domain>',[1] attrs, SvrCtrls, ClntCtrls);  
    Modified "CN=RID Manager$,CN=System,DC=<domain>".  
  
    ```  
  
    ![Rid-Ausstellung](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeilingSuccess.png)  
  
### <a name="other-rid-fixes"></a>Sonstige RID-Korrekturen  
Ältere Windows Server-Versionen hatten ein Verlustproblem im RID-Pool, wenn das rIDSetReferences-Attribut gefehlt hat. Um dieses Problem auf Domänen Controllern, auf denen Windows Server 2008 R2 ausgeführt wird, zu beheben, installieren Sie den Hotfix aus [KB 2618669](https://support.microsoft.com/kb/2618669).  
  
### <a name="unfixed-rid-issues"></a>Nicht korrigierte RID-Probleme  
Wenn die Kontoerstellung fehlschlägt, existiert ein weiteres RID-Verlustproblem. Wenn die Kontoerstellung fehlschlägt, wird dennoch eine RID verbraucht. Ein gängiges Beispiel ist die Erstellung von Benutzern, deren Kennwort die Komplexitätsanforderungen nicht erfüllt.  
  
### <a name="rid-fixes-for-earlier-versions-of-windows-server"></a>RID-Korrekturen für ältere Windows Server-Versionen  
Für alle der oben genannten Korrekturen und Änderungen existieren Hotfixes für Windows Server 2008 R2. Aktuell sind keine Windows Server 2008-Hotfixes geplant oder in Arbeit.  
  
## <a name="troubleshooting-rid-issuance"></a><a name="BKMK_Tshoot"></a>Problembehandlung bei der RID-Ausstellung  
  
### <a name="introduction-to-troubleshooting"></a>Einführung in die Problembehandlung  
Die Problembehandlung bei der RID-Ausstellung erfordert ein logisches und lineares Vorgehen. Sofern Sie Ihre Ereignisprotokolle nicht sorgfältig auf RID-bezogene Warnungen und Fehler überwachen, werden Sie als erstes Problem Fehler bei der Kontoerstellung bemerken. Für die Problembehandlung bei der RID-Ausstellung müssen Sie zunächst verstehen, welche Symptome zu erwarten sind. Manche Probleme bei der RID-Ausstellung betreffen nur einen Domänencontroller und haben nichts mit den Komponentenverbesserungen zu tun. Das folgende einfache Diagramm erleichtert Ihnen diese Entscheidungen:  
  
![Rid-Ausstellung](media/Managing-RID-Issuance/adds_rid_issuance_troubleshooting.png)  
  
### <a name="troubleshooting-options"></a>Optionen zur Problembehebung  
  
#### <a name="logging-options"></a>Protokollierungsoptionen  
Alle Protokolleinträge bei der RID-Ausstellung werden unter Verzeichnisdienste-SAM in das Systemereignisprotokoll geschrieben. Die Protokollierung ist standardmäßig aktiviert und für maximale Ausführlichkeit konfiguriert. Wenn keine Einträge für die neuen Komponentenänderungen in Windows Server 2012 protokolliert werden, sollten Sie das Problem als klassisches (Legacy-, vor Windows Server 2012) RID-Ausstellungsproblem behandeln, das in Windows Server 2008 R2 oder älteren Betriebssystemen auftritt.  
  
#### <a name="utilities-and-commands-for-troubleshooting"></a>Hilfsprogramme und Befehle für die Problembehandlung  
Die folgenden Tools dienen als Ausgangspunkt bei der Behandlung von Problemen, die nicht durch die genannten Protokolle erklärt werden können, insbesondere ältere RID-Ausstellungsprobleme:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Network Monitor 3.4  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>Allgemeine Methoden für die Problembehandlung bei der Domänencontroller-Konfiguration  
  
1.  Wurde der Fehler durch ein einfaches Berechtigungs- oder Verfügbarkeitsproblem eines Domänencontrollers verursacht?  
  
    1.  Haben Sie versucht, ein Sicherheitsprinzipal ohne die erforderlichen Berechtigungen zu erstellen? Untersuchen Sie die Ausgabe auf "Zugriff verweigert"-Fehler.  
  
    2.  Ist ein Domänencontroller verfügbar? Untersuchen Sie den zurückgegebenen Fehler sowie LDAP- und Domänencontroller-Verfügbarkeitsnachrichten.  
  
2.  Enthält der zurückgegebene Fehler einzelne RIDs bzw. ist er spezifisch genug, um als Hinweis zu dienen? Wenn ja, folgen Sie diesen Hinweisen.  
  
3.  Enthält der zurückgegebene Fehler einzelne RIDs, ist aber ansonsten eher unspezifisch? Zum Beispiel: "Windows kann das Objekt nicht erstellen, da es dem Verzeichnis-Dienst nicht möglich war, einen relativen Bezeichner zuzuweisen."  
  
    1.  Überprüfen Sie das System Ereignisprotokoll auf dem Domänen Controller auf "Legacy" (Pre-Windows Server 2012) Rid-Ereignisse, die in der [RID-Pool-Anforderung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee406152(v=ws.10)) (16642, 16643, 16644, 16645, 16656) ausführlich aufgeführt sind.  
  
    2.  Untersuchen Sie die Systemereignisse des Domänencontrollers und des RID-Masters auf die weiter unten in diesem Artikel beschriebenen Ereignisse, die auf neu erstellte Blocks hindeuten (16655, 16656, 16657).  
  
    3.  Prüfen Sie die Active Directory-Replikationsintegrität mit Repadmin.exe und die Verfügbarkeit des RID-Masters mit **Dcdiag.exe /test:ridmanager /v**. Führen Sie beidseitige Netzwerkerfassungen zwischen Domänencontroller und RID-Master durch, falls diese Tests nicht eindeutig ausfallen.  
  
### <a name="troubleshooting-specific-problems"></a>Beheben von bestimmten Problemen  
Die folgenden neuen Nachrichten werden in das Systemereignisprotokoll in Windows Server 2012-Domänencontrollern geschrieben. Automatische AD-Integritätsüberwachungssysteme wie System Center Operations Manager sollten diese Ereignisse überwachen, die allesamt wichtig sind und teilweise auf kritische Probleme in der Domäne hinweisen.  
  
|||  
|-|-|  
|Ereignis-ID|16653|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Warnung|  
|`Message`|Eine Poolgröße für Kontobezeichner (RIDs), die ein Administrator konfiguriert hat, übersteigt das unterstützte Maximum. Der maximale Wert "%1" wird verwendet, wenn der Domänencontroller der RID-Master ist.<p>Weitere Informationen finden Sie unter [Größenbeschränkungen der RID-Blockgröße](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_RIDBlockMaxSize).|  
|Hinweise und Lösung|Der maximale Wert für die RID-Blockgröße ist nun 15.000 dezimal (3A98 hexadezimal). Domänencontroller können nicht mehr als 15.000 RIDs anfordern. Dieses Ereignis wird bei jedem Neustart protokolliert, bis der Wert auf das Maximum oder darunter gesetzt wurde.|  
  
|||  
|-|-|  
|Ereignis-ID|16654|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Informational|  
|`Message`|Ein Pool aus Kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in folgenden erwarteten Fällen vorkommen:<p>1. ein Domänen Controller wird aus der Sicherung wieder hergestellt.<p>2. ein Domänen Controller, der auf einer virtuellen Maschine ausgeführt wird, wird aus einer Momentaufnahme wieder hergestellt<p>3. ein Administrator hat den Pool manuell ungültig gemacht.<p>Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=226247.|  
|Hinweise und Lösung|Wenn dieses Ereignis unerwartet auftritt, sollten Sie alle Domänenadministratoren kontaktieren und herausfinden, wer diese Aktion ausgeführt hat. Das Verzeichnisdienste-Ereignisprotokoll enthält außerdem weitere Informationen zum Zeitpunkt, zu dem einer dieser Schritte ausgeführt wurde.|  
  
|||  
|-|-|  
|Ereignis-ID|16655|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Informational|  
|`Message`|Das globale Maximum für Kontobezeichner (RIDs) wurde auf "%1" erhöht.|  
|Hinweise und Lösung|Wenn dieses Ereignis unerwartet auftritt, sollten Sie alle Domänenadministratoren kontaktieren und herausfinden, wer diese Aktion ausgeführt hat. Dieses Ereignis deutet auf die Erhöhung der Gesamtgröße des RID-Pools jenseits der Standardgrenze von 2<sup>30</sup> und tritt nicht automatisch auf, sondern nur durch Verwaltungsaktionen.|  
  
|||  
|-|-|  
|Ereignis-ID|16656|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Warnung|  
|`Message`|Das globale Maximum für Kontobezeichner (RIDs) wurde auf "%1" erhöht.|  
|Hinweise und Lösung|Es ist eine Aktion erforderlich! Diesem Domänencontroller wurde ein Pool aus Kontobezeichnern (RIDs) zugeordnet. Dem Poolwert ist zu entnehmen, dass diese Domäne einen erheblichen Teil der insgesamt verfügbaren Konto-IDs beansprucht.<p>Ein Schutzmechanismus wird aktiviert, wenn die Domäne den folgenden Schwellenwert der insgesamt verfügbaren Konto-IDs erreicht: %1.  Der Schutzmechanismus verhindert die Kontoerstellung, bis Sie die Zuweisung von Kontobezeichnern auf dem RID-Master-Domänencontroller manuell aktivieren.<p>Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228610.|  
  
|||  
|-|-|  
|Ereignis-ID|16657|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Fehler|  
|`Message`|Es ist eine Aktion erforderlich! In dieser Domäne ist ein erheblicher Teil der grundsätzlich verfügbaren Kontobezeichner (RIDs) vergeben. Ein Schutzmechanismus wurde aktiviert, weil die verfügbaren verfügbaren Konto-IDs kleiner als: X% [künstliche Ceiling-Argument] sind.<p>Der Schutzmechanismus verhindert die Kontoerstellung, bis Sie die Zuweisung von Kontobezeichnern auf dem RID-Master-Domänencontroller manuell aktivieren.<p>Vor der erneuten Aktivierung der Kontoerstellung müssen unbedingt bestimmte Diagnosemaßnahmen durchgeführt werden, um sicherzustellen, dass die RIDs der Domäne nicht übermäßig schnell verbraucht werden. Alle identifizierten Probleme sollten vor der erneuten Aktivierung der Kontoerstellung behoben werden.<p>Wenn die Probleme, die zum übermäßig schnellen Verbrauch der RIDs führen, nicht behoben werden, können die RIDs der Domäne erschöpft werden, was zur permanenten Deaktivierung der Kontoerstellung in der Domäne führt.<p>Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228610.|  
|Hinweise und Lösung|Kontaktieren Sie alle Domänenadministratoren und informieren Sie diese darüber, dass keine weiteren Sicherheitsprinzipale erstellt werden können, bis dieser Schutz außer Kraft gesetzt wird. Weitere Informationen zum Außerkraftsetzen des Schutzes und zur Vergrößerung des RID-Gesamtpools finden Sie unter [Freischalten des globalen RID-Raums](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_GlobalRidSpaceUnlock).|  
  
|||  
|-|-|  
|Ereignis-ID|16658|  
|`Source`|Verzeichnisdienst-SAM|  
|Schweregrad|Warnung|  
|`Message`|Dieses Ereignis ist eine regelmäßige Aktualisierung der Anzahl von verbliebenen verfügbaren Kontobezeichnern (RIDs). Die Anzahl der verbleibenden Konto Bezeichner beträgt ungefähr: %1.<p>Kontobezeichner werden verwendet, wenn Konten erstellt werden. Wenn keine Kontobezeichner mehr verfügbar sind, können in der Domäne keine neuen Konten mehr erstellt werden.<p>Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=228745.|  
|Hinweise und Lösung|Kontaktieren Sie alle Domänenadministratoren und informieren Sie diese darüber, dass der RID-Verbrauch einen wichtigen Meilenstein überschritten hat. Ermitteln Sie, ob dieses Verhalten zu erwarten ist, indem Sie die Erstellungsmuster für Objekte prüfen. Dieses Ereignis sollte nur in den seltensten Fällen auftreten und deutet darauf hin, dass mindestens ~100 Millionen RIDs verbraucht wurden.|  
  
## <a name="see-also"></a>Weitere Informationen  
[Verwalten der RID-Ausstellung in Windows Server 2012](/archive/blogs/askds/managing-rid-issuance-in-windows-server-2012)  
  
