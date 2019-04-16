---
ms.assetid: 5ab76733-804d-4f30-bee6-cb672ad5075a
title: "Problembehandlung bei der Bereitstellung von Domänencontrollern"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 254209b0da6a7bc0cd5f3880e14a7e5b16822cdd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshooting-domain-controller-deployment"></a>Problembehandlung bei der Bereitstellung von Domänencontrollern

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieser Artikel behandelt detaillierte Methoden für die Problembehandlung bei der Domänencontroller-Konfiguration und Bereitstellung.  
  
-   [Einführung in die Problembehandlung](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md#BKMK_Intro)  
  
-   [Optionen für die Problembehandlung](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md#BKMK_Options)  
  
## <a name="BKMK_Intro"></a>Einführung in die Problembehandlung  
![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/adds_deploy_troubleshooting.png)  
  
## <a name="BKMK_Options"></a>Optionen für die Problembehandlung  
  
### <a name="logging-options"></a>Optionen für die Protokollierung  
Die integrierten Protokolle sind das wichtigste Instrument zur Behandlung von Problemen mit der Domäne Domänencontroller herauf- und Herabstufung. Alle diese Protokolle sind aktiviert und wird standardmäßig für maximale Ausführlichkeit konfiguriert.  
  
|Phase|Protokoll|  
|---------|-------|  
|Server-Manager oder ADDSDeployment Windows PowerShell-Operationen|-%systemroot%\debug\dcpromoui.log<br /><br />-%systemroot%\debug\dcpromoui*.log|  
|Installation/heraufstufung des Domänencontrollers|-%systemroot%\debug\dcpromo.log<br /><br />-%systemroot%\debug\dcpromo*.log<br /><br />-Ereignis protokoll\system<br /><br />-Ereignisanzeige\windows-protokoll\anwendung Ereignis<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\verzeichnisdienst<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dateireplikationsdienst<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dfs-Replikation|  
|Upgrade von Gesamtstruktur oder Domäne|-%systemroot%\debug\adprep\\<datetime>\adprep.log<br /><br />-%systemroot%\debug\adprep\\<datetime>\csv.log<br /><br />-%systemroot%\debug\adprep\\<datetime>\dspecup.log<br /><br />-%systemroot%\debug\adprep\\<datetime>\ldif.log*|  
|Server-Manager ADDSDeployment Windows PowerShell Bereitstellungsmodul|-Ereignis ereignisanzeige\Anwendungs- und dienstprotokolle\microsoft\windows\verzeichnisdienste-bereitstellung\operational|  
|Für Windows|-%systemroot%\Logs\CBS\\*<br /><br />-%systemroot%\Servicing\sessions\sessions.xml<br /><br />-%systemroot%\winsxs\poqexec.log<br /><br />-%systemroot%\winsxs\pending.xml|  
  
### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Konfiguration des Domänencontrollers  
Verwenden Sie zum Beheben von Problemen, die nicht durch Protokolle erklärt werden die folgenden Tools als Ausgangspunkt verwendet:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   [AutoRuns.exe](https://technet.microsoft.com/sysinternals/bb963902.aspx), Task-Manager und MSInfo32.exe  
  
-   [Network Monitor 3.4](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=4865) (oder ein Drittanbieter Netzwerk erfassen und -Analyse-Tool)  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>Allgemeine Methodik zur Problembehandlung bei der Konfiguration des Domänencontrollers  
  
1.  Verursacht ein Problem mit einfachen Syntaxfehler?  
  
    1.  Sie falsch oder vergessen, ein Argument von ADDSDeployment Windows PowerShell bereitstellen? Beispielsweise, wenn Sie ADDSDeployment Windows PowerShell verwenden, haben Sie vergessen, benötigte Argument **- Domainname** mit einem gültigen Namen?  
  
    2.  Überprüfen Sie die Windows PowerShell-Konsolenausgabe sorgfältig, um genau, warum die eingegebene Befehlszeile analysiert.  
  
2.  Ist der Fehler eine erforderliche Fehler?  
  
    1.  Viele Fehler, die als schwerwiegender Promotion-Ergebnisse angezeigt werden jetzt von der voraussetzungsprüfung verhindert.  
  
    2.  Prüfen Sie den Text der voraussetzungsfehler sorgfältig vor, sie bieten Hinweise für die meisten Probleme zu lösen, kontrollierte Szenarien werden.  
  
3.  Liegt der Fehler bei der heraufstufung und somit nicht behebbar?  
  
    1.  Überprüfen Sie die Ergebnisse sorgfältig: viele Fehler haben einfache Ursachen wie z.B. falsche Kennwörter, Netzwerk-Namensauflösung oder kritische Offline-Domänencontroller.  
  
    2.  Überprüfen Sie die Dcpromoui.log und dcpromo.log für Fehler in der Ausgabe angezeigt dann funktionieren Abwärtskompatibilität von ihnen finden Sie unter Anzeichen dafür, warum der Fehler aufgetreten ist.  
  
        1.  Vergleichen Sie immer mit einem funktionierenden Beispielprotokoll  
  
        2.  Überprüfen Sie die ADPrep-Ereignisprotokolle auf Fehler, nur dann, wenn die Ergebnisse auf ein Problem bei der schemaerweiterung oder der Vorbereitung von Gesamtstruktur oder Domäne Hinweisen.  
  
        3.  Untersuchen Sie das Verzeichnisdienste-Bereitstellung-Ereignisprotokoll auf Fehler, nur dann, wenn die Dcpromoui.log Detail fehlen oder nach dem Zufallsprinzip aufgrund eines Ausnahmefehlers beim Konfigurationsprozess endet.  
  
    3.  Überprüfen Sie die Ereignisprotokolle Verzeichnisdienste, System und Anwendung nach weiteren Anzeichen für Konfigurationsprobleme. Oft ist das Heraufstufen von Domänencontrollern nur Symptome für andere Netzwerk-Fehlkonfigurationen, die alle verteilten Systeme betreffen würden.  
  
    4.  Verwenden Sie dcdiag.exe und repadmin.exe, überprüfen die Integrität der Gesamtstruktur und subtilen Fehlkonfigurationen zu suchen, die weitere heraufstufung des Domänencontrollers verhindern könnten.  
  
    5.  Verwenden Sie AutoRuns.exe, Task-Manager oder MSinfo32.exe, um den Computer für die Software von Drittanbietern zu überprüfen, die möglicherweise beeinträchtigen.  
  
        1.  Entfernen Sie die Software von Drittanbietern (einfach deaktivieren Sie nicht die Software, die Laden von Treibern nicht verhindert).  
  
    6.  Installieren Sie NetMon 3.4 auf dem Computer, der nicht als auch die Replikationspartner-Domänencontroller heraufstufen und analysieren den Heraufstufungsprozess mit zwei Spitzen Netzwerkaktivitäten.  
  
        1.  Vergleichen Sie dies, mit Ihrer laborumgebung zu wissen, was eine korrekte heraufstufung Aussehen und wo der Fehler liegt.  
  
        2.  An diesem Punkt Fehler sind wahrscheinlich mit Objekten der Gesamtstruktur, der nicht standardmäßigen sicherheitsänderungen oder im Netzwerk, und der neue Domänencontroller ist ein Opfer von Fehlkonfigurationen in DNS, Firewalls, Schutzsoftware oder sonstigen externen Faktoren.  
  
### <a name="troubleshooting-specific-problems"></a>Problembehandlung bei bestimmten Problemen  
  
#### <a name="events-and-error-messages"></a>Ereignis- und Fehlermeldungen  
Domäne Domänencontroller herauf- und Herabstufung immer zurückgegeben einen Code am Ende des Vorgangs und im Gegensatz zu den meisten Programmen NULL nicht für die erfolgreiche. Um den Code am Ende einer Domänencontroller-Konfiguration angezeigt wird, haben Sie mehrere Optionen:  
  
1.  Wenn Sie Server-Manager verwenden, wird das heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart eingefügt.  
  
2.  Wenn Sie ADDSDeployment Windows PowerShell verwenden, wird das heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart eingefügt. Sie können auch entscheiden Sie, keine Ausführung automatisch neu gestartet. Sie sollten hinzufügen, die **Format-List** Pipeline die Ausgabe übersichtlicher zu gestalten. Zum Beispiel:  
  
    ```  
    Install-addsdomaincontroller <options> -norebootoncompletion:$true | format-list  
  
    ```  
  
    Fehler bei der Prüfung der erforderlichen Komponenten und Überprüfung fahren bei einem Neustart Sie nicht damit sie stets sichtbar sind. Zum Beispiel:  
  
  ![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/ADDS_PSPrereqError.png)  
  
3.  Überprüfen Sie in jedem Szenario die dcpromo.log und dcpromoui.log.  
  
    > [!NOTE]  
    > Einige der unten aufgeführten Fehler sind nicht mehr möglich, da das Betriebssystem und Domain Controller Änderungen an der Konfiguration in späteren Betriebssystemen bereitgestellt. Der neue ADDSDeployment Windows PowerShell-Codes verhindert ebenfalls bestimmte Fehler, aber die dcpromo.exe//unattend nicht; Dies ist eine andere zwingender Grund für alle Ihre aktuelle Automatisierung vom veralteten DCPromo auf ADDSDeployment Windows PowerShell zu wechseln.  
  
Herauf- und Herabstufung von Rückgabecodes der folgenden Erfolg Nachricht.  
  
|Fehlercode:|Erläuterung|Hinweis:|  
|--------------|---------------|--------|  
|1|Ende, Erfolg|Dennoch muss neu gestartet, diese nur Notizen, dass die automatische Kennzeichen neu gestartet wurde entfernt.|  
|2|Ende, Erfolg, Neustart erforderlich||  
|3|Ende, Erfolg mit nicht-kritischem Fehler|In der Regel angezeigt, wenn der DNS-Delegierungswarnung zurückgegeben. Wenn keine DNS-Delegierung konfigurieren möchten, verwenden Sie:<br /><br />-Creatednsdelegation: $false|  
|4|Ende, Erfolg mit nicht-kritischem Fehler, Neustart erforderlich|In der Regel angezeigt, wenn der DNS-Delegierungswarnung zurückgegeben. Wenn keine DNS-Delegierung konfigurieren möchten, verwenden Sie:<br /><br />-Creatednsdelegation: $false|  
  
Herauf- und Herabstufung von Rückgabecodes der folgende Fehler angezeigt. Es ist auch eine erweiterte Fehlermeldung angezeigt werden. Lesen Sie immer die gesamte Fehlermeldung sorgfältig, nicht nur den numerischen Teil.  
  
|Fehlercode:|Erläuterung|Vorgeschlagene Lösung|  
|--------------|---------------|------------------------|  
|11|Domänencontroller-heraufstufung wird bereits ausgeführt.|Führen Sie nicht als eine Instanz des Domänencontroller-heraufstufung gleichzeitig für denselben Zielcomputer aus|  
|12|Benutzer muss Administrator sein.|Melden Sie sich als Mitglied der integrierten, die Administratoren gruppieren und stellen Sie sicher, dass Sie die Rechte mit UAC|  
|13|Zertifizierungsstelle ist installiert.|Sie können nicht diesen Domänencontroller tiefer stufen, wie sie auch eine Zertifizierungsstelle ist. Entfernen Sie die Zertifikate die Zertifizierungsstelle, bevor Sie dessen Nutzung sorgfältig, wenn es ausstellt, entfernen die Rolle bewirkt, dass einen Ausfall. Zertifizierungsstellen auf Domänencontrollern ausgeführt wird davon abgeraten|  
|14|Im abgesicherten Modus ausgeführt wird|Starten Sie den Server im normalen Modus|  
|15|Ändern einer Benutzerrolle wird oder muss neu gestartet werden|Starten Sie Server (aufgrund vorheriger Konfigurationsänderungen) vor der heraufstufung neu.|  
|16|Ausführung auf falscher Plattform|*Dieser Fehler nicht wahrscheinlich*|  
|17|Keine NTFS 5-Laufwerke vorhanden sein.|Dieser Fehler kann nicht in Windows Server2012, die mindestens der %SystemDrive% mit NTFS formatiert sein|  
|18|Nicht genügend Speicherplatz in "Windir"|Geben Sie Speicherplatz auf dem % Systemdrive % Volume mit cleanmgr.exe frei|  
|19|Name steht, muss neu gestartet werden|Starten Sie den Server|  
|20|Name des Computers ist Ungültige syntax|Benennen Sie den Computer mit einem gültigen Namen|  
|21|Dieser Domänencontroller enthält FSMO-Rollen, ist ein globaler Katalog und/oder ein DNS-Server|Hinzufügen **- Demoteoperationmasterrole** Verwendung **- Forceremoval**.|  
|22|TCP/IP muss installiert werden oder funktioniert nicht|Stellen Sie sicher, dass Computer TCP/IP konfiguriert, gebunden ist und korrekt funktioniert|  
|23|DNS-Client muss zunächst konfiguriert werden|Legen Sie einen primären DNS-Server, beim Hinzufügen eines neuen Domänencontrollers zu einer Domäne|  
|24|Eingegebene Anmeldeinformationen sind ungültig oder unvollständig|Überprüfen Sie Ihren Benutzernamen und Kennwort richtig ist.|  
|25|Domänencontroller für die angegebene Domäne konnte nicht gefunden werden.|Überprüfen von DNS-Clienteinstellungen und Firewallregeln|  
|26|Liste der Domänen konnte nicht aus der Gesamtstruktur gelesen werden|Überprüfen von DNS-Clienteinstellungen, LDAP-Funktionalität und Firewallregeln|  
|27|Fehlender Domänenname|Geben Sie eine Domäne bei herauf- und Herabstufung|  
|28|Ungültiger Domänenname|Wählen Sie einen anderen, gültigen DNS-Domänennamen beim Heraufstufen|  
|29|Übergeordnete Domäne existiert nicht|Beim Erstellen einer neuen untergeordneten Domäne oder Gesamtstrukturdomäne angegebene übergeordnete Domäne überprüfen|  
|30|Domäne nicht in der Gesamtstruktur|Überprüfen Sie den Domänennamen, sofern|  
|31|Untergeordnete Domäne existiert bereits|Geben Sie einen anderen Domänennamen an|  
|32|Ungültiger NetBIOS-Domänenname|Geben Sie einen gültigen NetBIOS-Domänennamen|  
|33|Pfad der IFM-Dateien ist ungültig|Prüfen Sie Ihren Pfad zum Install From Media-Ordner|  
|34|Die IFM-Datenbank ist ungültig|Verwenden Sie die korrekte Install From Media für dieses Betriebssystem und Rolle (gleiche Betriebssystem-Version, denselben Typ von Domänencontroller - RODC oder RWDC)|  
|35|Fehlende Systemschlüssel (Syskey)|Die Install from Media ist verschlüsselt, und geben Sie einen gültigen SYSKEY zur Verwendung|  
|37|Pfad für NTDS-Datenbank oder den zugehörigen Protokollen ist ungültig|Ändern Sie Pfad der Datenbank und Protokolle auf einem festen NTFS-Volume, nicht zugeordnetes Laufwerk oder UNC-Pfad|  
|38|Volume ist nicht genügend Speicherplatz für NTDS-Datenbank oder Protokolle verfügbar.|Freigeben von Speicherplatz mit cleanmgr.exe, mehr Speicherplatz hinzufügen, Speicherplatz manuell zu löschen, indem Sie nicht benötigte Daten an anderer Stelle verschieben|  
|39|Pfad für SYSVOL ist ungültig|Ändern der Pfad des Ordners "SYSVOL" auf einem festen NTFS-Volume, nicht zugeordnetes Laufwerk oder UNC-Pfad|  
|40|Ungültiger Sitename|Geben Sie einen, die vorhanden ist|  
|41|Geben Sie ein Kennwort für abgesicherten Modus müssen|Geben Sie ein Kennwort für das DSRM-Konto, es darf nicht leer, unabhängig davon, wie der Kennwortrichtlinie sein.|  
|42|Kennwort für abgesicherten Modus erfüllt nicht die Kriterien (nur heraufstufung)|Geben Sie ein Kennwort für das DSRM-Konto, das konfigurierten Regeln für die Kennwortrichtlinie erfüllt|  
|43|Admin-Kennwort erfüllt nicht die Kriterien (nur heraufstufung)|Geben Sie an, dass ein Kennwort für das lokale Administratorkonto an, das der Kennwortrichtlinie erfüllt Regeln konfiguriert.|  
|44|Der angegebene Name für die Gesamtstruktur ist ungültig|Geben Sie einen gültigen Gesamtstruktur Stamm-DNS-Domänennamen|  
|45|Eine Gesamtstruktur mit dem angegebenen Namen ist bereits vorhanden.|Wählen Sie einen anderen Gesamtstruktur Stamm-DNS-Domänennamen|  
|46|Der angegebene Name für die Struktur ist ungültig|Geben Sie einen gültigen Struktur DNS-Domänennamen|  
|47|Eine Struktur mit dem angegebenen Namen ist bereits vorhanden.|Wählen Sie einen andere Struktur DNS-Domänennamen|  
|48|Der Strukturname passt nicht in der Gesamtstruktur|Wählen Sie einen andere Struktur DNS-Domänennamen|  
|49|Die angegebene Domäne ist nicht vorhanden.|Überprüfen Sie den eingegebenen Domänennamen|  
|50|Bei der Herabstufung wurde letzter Domänencontroller entdeckt, auch wenn nicht, oder letzter Domänencontroller angegeben wurde, aber es nicht ist|Geben Sie **letzter Domänencontroller in der Domäne** (**- Lastdomaincontrollerindomain**), wenn dieser Wert WAHR ist. Verwendung **- Ignorelastdcindomainmismatch** zu überschreiben, wenn dies wirklich der letzte Domänencontroller ist und phantom Metadaten eines Domänencontrollers|  
|51|Anwendungspartitionen existieren auf diesem Domänencontroller|Gibt an, dass **Anwendungspartitionen entfernen** (**- Removeapplicationpartitions**)|  
|52|Erforderliches Befehlszeilenargument fehlt (d.h. eine Antwortdatei muss in der Befehlszeile angegeben werden)|*Tritt nur bei dem Dcpromo//unattend, das nicht mehr verfügbar ist. Finden Sie ältere Dokumentation*|  
|53|Herauf-/Herabstufung fehlgeschlagen, Computer muss neu gestartet werden, um Bereinigung|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|54|Herauf-/Herabstufung fehlgeschlagen|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|55|Herauf-/Herabstufung wurde vom Benutzer abgebrochen.|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|56|Herauf-/Herabstufung wurde vom Benutzer abgebrochen, Computer muss zur Bereinigung neu gestartet werden|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|58|Bei der RODC-heraufstufung muss ein Sitename angegeben werden|Sie müssen einen Standort für einen RODC angeben, wird nicht automatisch erkannt werden wie bei RWDC|  
|59|Bei der Herabstufung ist dieser Domänencontroller der letzte DNS-Server für eine der betroffenen Zonen|Gibt an, dass dies ist die **letzten DNS-Server in der Domäne** oder verwenden Sie **- Ignorelastdnsserverfordomain**|  
|60|Ein Domänencontroller unter Windows Server 2008 oder höher muss in der Domäne vorhanden sein, um RODC heraufstufen|Mindestens Windows Server2008 oder höher Modell beschreibbaren Domänencontroller heraufstufen|  
|61|Sie können keine Active Directory-Domänendienste mit DNS in einer vorhandenen Domäne installieren, die nicht bereits DNS hostet|*Dieser Fehler nicht möglich*|  
|62|Antwortdatei hat keinen Abschnitt [DCInstall]|*Tritt nur bei dem Dcpromo//unattend, das nicht mehr verfügbar ist. Finden Sie ältere Dokumentation.*|  
|63|Gesamtstruktur-Funktionsebene ist Windows Server2003|Funktionsebene der Gesamtstruktur auf mindestens Windows Server2003 im einheitlichen Modus. Windows2000 und Windows NT 4.0 sind nicht mehr unterstützte Betriebssysteme|  
|64|Heraufstufung wegen Fehler bei binären Erkennung Komponente fehlgeschlagen|Installieren der AD DS-Rolle|  
|65|Heraufstufung wegen Fehler bei binären Komponenteninstallation fehlgeschlagen|Installieren der AD DS-Rolle|  
|66|Heraufstufung wegen Fehler bei Erkennung des Betriebssystems fehlgeschlagen|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle; der Server ist nicht die Betriebssystemversion zurückgeben. Es ist wahrscheinlich, dass der Computer muss vermutlich neu installiert werden, da seine Gesamtintegrität beschädigt ist|  
|68|Replikationspartner ist ungültig|Verwenden Sie repadmin.exe oder die **Get-ADReplication\ *** Windows PowerShell zum Überprüfen der Partner-domänencontrollerintegrität|  
|69|Benötigte Port wird bereits von einer anderen Anwendung verwendet wird|Verwendung **netstat.exe - Anob** um Prozesse zu ermitteln, die fälschlicherweise reservierte AD DS-Ports zugewiesen sind|  
|70|Der Stammdomänencontroller der Gesamtstruktur muss ein globaler Katalogserver sein.|*Tritt nur bei dem Dcpromo//unattend, das nicht mehr verfügbar ist. Finden Sie ältere Dokumentation*|  
|71|DNS-Server ist bereits installiert.|Geben Sie zum Installieren von DNS (**- InstallDNS**), wenn der DNS-Dienst bereits installiert ist|  
|72|Computer wird Remote Desktop Services im Modus ohne Administratorrechte ausgeführt werden.|Dieser Domänencontroller kann nicht heraufgestuft werden, wie sie auch als RDS-Server für mehr als zwei Admin-Benutzer konfiguriert ist. Entfernen Sie RDS erst, nachdem Sie dessen Nutzung sorgfältig, wenn es, indem Anwendungen oder Endbenutzern, zum Entfernen verwendet wird ein Ausfalls bewirkt|  
|73|Die angegebene Gesamtstrukturfunktionsebene ist ungültig.|Geben Sie eine gültige Gesamtstrukturfunktionsebene an|  
|74|Die angegebene Domänenfunktionsebene ist ungültig.|Geben Sie eine gültige Domänenfunktionsebene an|  
|75|Kann nicht die Standard-Kennwortreplikationsrichtlinie bestimmt.|Überprüfen Sie, dass die RODC-Kennwortreplikationsrichtlinie existiert und zugänglich ist|  
|76|Angegebene replizierte/nicht replizierte Sicherheitsgruppen sind ungültig|Überprüfen Sie, ob Sie bei der Angabe einer Kennwortreplikationsrichtlinie gültige Domänen- und Benutzerkonten eingegeben haben|  
|77|Das angegebene Argument ist ungültig|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|78|Fehler beim Überprüfen von Active Directory-Gesamtstruktur|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|79|RODC kann nicht heraufgestuft werden, da Rodcprep nicht ausgeführt wurde|Windows Server2012 verwenden, um die Gesamtstruktur vorzubereiten, oder verwenden Sie **adprep.exe/rodcprep**|  
|80|DomainPrep wurde nicht ausgeführt|Mit Windows Server2012 Vorbereiten der Domäne, oder führen **adprep.exe/domainprep**|  
|81|ForestPrep wurde nicht ausgeführt|Windows Server2012 verwenden, um die Gesamtstruktur vorzubereiten, oder verwenden Sie **adprep.exe/ForestPrep**|  
|82|Gesamtstrukturschema-Konflikt|Windows Server2012 verwenden, um die Gesamtstruktur vorzubereiten, oder verwenden Sie **adprep.exe/ForestPrep**|  
|83|Nicht unterstützte SKU|*Dieser Fehler nicht wahrscheinlich*|  
|84|Keine Domänencontroller-Konto gefunden|Überprüfen Sie, ob vorhandene Domänencontroller die korrekte Benutzerkontensteuerungs-Attribut festgelegt haben.|  
|85|Auswählen ein Domänencontrollerkontos für Phase 2 nicht möglich|Zurückgegeben, wenn Sie "vorhandenes Konto verwenden" jedoch entweder kein Konto gefunden wurde oder bei der kontosuche ein Fehler vorliegt. Stellen Sie sicher, dass Sie das korrekte gestaffelte RODC-Konto angegeben haben.|  
|86|Heraufstufung Stufe 2 muss ausführen müssen|Zurückgegeben, wenn Sie einen zusätzlichen Domänencontroller heraufstufen, jedoch bereits ein Konto existiert und "Erneute Installation erlauben" nicht angegeben wurde|  
|87|Ein in Konflikt stehendes Domänencontrollerkonto existiert|Benennen Sie den Computer vor dem Heraufstufen, wenn Sie nicht versuchen, an einen nicht belegten Domänencontroller anzufügen. Muss angefügt werden, um das nicht belegten Domänencontroller mit **- Useexistingaccount** und das richtige schreibgeschützt oder beschreibbar Argument, je nach Kontotyp|  
|88|Der angegebene serveradmin ist ungültig.|Sie haben ein ungültiges Konto für die RODC Admin-Delegierung angegeben. Stellen Sie sicher, dass das angegebene Konto ein gültiger Benutzer oder eine Gruppe ist.|  
|89|RID-Master für die angegebene Domäne ist offline.|Verwendung **netdom.exe Query Fsmo** den RID-Master zu erkennen. Online schalten und Zugriff auf den Domänencontroller, den Sie erweitern|  
|90|Domänennamenmaster ist offline.|Verwendung **netdom.exe Query Fsmo** den Domänennamenmaster zu erkennen. Online schalten und Zugriff auf den Domänencontroller, den Sie erweitern|  
|91|Um festzustellen, ob der Prozess wow64 ist fehlgeschlagen|*Dieser Fehler nicht möglich ist nicht mehr, das Betriebssystem 64-Bit*|  
|92|WOW64-Prozess wird nicht unterstützt.|*Dieser Fehler nicht möglich ist nicht mehr, das Betriebssystem 64-Bit*|  
|93|Domänencontrollerdienst wird nicht ausgeführt für nichterzwungene Herabstufung|Starten Sie den AD DS-Dienst|  
|94|Kennwort des lokalen Administrators stimmt nicht überein: entweder leer oder nicht erforderlich|Ein nicht leeres Kennwort angeben, und stellen Sie sicher, dass die lokale Kennwortrichtlinie ein Kennwort erforderlich ist.|  
|95|Kann nicht gelöscht werden letzten Windows Server2008 oder höher Domänencontroller in der Domäne, in denen Live-RODCs existieren|Sie müssen zunächst alle RODCs herabstufen, bevor Sie alle Windows Server2008 oder höher beschreibbaren Domänencontroller herabstufen können|  
|96|So deinstallieren Sie den DS-Binärdateien|*Tritt nur bei dem Dcpromo//unattend, das nicht mehr verfügbar ist. Finden Sie ältere Dokumentation*|  
|97|Version der Gesamtstrukturfunktionsebene ist neuer als die des Betriebssystems untergeordneten Domäne|Bereitstellen Sie einer untergeordnete Domäne, die gleichen oder höher als die Funktionsebene der Gesamtstruktur|  
|98|Komponente binäre Installation/Deinstallation wird ausgeführt.|*Tritt nur bei dem Dcpromo//unattend, das nicht mehr verfügbar ist. Finden Sie ältere Dokumentation*|  
|99|Funktionsebene der Gesamtstruktur ist zu niedrig (Fehler tritt nur den Windows Server2012 aus)|Funktionsebene der Gesamtstruktur auf mindestens Windows Server2003 im einheitlichen Modus. Windows2000 und Windows NT 4.0 sind nicht mehr unterstützte Betriebssysteme|  
|100|Domänenfunktionsebene ist zu niedrig (Fehler tritt nur den Windows Server2012 aus)|Lösen Sie die Domänenfunktionsebene mindestens Windows Server2003 im einheitlichen Modus. Windows2000 und Windows NT 4.0 sind nicht mehr unterstützte Betriebssysteme|  
  
#### <a name="knownlikely-issues-and-support-scenarios"></a>Bekannte/häufige Probleme und Supportszenarien  
Die folgende Liste gängiger Probleme während der Entwicklung von Windows Server 2012. All diese Probleme sind "beabsichtigt" und eine gültige problemumgehung oder eine geeignetere Methode in erster Linie vermeiden. Viele dieser Verhaltensweisen sind identisch unter Windows Server2008 R2 und älteren Betriebssystemen, aber die neue Version der AD DS-Bereitstellung bringt gestiegener Empfindlichkeit für Probleme.  
  
|Problem|Herabstufen eines Domänencontrollers bleibt DNS ohne Zonen zurück|  
|---------|-----------------------------------------------------------------|  
|Symptome|Server weiterhin auf DNS-Anforderungen reagiert verfügt jedoch keine Zoneninformationen|  
|Lösung und Hinweise|Wenn Sie die AD DS-Rolle entfernen, auch Entfernen der DNS-Serverrolle oder des DNS-Serverdiensts deaktiviert. Denken Sie daran, sich selbst als einen anderen Server den DNS-Client auf. Wenn Sie Windows PowerShell verwenden, führen Sie Folgendes, nachdem Sie den Server herabzustufen:<br /><br />Code - deinstallieren-Windowsfeature dns<br /><br />oder<br /><br />Code - Set-Service-DNS - Starttyp deaktiviert<br />Stop-Service-dns|  
  
|Problem|Heraufstufen von einem Windows Server2012 in einer vorhandenen einteilige Domäne wird Updatetopleveldomain nicht konfiguriert = 1 bzw. Allowsinglelabeldnsdomain = 1|  
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|  
|Symptome|Dynamische DNS-Registrierung tritt nicht auf.|  
|Lösung und Hinweise|Legen Sie diese Werte über die Netlogon- und DNS-Gruppenrichtlinien. Microsoft begann blockiert die Erstellung einteiliger Domänen, in Windows Server2008; Sie können ADMT oder das Domänenumbenennungstool um in einer genehmigten DNS-Domänenstruktur zu ändern.|  
  
|Problem|Herabstufung des letzten Domänencontrollers in einer Domäne schlägt fehl, wenn vorab erstellte und nicht belegte RODC-Konten vorhanden sind|  
|---------|------------------------------------------------------------------------------------------------------------|  
|Symptome|Herabstufung schlägt fehl mit Meldung:<br /><br />**Dcpromo.General.54**<br /><br />Active Directory Domain Services konnte nicht gefunden werden einer anderen Active Directory-Domänencontroller übertragen Sie die verbleibenden Daten in der Verzeichnispartition CN = Schema, CN = Configuration, DC = corp, DC = Contoso, DC = com.<br /><br />"Das Format des angegebenen Domänennamens ist ungültig."|  
|Lösung und Hinweise|Entfernen Sie alle verbleibenden vorab erstellten RODC-Konten vor dem Herabstufen einer Domäne mit **Dsa.msc** oder **Ntdsutil.exe Metadatenbereinigung**.|  
  
|Problem|Automatische Gesamtstruktur- und domänenvorbereitung führt GPPREP nicht aus.|  
|---------|---------------------------------------------------------------|  
|Symptome|Domänenübergreifende Funktionalität für Gruppenrichtlinien, Richtlinienergebnissatz (Resultant Set of Policy, RSOP) Planungsmodus, benötigt aktualisiertes Dateisystem und Active Directory-Berechtigungen für vorhandene GP. Ohne Gpprep nicht RSOP-Planung domänenübergreifend verwendet werden.|  
|Lösung und Hinweise|Führen Sie **adprep.exe/gpprep** manuell für alle Domänen, die zuvor nicht für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Administratoren sollten gpprep nur einmal während der Lebensdauer einer Domäne nicht bei jedem Upgrade ausführen. Es wird nicht durch automatische Adprep ausgeführt werden, dass wenn Sie bereits entsprechende benutzerdefinierte Berechtigungen festgelegt haben, alle SYSVOL-Inhalte erneut auf allen Domänencontrollern repliziert ist.|  
  
|Problem|Installieren von Medium kann nicht geprüft werden, wenn auf einen UNC-Pfad verweist|  
|---------|------------------------------------------------------------------|  
|Symptome|Fehler zurückgegeben:<br /><br />Code – Medienpfad konnte nicht überprüft werden. Ausnahme beim Aufrufen von "GetDatabaseInfo" mit "2" Argumenten. Der Ordner ist ungültig.|  
|Lösung und Hinweise|Sie müssen IFM-Dateien auf einem lokalen Datenträger, nicht auf einem remote UNC-Pfad speichern. Diese beabsichtigte verhindert Sperre die teilweise heraufstufung netzwerkunterbrechungen.|  
  
|Problem|DNS-Delegierungswarnung zweimal bei der heraufstufung von Domänencontrollern angezeigt|  
|---------|-------------------------------------------------------------------------|  
|Symptome|Warnung zurückgegeben *zweimal* bei der Ausführung von ADDSDeployment Windows PowerShell:<br /><br />Code - "eine Delegierung für diesen DNS-Server kann nicht erstellt werden, da die autorisierende übergeordnete Zone nicht gefunden werden, oder er nicht ausgeführt, Windows-DNS wird-Server. Wenn Sie die Integration in eine vorhandene DNS-Infrastruktur vornehmen möchten, sollten Sie manuell eine Delegierung an den DNS-Server in der übergeordneten Zone, um sicherzustellen, dass zuverlässige Namensauflösung von außerhalb der Domäne erstellen. Andernfalls ist keine Aktion erforderlich."|  
|Lösung und Hinweise|Ignorieren. ADDSDeployment Windows PowerShell zeigt die Warnung zuerst bei der voraussetzungsprüfung aus, und klicken Sie dann erneut bei der Konfiguration des Domänencontrollers. Wenn Sie keine DNS-Delegierung konfigurieren möchten, verwenden Sie Argument:<br /><br />Code - - Creatednsdelegation: $false<br /><br />Führen Sie *nicht* voraussetzungsprüfungen überspringen, um diese Meldung zu Unterdrücken|  
  
|Problem|UPN oder außerhalb der Domäne Anmeldeinformationen angeben, bei der Konfiguration zurückgegeben irreführende Fehler|  
|---------|--------------------------------------------------------------------------------------------|  
|Symptome|Server-Manager gibt Fehler zurück:<br /><br />Code - Ausnahme beim Aufrufen von "DNSOption" mit "6" Argumenten<br /><br />ADDSDeployment Windows PowerShell gibt Fehler zurück:<br /><br />Code - Überprüfung von Berechtigungen, ist fehlgeschlagen. Sie müssen den Namen der Domäne angeben, zu denen dieses Benutzerkonto gehört.|  
|Lösung und Hinweise|Stellen Sie sicher, dass Sie gültige Domänen-Anmeldeinformationen in Form von bereitstellen **Domäne\Benutzer**.|  
  
|Problem|Entfernen der DirectoryServices-DomainController-Rolle mithilfe von Dism.exe führt zu nicht startbaren Server|  
|---------|---------------------------------------------------------------------------------------------------|  
|Symptome|Wenn Sie Dism.exe verwenden, um die AD DS-Serverrolle zu entfernen, bevor Sie ordnungsgemäß Herabstufen eines Domänencontrollers, wird der Server nicht mehr normal startet und zeigt Fehler:<br /><br />Code - Status: 0x000000000<br />Info: Es ist ein unerwarteter Fehler aufgetreten.|  
|Lösung und Hinweise|Im Verzeichnisdienst-Wiederherstellungsmodus mit starten *UMSCHALT+F8*. Hinzufügen der AD DS-Serverrolle zurück, und klicken Sie dann den Domänencontroller zwangsweise herabstufen. Sie können auch wiederherstellen Sie den Systemstatus von Sicherung. Verwenden Sie keine Dism.exe zum Entfernen von AD DS-Rolle. Das Dienstprogramm hat keine Kenntnis von Domänencontrollern.|  
  
|Problem|Installieren einer neuen Gesamtstruktur festlegen Forestmode win2012 schlägt fehl|  
|---------|--------------------------------------------------------------------|  
|Symptome|Bei der heraufstufung mit ADDSDeployment Windows PowerShell gibt Fehler zurück:<br /><br />Code - Test.VerifyDcPromoCore.DCPromo.General.74<br /><br />Fehler bei Überprüfung der erforderlichen Komponenten zum Domänencontroller heraufstufen. Die angegebene Domänenfunktionsebene ist ungültig|  
|Lösung und Hinweise|Geben Sie eine funktionale Gesamtstrukturmodus win2012 *auch* eine funktionale Domänenmodus win2012 angeben. Hier ist ein Beispiel, das fehlerfrei funktioniert:<br /><br />Code - - Forestmode Win2012 - Domainmode Win2012]|  
  
|||  
|-|-|  
|Problem|Überprüfen, ob in Install from Media-Auswahlbereichs klicken, geschieht nichts|  
|Symptome|Wenn Sie einen Pfad zu einem IFM-Ordner angeben, durch Klicken auf die **überprüfen, ob** Schaltfläche nie sendet eine Nachricht oder nichts angezeigt wird.|  
|Lösung und Hinweise|Die **überprüfen, ob** Schaltfläche gibt nur Fehler zurück, wenn Probleme auftreten. Andernfalls wird die **Weiter** Schaltfläche ausgewählt werden, wenn Sie einen IFM-Pfad angegeben haben. Klicken Sie auf **überprüfen, ob** zur Vorgehensweise, wenn Sie IFM ausgewählt haben.|  
  
|||  
|-|-|  
|Problem|Herabstufung mit Server-Manager bietet keine Feedback bis abgeschlossen.|  
|Symptome|Wenn Server-Manager zum Entfernen der AD DS-Rolle und zum Herabstufen eines Domänencontrollers, besteht keine kontinuierliches Feedback erhalten, bis die Herabstufung fehlschlägt bzw. abgeschlossen ist.|  
|Lösung und Hinweise|Dies ist eine Einschränkung von Server-Manager. Verwenden Sie für Feedback ADDSDeployment Windows PowerShell-Cmdlet aus:<br /><br />Code - Uninstall-addsdomaincontroller|  
  
|||  
|-|-|  
|Problem|Die Install from Media-Prüfung erkennt nicht, ein RODC-Medium für beschreibbaren Domänencontroller oder umgekehrt.|  
|Symptome|Beim Heraufstufen eines neuen Domänencontrollers mit IFM Heraufstufen und dabei IFM - z.B. ein RODC-Medium für einen beschreibbaren Domänencontroller oder RWDC-Medium für einen RODC - wird die Schaltfläche "bestätigen" kein Fehler zurückgegeben. Tritt der Fehler später Werbung:<br /><br />Konfigurieren Sie diesen Computer als Domänencontroller in Code - ist ein Fehler aufgetreten. <br />Die Förderung Install-From-Media eine Read-Only Domänencontroller kann nicht gestartet werden, da die angegebene Quelldatenbank nicht zulässig ist. Für die IFM-heraufstufung eines RODC können nur Datenbanken von anderen RODCs verwendet werden.|  
|Lösung und Hinweise|Vergewissern Sie sich prüft nur die Gesamtintegrität von IFM. Bieten Sie keine der IFM-Typ für einen Server. Starten Sie den Server neu, bevor Sie Werbung mit dem korrekten Medium erneut versuchen.|  
  
|||  
|-|-|  
|Problem|Die heraufstufung eines RODC in einem vorab erstellten Computerkonto schlägt fehl|  
|Symptome|Wenn Sie ADDSDeployment Windows PowerShell verwenden, um einen neuen RODC mit einem gestaffelten Computerkonto bewerben, die Fehlermeldung:<br /><br />Code - Parametersatz kann nicht mit den angegebenen benannten Parameter aufgelöst werden.    <br />Ungültiges Argument angezeigt: ParameterBindingException<br />    + FullyQualifiedErrorId: AmbiguousParameterSet, Microsoft.DirectoryServices.Deployment.PowerShell.Commands.Install|  
|Lösung und Hinweise|Bieten Sie keine Parameter, die bereits auf einem vorab erstellten RODC-Konto bereits definiert. Dazu zählen:<br /><br />Code - - readonlyreplica<br />-installdns<br />-donotconfigureglobalcatalog<br />-sitename<br />-installdns|  
  
|||  
|-|-|  
|Problem|Aufheben der Auswahl/Deaktivieren der Option "Zielserver automatisch bei Bedarf neu starten" hat keine Auswirkung|  
|Symptome|Aktivieren (bzw. nicht auswählen) die Option Server Manager **Zielserver bei Bedarf automatisch neu** Whendemoting eines Domänencontrollers durch Entfernen der Rolle, des Servers immer neu gestartet, unabhängig von Ihrer Auswahl.|  
|Lösung und Hinweise|Dies ist beabsichtigt. Der Herabstufungsprozess startet den Server unabhängig von dieser Einstellung neu.|  
  
|||  
|-|-|  
|Problem|Dcpromo.log zeigt "[Fehler] sicherheitseinstellung für Serverdateien fehlgeschlagen mit 2"|  
|Symptome|Herabstufung eines Domänencontrollers läuft ohne Fehler, aber das Dcpromo-Protokoll geht hervor Fehler:<br /><br />Code - [Fehler] Festlegen der Sicherheit für Serverdateien fehlgeschlagen mit 2|  
|Lösung und Hinweise|Ignorieren, dieser Fehler ist zu erwarten und kosmetischer Natur.|  
  
|||  
|-|-|  
|Problem|Adprep-voraussetzungsprüfung tritt der Fehler "Kann nicht Exchange-schemakonfliktüberprüfung ausgeführt"|  
|Symptome|Wenn Sie versuchen, einen Windows Server2012-Domänencontroller in einer vorhandenen Windows Server2003, Windows Server2008 oder Windows Server2008 R2-Gesamtstruktur heraufzustufen, tritt der Fehler Überprüfung der Voraussetzungen:<br /><br />Code - Überprüfung der Voraussetzungen für die Vorbereitung der Active Directory ist fehlgeschlagen. Führen Sie Exchange-schemakonfliktüberprüfung für die Domäne kann nicht *<domain name>* (Ausnahme: der RPC-Server ist nicht verfügbar)<br /><br />Die adprep.log wird die Fehlermeldung angezeigt:<br /><br />Code - Adprep Daten konnten nicht vom Server abgerufen*<domain controller>*<br /><br />über Windows-Verwaltungsinstrumentation (WMI).|  
|Lösung und Hinweise|Der neue Domänencontroller kann nicht über DCOM/RPC-Protokolle für die existierenden Domänencontroller WMI zugreifen. Aktuell existieren drei Ursachen für diesen Fehler:<br /><br />– Eine Firewall blockiert den Zugriff auf den existierenden Domänencontrollern<br /><br />-Das Konto Netzwerkdienst fehlt "Anmelden als Dienst" (SeServiceLogonRight) Berechtigungen auf den existierenden Domänencontrollern<br /><br />-NTLM ist mit in beschriebenen Sicherheitsrichtlinien auf den Domänencontrollern deaktiviert [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(WS.10).aspx)|  
  
|||  
|-|-|  
|Problem|Erstellen Sie eine neue AD DS-Gesamtstruktur immer von DNS-Warnung angezeigt|  
|Symptome|Beim Erstellen einer neuen AD DS-Gesamtstruktur, und erstellen die DNS-Zone auf den neuen Domänencontroller für sich selbst, Sie immer Warnung angezeigt werden:<br /><br />In der DNS-Konfiguration wurde Code - Fehler festgestellt. <br />Keiner der von diesem Computer verwendet DNS-Server innerhalb des Zeitlimits geantwortet.<br />(Fehlercode: 0x000005B4 "ERROR_TIMEOUT")|  
|Lösung und Hinweise|Ignorieren. Diese Warnung ist beabsichtigt, auf dem ersten Domänencontroller in der Stammdomäne einer neuen Gesamtstruktur, für den Fall, dass Sie auf eine vorhandene DNS-Server und die Zone verwiesen werden soll.|  
  
|||  
|-|-|  
|Problem|Windows PowerShell - Whatif-Argument gibt falsche DNS-Serverinformationen zurück.|  
|Symptome|Bei Verwendung der **- Whatif** Argument bei der Konfiguration eines Domänencontrollers mit implizitem oder explizitem **- Installdns: $true**, Ausgabe angezeigt:<br /><br />Code - "DNS-Server: No"|  
|Lösung und Hinweise|Ignorieren. DNS ist installiert und ordnungsgemäß konfiguriert.|  
  
|||  
|-|-|  
|Problem|Nach der heraufstufung schlägt fehl, Anmeldung mit "steht nicht genügend Speicher zum Verarbeiten des Befehls"|  
|Symptome|Nachdem Sie einen neuen Domänencontroller heraufstufen und melden Sie sich ab und versuchen, sich interaktiv anzumelden, wird die folgende Fehlermeldung angezeigt:<br /><br />Code - steht nicht genügend Speicher zum Verarbeiten des Befehls|  
|Lösung und Hinweise|Der Domänencontroller wurde nach der heraufstufung, entweder aufgrund eines Fehlers nicht neu gestartet, oder weil Sie das ADDSDeployment Windows PowerShell-Argument angegeben **- Norebootoncompletion **. Starten Sie den Domänencontroller neu.|  
  
|||  
|-|-|  
|Problem|Die Schaltfläche "Weiter" ist nicht verfügbar, auf der Seite Domänencontrolleroptionen|  
|Symptome|Auch wenn Sie ein Kennwort festgelegt haben die **Weiter** auf die Schaltfläche der **Domänencontrolleroptionen** Seite im Server-Manager ist nicht verfügbar. Es ist keine Sites die **Standortname** Menü.|  
|Lösung und Hinweise|Sie verfügen über mehrere AD DS-Standorte und mindestens eine fehlen Subnetze. Dieser zukünftige Domänencontroller gehört zu einem dieser Subnetze. Sie müssen manuell das Subnetz aus der Dropdownmenü Sitename auswählen. Überprüfen Sie auch alle DSSITE.MSC, oder verwenden Sie den folgenden Windows PowerShell-Befehl sucht alle Sites fehlen Subnetze:<br /><br />Code - Get-Adreplicationsite-Filter *-Eigenschaft Subnetze & 124; WHERE-Object {! $_.subnets -eq "\ *"} & 124; Format-Table name|  
  
|||  
|-|-|  
|Problem|Oder Herabstufung schlägt fehl mit "kann keine Meldung der Dienst gestartet werden"|  
|Symptome|Wenn Sie versuchen, einen heraufstufen, herabstufen oder Klonen eines Domänencontrollers erhalten Sie Fehler:<br /><br />Code - der Dienst kann nicht gestartet werden, entweder weil ist deaktiviert, oder es ist keine aktivierten Geräte zugeordnet"(0x80070422)<br /><br />Der Fehler ist möglicherweise interaktive, ein Ereignis oder eines der Protokolle wie z.B. dcpromoui.log oder dcpromo.log geschrieben|  
|Lösung und Hinweise|Der DS-rollenserverdienst (DsRoleSvc) ist deaktiviert. Standardmäßig wird dieser Dienst während der Installation von AD DS-Rolle installiert und Starttyp festgelegt. Deaktivieren Sie diesen Dienst nicht. Legen Sie sie zurück auf manuell, und ermöglichen Sie den DS-rollenoperationen starten und beenden Sie diesen bei Bedarf. Dieses Verhalten ist beabsichtigt.|  
  
|||  
|-|-|  
|Problem|Server-Manager erhalten weiterhin eine Warnung, dass Sie Domänencontroller heraufstufen müssen|  
|Symptome|Wenn Sie einen Domänencontroller mit veralteten dcpromo.exe//unattend Heraufstufen oder ein einer vorhandenen Windows Server2008 R2-Domänencontrollers auf Windows Server2012 Upgrade, Server-Manager wird nach der Bereitstellungskonfiguration **Server zu einem Domänencontroller heraufstufen **.|  
|Lösung und Hinweise|Klicken Sie auf den Warn-Link, und die Meldung verschwindet. Dieses Verhalten ist erwarten und kosmetischer Natur.|  
  
|||  
|-|-|  
|Problem|Server-Manager-Bereitstellungsskript fehlende Rolleninstallation|  
|Symptome|Wenn Sie einen Domänencontroller mit Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, werden keine der Rolle Cmdlet und Argumente (Install-Windowsfeature-Ad-Domain-Services - Includemanagementtools nennen). Der Domänencontroller kann nicht konfiguriert werden, ohne die Rolle.|  
|Lösung und Hinweise|Manuell hinzufügen, das Cmdlet und Argumente für alle Skripts. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  
  
|||  
|-|-|  
|Problem|Server-Manager-Bereitstellungsskript ist nicht PS1-Datei benannt.|  
|Symptome|Wenn Sie einen Domänencontroller mit Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, wird die Datei mit einem zufälligen temporären Namen und nicht als PS1-Datei benannt.|  
|Lösung und Hinweise|Benennen Sie die Datei manuell um. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  
  
|Problem|Dcpromo//unattend können nicht unterstützte funktionale Ebenen|  
|-|-|  
|Symptome|Wenn Sie einen Domänencontroller mithilfe von Dcpromo//unattend mit der folgenden Beispiel-Antwortdatei heraufstufen:<br /><br />Code-<br /><br />[DCInstall]<br />NewDomain = Gesamtstruktur<br /><br />ReplicaOrNewDomain = Domain<br /><br />NewDomainDNSName = corp.contoso.com<br /><br />SafeModeAdminPassword =Safepassword@6<br /><br />DomainNetbiosName = corp<br /><br />DNSOnNetwork = Yes<br /><br />AutoConfigDNS = Yes<br /><br />RebootOnSuccess = NoAndNoPromptEither<br /><br />RebootOnCompletion = No<br /><br />*DomainLevel = 0*<br /><br />*ForestLevel = 0*<br /><br />Die heraufstufung schlägt mit den folgenden Fehlern in dcpromoui.log die:<br /><br />Code - Dcpromoui EA4.5B8 0089 13:31:50.783 EINGABETASTE CArgumentsSpec::ValidateArgument DomainLevel<br /><br />Dcpromoui EA4.5B8 008A 13:31:50.783 Wert für DomainLevel ist 0<br /><br />Dcpromoui EA4.5B8 008 b 13:31:50.783 Exitcode ist 77<br /><br />Dcpromoui EA4.5B8 008C 13:31:50.783 das angegebene Argument ist ungültig.<br /><br />Dcpromoui EA4.5B8 008D 13:31:50.783 schließenden Protokoll<br /><br />Dcpromoui EA4.5B8 0032 13:31:50.830 Exitcode ist 77<br /><br />Ebene 0 steht für Windows2000, die in Windows Server2012 nicht unterstützt wird.|  
|Lösung und Hinweise|Verwenden Sie die veralteten Befehl Dcpromo//unattend nicht, und wissen Sie, dass Sie die Angabe ungültiger Einstellungen, späteren zu Fehlern führen können. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  

|Problem|Werbung "hängt", bei der Erstellung des NTDS-Einstellungsobjekt wird nicht beendet|  
|-|-|  
|Symptome|Wenn Sie ein Replikat-Domänencontroller oder einen RODC heraufstufen, "Erstellen von NTDS-Einstellungsobjekts" erreicht die Förderung und wird nicht fortgesetzt oder abgeschlossen ist. Die Protokolle nicht mehr, ebenfalls aktualisiert.|  
|Lösung und Hinweise|Dies ist ein bekanntes Problem, durch Bereitstellen von Anmeldeinformationen des integrierten lokalen Administratorkontos mit dem Kennwort integrierten Domänenadministratorkontos verursacht. Dies kann bei einem Ausfall nach unten in der zentralen Setupmodul, das keine Fehler, sondern unbegrenzt wartet (quasi Schleife) unterstützt. Dies wird erwartet,-obgleich unerwünschten - Verhalten.<br /><br />So beheben Sie den Server:<br /><br />1. Neu starten.<br /><br />1. In Active Directory Löschen des Servers Mitglieds-Computerkonto (es wird nicht noch kein Domänencontroller-Konto.)<br /><br />1. Auf dem Server trennen Sie nach Ablauf der Anmeldezeit es aus der Domäne<br /><br />1. Auf diesem Server entfernen Sie die AD DS-Rolle.<br /><br />1. Neustart<br /><br />1. Erneut hinzufügen, die AD DS-Rolle und wiederholen Förderung, um sicherzustellen, dass Sie immer Bereitstellen der ***Domain\admin*** Anmeldeinformationen DC-heraufstufung und nicht nur das integrierte lokale Administratorkonto|  
