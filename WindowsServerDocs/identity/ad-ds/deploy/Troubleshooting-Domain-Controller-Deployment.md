---
ms.assetid: 5ab76733-804d-4f30-bee6-cb672ad5075a
title: Problembehandlung der Domänencontrollerbereitstellung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 54ae67c520f2874199982ca790ced5db346f0c16
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877571"
---
# <a name="troubleshooting-domain-controller-deployment"></a>Problembehandlung der Domänencontrollerbereitstellung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel behandelt detaillierte Methoden für die Problembehandlung bei Konfiguration und Bereitstellung von Domänencontrollern.  
  
-   [Einführung in die Problembehandlung](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md#BKMK_Intro)  
  
-   [Optionen für die Problembehandlung](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md#BKMK_Options)  
  
## <a name="BKMK_Intro"></a>Einführung in die Problembehandlung  
![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/adds_deploy_troubleshooting.png)  
  
## <a name="BKMK_Options"></a>Optionen für die Problembehandlung  
  
### <a name="logging-options"></a>Protokollierungsoptionen  
Die integrierten Protokolle sind das wichtigste Hilfsmittel für die Fehlerbehebung bei Herauf- und Herabstufung von Domänencontrollern. All diese Protokolle sind standardmäßig aktiviert und für maximale Ausführlichkeit konfiguriert.  
  
|Phase|Protokoll|  
|---------|-------|  
|Server-Manager- bzw. ADDSDeployment-Windows PowerShell-Operationen|-%systemroot%\debug\dcpromoui.log<br /><br />-%systemroot%\debug\dcpromoui*.log|  
|Installation/Heraufstufung des Domänencontrollers|-%systemroot%\debug\dcpromo.log<br /><br />-%systemroot%\debug\dcpromo*.log<br /><br />-Ereignisanzeige\windows-protokolle\system Ereignis<br /><br />-Ereignisanzeige\windows-protokolle\anwendung Ereignis<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\verzeichnisdienst<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dateireplikationsdienst<br /><br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dfs-Replikation|  
|Upgrade von Gesamtstruktur oder Domäne|-   %systemroot%\debug\adprep\\<datetime>\adprep.log<br /><br />-   %systemroot%\debug\adprep\\<datetime>\csv.log<br /><br />-   %systemroot%\debug\adprep\\<datetime>\dspecup.log<br /><br />-%systemroot%\debug\adprep\\<datetime>\ldif.log*|  
|Server-Manager ADDSDeployment Windows PowerShell Bereitstellungsmodul|-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\microsoft\windows\verzeichnisdienste-bereitstellung\operational|  
|Windows-Wartung|-%systemroot%\Logs\CBS\\*<br /><br />-%systemroot%\servicing\sessions\sessions.xml<br /><br />-%systemroot%\winsxs\poqexec.log<br /><br />-%systemroot%\winsxs\pending.xml|  
  
### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Domänencontroller-Konfiguration  
Die folgenden Tools dienen als Ausgangspunkt bei der Behandlung von Problemen, die nicht durch Protokolle erklärt werden können:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   [AutoRuns.exe](https://technet.microsoft.com/sysinternals/bb963902.aspx), Task-Manager und MSInfo32.exe  
  
-   [Network Monitor 3.4](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=4865) (oder ein Tool netzwerkerfassungs- und Analysetools von Drittanbietern)  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>Allgemeine Methoden für die Problembehandlung bei der Domänencontroller-Konfiguration  
  
1.  Wurde das Problem durch einen einfachen Syntaxfehler verursacht?  
  
    1.  Haben Sie sich vertippt oder ein Argument von ADDSDeployment Windows PowerShell vergessen? Haben Sie z. B. beim Einsatz von ADDSDeployment Windows PowerShell vergessen, das benötigte Argument **-domainname** mit einem gültigen Namen anzugeben?  
  
    2.  Prüfen Sie die Windows PowerShell-Konsolenausgabe sorgfältig, um herauszufinden, warum die eingegebene Befehlszeile nicht korrekt verarbeitet wird.  
  
2.  Wurde das Problem durch einen Fehler bei den Voraussetzungen verursacht?  
  
    1.  Viele Probleme, die früher zu schwerwiegenden Fehlern bei der Heraufstufung führten, werden nun durch die Voraussetzungsüberprüfung verhindert.  
  
    2.  Prüfen Sie den Text der Voraussetzungsfehler sorgfältig. Diese liefern entscheidende Hinweise für die Lösung der meisten Probleme, da es sich um kontrollierte Szenarien handelt.  
  
3.  Tritt das Problem bei der Heraufstufung auf und ist somit nicht behebbar?  
  
    1.  Prüfen Sie die Ergebnisse sorgfältig: viele Fehler haben einfache Ursachen wie z. B. falsche Kennwörter, Netzwerk-Namensauflösung oder kritische Offline-Domänencontroller.  
  
    2.  Suchen Sie in den Dateien Dcpromoui.log und dcpromo.log nach den in der Ausgabe angezeigten Fehlern und untersuchen Sie die Protokolle ab deren Auftreten rückwärts, um Hinweise auf die Fehlerursache zu erhalten.  
  
        1.  Vergleichen Sie die Protokolle immer mit einem funktionierenden Beispielprotokoll  
  
        2.  Suchen Sie nur dann nach Fehlern in den ADPrep-Protokollen, wenn die Ergebnisse auf ein Problem bei der Schemaerweiterung oder der Vorbereitung von Gesamtstruktur oder Domäne hindeuten.  
  
        3.  Suchen Sie nur dann nach Fehlern im Verzeichnisdienste-Bereitstellung-Ereignisprotokoll, wenn in der Datei Dcpromoui.log Details fehlen oder die Datei aufgrund eines Ausnahmefehlers beim Konfigurationsprozess abrupt endet.  
  
    3.  Untersuchen Sie die Ereignisprotokolle Verzeichnisdienste, System und Anwendungen nach weiteren Anzeichen für Konfigurationsprobleme. Oft sind Probleme bei der Heraufstufung von Domänencontrollern nur Symptome für andere Netzwerk-Fehlkonfigurationen, die alle verteilten Systeme betreffen würden.  
  
    4.  Verwenden Sie dcdiag.exe und repadmin.exe, um die Integrität der Gesamtstruktur zu prüfen und nach subtilen Fehlkonfigurationen zu suchen, die die weitere Heraufstufung des Domänencontrollers verhindern könnten.  
  
    5.  Verwenden Sie AutoRuns.exe, Task Manager oder MSinfo32.exe, um den Computer auf mögliche Wechselwirkungen durch Software von Drittanbietern zu untersuchen.  
  
        1.  Entfernen Sie Software von Drittanbietern (deaktivieren Sie diese nicht einfach, dadurch wird das Laden von Treibern nicht verhindert).  
  
    6.  Installieren Sie NetMon 3.4 auf dem Computer, dessen Heraufstufung fehlschlägt, sowie auf dem Replikationspartner-Domänencontroller und analysieren Sie den Heraufstufungsprozess mit beidseitigen Netzwerkerfassungen.  
  
        1.  Vergleichen Sie die Ergebnisse mit Ihrer Laborumgebung, um zu verstehen, wie eine korrekte Heraufstufung aussehen soll und wo der Fehler liegt.  
  
        2.  Zu diesem Zeitpunkt liegt der Fehler vermutlich bei den Objekten der Gesamtstruktur, vom Standard abweichenden Sicherheitsänderungen oder dem Netzwerk, und der neue Domänencontroller ist ein Opfer von DNS-Fehlkonfigurationen, Firewalls, Schutzsoftware vor unberechtigten Zugriff oder sonstigen externen Faktoren.  
  
### <a name="troubleshooting-specific-problems"></a>Problembehandlung spezifischer Probleme  
  
#### <a name="events-and-error-messages"></a>Ereignis- und Fehlermeldungen  
Bei der Herauf- und Herabstufung von Domänencontrollern wird am Ende der Operation immer ein Code zurückgegeben, und im Gegensatz zu vielen Programmen steht der Code null nicht für Erfolg. Sie haben mehrere Optionen, um den abschließenden Code bei einer Domänencontroller-Konfiguration abzurufen:  
  
1.  Wenn Sie Server-Manager verwenden, wird das Heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart angezeigt.  
  
2.  Wenn Sie ADDSDeployment Windows PowerShell verwenden, wird das Heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart angezeigt. Alternativ können Sie sich entscheiden, nach Abschluss keinen automatischen Neustart durchzuführen. Sie sollten die **Format-List**-Pipeline hinzufügen, um die Ausgabe leichter lesbar zu machen. Zum Beispiel:  
  
    ```  
    Install-addsdomaincontroller <options> -norebootoncompletion:$true | format-list  
  
    ```  
  
    Im Fehlerfall bei der Voraussetzungsprüfung wird kein Neustart durchgeführt, daher sind diese Fehler in jedem Fall sichtbar. Zum Beispiel:  
  
  ![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/ADDS_PSPrereqError.png)  
  
3.  Prüfen Sie in jedem Szenario die Dateien dcpromo.log und dcpromoui.log.  
  
    > [!NOTE]  
    > Manche der unten genannten Fehler können aufgrund von Konfigurationsänderungen an Betriebssystem und Domänencontroller in späteren Betriebssystemen nicht mehr auftreten. Der neue ADDSDeployment Windows PowerShell-Code verhindert ebenfalls bestimmte Fehler im Gegensatz zu dcpromo.exe /unattend. Dies ist ein weiterer wichtiger Grund, warum Sie Ihre gesamte aktuelle Automatisierung vom veralteten DCPromo auf ADDSDeployment Windows PowerShell umstellen sollten.  
  
Bei Herauf- und Herabstufung werden die folgenden Ergebnis-Erfolgscodes zurückgegeben.  
  
|Fehlercode|Erläuterung|Hinweis|  
|--------------|---------------|--------|  
|1|Ende, Erfolg|Der Neustart muss dennoch ausgeführt werden. Dieser Code weist lediglich darauf hin, dass die Kennzeichnung für den automatischen Neustart entfernt wurde|  
|2|Ende, Erfolg, Neustart erforderlich||  
|3|Ende, Erfolg mit nicht-kritischem Fehler|Wird normalerweise bei einer DNS-Delegierungswarnung zurückgegeben. Verwenden Sie ohne DNS-Delegierung den folgenden Parameter:<br /><br />-creatednsdelegation:$false|  
|4|Ende, Erfolg mit nicht-kritischem Fehler, Neustart erforderlich|Wird normalerweise bei einer DNS-Delegierungswarnung zurückgegeben. Verwenden Sie ohne DNS-Delegierung den folgenden Parameter:<br /><br />-creatednsdelegation:$false|  
  
Bei Herauf- und Herabstufung werden die folgenden Ergebnis-Fehlercodes zurückgegeben. Zusätzlich existiert vermutlich eine erweiterte Fehlermeldung. Lesen Sie stets die gesamte Fehlermeldung sorgfältig, nicht nur den numerischen Teil.  
  
|Fehlercode|Erläuterung|Lösungsvorschlag|  
|--------------|---------------|------------------------|  
|11|Domänencontroller-Heraufstufung wird bereits ausgeführt|Führen Sie niemals mehr als eine Domänencontroller-Heraufstufung gleichzeitig für denselben Zielcomputer aus|  
|12|Benutzer muss Administrator sein|Melden Sie sich mit einem integrierten Administratorkonto an und heben Sie die Rechte mit UAC an|  
|13|Zertifizierungsstelle ist installiert|Sie können diesen Domänencontroller nicht herabstufen, da dieser auch als Zertifizierungsstelle fungiert. Entfernen Sie die ZS erst, nachdem Sie deren Nutzung sorgfältig erfasst haben. Falls die ZS Zertifikate ausstellt, wird deren Entfernung zu einem Ausfall führen. Es wird davon abgeraten, ZS auf Domänencontrollern zu betreiben|  
|14|Ausführen im abgesicherten Modus|Starten Sie den Server im normalen Modus|  
|15|Die Rollenänderung wird durchgeführt, oder der Computer muss neu gestartet werden|Sie müssen den Server vor der Heraufstufung neu starten (aufgrund vorheriger Konfigurationsänderungen)|  
|16|Ausführung auf falscher Plattform|*Wahrscheinlich nicht um diesen Fehler zu erhalten.*|  
|17|Keine NTFS 5-Laufwerke vorhanden|Dieser Fehler kann unter Windows Server 2012 nicht auftreten, da in diesem Fall zumindest %systemdrive% mit NTFS formatiert sein muss|  
|18|Nicht genügend Speicher in "windir"|Geben Sie mithilfe von cleanmgr.exe Speicherplatz auf dem %systemdrive%-Laufwerk frei|  
|19|Namensänderung steht aus. Neustart erforderlich|Starten Sie den Server neu|  
|20|Ungültige Syntax in Computername|Benennen Sie den Computer mit einem gültigen Namen|  
|21|Dieser Domänencontroller enthält FSMO-Rollen, ist ein globaler Katalog und/oder ein DNS-Server|Hinzufügen **- Demoteoperationmasterrole** Verwendung **- Forceremoval**.|  
|22|TCP/IP muss installiert werden oder funktioniert nicht|Prüfen Sie, ob TCP/IP auf dem Computer konfiguriert und gebunden ist und korrekt funktioniert|  
|23|DNS-Client muss zunächst konfiguriert werden|Konfigurieren Sie beim Hinzufügen eines neuen Domänencontrollers zu einer Domäne einen primären DNS-Server|  
|24|Eingegebene Anmeldeinformationen sind ungültig oder unvollständig|Überprüfen Sie Benutzername und Kennwort|  
|25|Domänencontroller für die angegebene Domäne wurde nicht gefunden|Prüfen Sie DNS-Clienteinstellungen und Firewallregeln|  
|26|Liste der Domänen konnte nicht aus der Gesamtstruktur abgerufen werden|Prüfen Sie DNS-Clienteinstellungen, LDAP-Funktionalität und Firewallregeln|  
|27|Fehlender Domänenname|Geben Sie bei Herauf- und Herabstufung eine Domäne an|  
|28|Ungültiger Domänenname|Wählen Sie bei der Heraufstufung einen anderen, gültigen Domänennamen aus|  
|29|Übergeordnete Domäne existiert nicht|Prüfen Sie die bei der Erstellung einer neuen untergeordneten Domäne oder Gesamtstrukturdomäne angegebene übergeordnete Domäne|  
|30|Domäne nicht Teil der Gesamtstruktur|Prüfen Sie den angegebenen Domänennamen|  
|31|Untergeordnete Domäne existiert bereits|Geben Sie einen anderen Domänennamen an|  
|32|Ungültiger NetBIOS-Domänenname|Geben Sie einen gültigen NetBIOS-Domänennamen an|  
|33|Pfad der IFM-Dateien ist ungültig|Prüfen Sie Ihren Pfad zum Install From Media-Ordner|  
|34|Ungültige IFM-Datenbank|Verwenden SIe die korrekte Install From Media-Option für Betriebssystem und Rolle (gleiche Betriebssystem-Version, gleicher Typ von Domänencontroller - RODC oder RWDC)|  
|35|SYSKEY fehlt|Install from Media ist verschlüsselt, und Sie müssen einen gültigen SYSKEY eingeben|  
|37|Ungültiger Pfad für NTDS-Datenbank oder deren Protokolle|Ändern Sie die Pfade für Datenbank und Protokolle zu einem festen NTFS-Laufwerk (kein zugeordnetes Laufwerk oder UNC-Pfad)|  
|38|Nicht genügend Speicherplatz für NTDS-Datenbank oder Protokolle|Geben Sie Speicherplatz mit cleanmgr.exe frei, erweitern Sie den Speicherplatz oder schaffen Sie Speicherplatz, indem Sie nicht benötigte Daten an einen anderen Ort verschieben|  
|39|Ungültiger Pfad für SYSVOL|Ändern Sie den SYSVOL-Pfad zu einem festen NTFS-Laufwerk (kein zugeordnetes Laufwerk oder UNC-Pfad)|  
|40|Ungültiger Sitename|Geben Sie einen existierenden Sitenamen an|  
|41|Kennwort für abgesicherten Modus erforderlich|Geben Sie ein Kennwort für das DSRM-Konto ein. Dieses Kennwort darf unabhängig von der Kennwortrichtlinie nicht leer sein|  
|42|Kennwort für abgesicherten Modus erfüllt die Kriterien nicht (nur Heraufstufung)|Geben Sie ein Kennwort für das DSRM-Konto ein, das die Regeln für die Kennwortrichtlinie erfüllt|  
|43|Admin-Kennwort erfüllt die Kriterien nicht (nur Heraufstufung)|Geben Sie ein Kennwort für das lokale Administratorkonto ein, das die Regeln für die Kennwortrichtlinie erfüllt|  
|44|Der angegebene Name für die Gesamtstruktur ist ungültig|Geben Sie einen gültigen DNS-Namen für die Gesamtstruktur-Stammdomäne an|  
|45|Eine Gesamtstruktur mit diesem Namen ist bereits vorhanden|Wählen Sie einen anderen DNS-Namen für die Gesamtstruktur-Stammdomäne|  
|46|Der angegebene Name für die Struktur ist ungültig|Geben Sie einen gültigen DNS-Domänennamen für die Struktur an|  
|47|Eine Struktur mit diesem Namen ist bereits vorhanden|Wählen Sie einen anderen DNS-Domänennamen für die Struktur|  
|48|Der Strukturname passt nicht in die Gesamtstruktur|Wählen Sie einen anderen DNS-Domänennamen für die Struktur|  
|49|Die angegebene Domäne existiert nicht|Prüfen Sie den eingegebenen Domänennamen|  
|50|Bei der Herabstufung wurde ein nicht angegebener letzter Domänencontroller entdeckt bzw. der letzte Domänencontroller wurde fälschlicherweise angegeben|Geben Sie **Letzter Domänencontroller in der Domäne** (**-lastdomaincontrollerindomain**) nur an, wenn dieser Wert wahr ist. Verwendung **- Ignorelastdcindomainmismatch** überschreiben, wenn dies wirklich der letzte Domänencontroller und phantom-Controller-Metadaten vorhanden ist|  
|51|Anwendungspartitionen existieren auf diesem Domänencontroller|Markieren Sie **Anwendungspartitionen entfernen** (**-removeapplicationpartitions**)|  
|52|Benötigtes Befehlszeilenargument fehlt (d. h. eine Antwortdatei muss in der Befehlszeile angegeben werden)|*Tritt nur bei Dcpromo / unattend, der veraltet ist. Finden Sie die ältere Dokumentation*|  
|53|Herauf-/Herabstufung fehlgeschlagen, Computer muss zur Bereinigung neu gestartet werden|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|54|Herauf-/Herabstufung fehlgeschlagen|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|55|Herauf-/Herabstufung wurde vom Benutzer abgebrochen|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|56|Herauf-/Herabstufung wurde vom Benutzer abgebrochen, Computer muss zur Bereinigung neu gestartet werden|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|58|Bei der RODC-Heraufstufung muss ein Sitename angegeben werden|Sie müssen eine Site für einen RODC angeben, da dieser nicht wie bei RWDC automatisch erkannt wird|  
|59|Bei der Herabstufung ist dieser Domänencontroller der letzte DNS-Server für eine der betroffenen Zonen|Markieren Sie die Opeion **Letzter DNS-Server in der Domäne** oder verwenden Sie **-ignorelastdnsserverfordomain**|  
|60|Für die Heraufstufung des RODC muss ein Domänencontroller unter Windows Server 2008 oder neuer in der Domäne vorhanden sein|Stufen Sie mindestens einen beschreibbaren Domänencontroller unter Windows Server 2008 oder neuer herauf|  
|61|Sie können Active Directory-Domänendienste mit DNS nicht in einer existierenden Domäne installieren, die nicht bereits DNS hostet|*Dieser Fehler tritt nicht möglich*|  
|62|Antwortdatei hat keinen [DCInstall]-Bereich|*Tritt nur bei Dcpromo / unattend, der veraltet ist. Finden Sie die ältere Dokumentation.*|  
|63|Die Funktionsebene der Gesamtstruktur entspricht nicht mindestens Windows Server 2003|Setzen Sie die Domänenfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt|  
|64|Heraufstufung wegen Fehler bei der Erkennung der Komponenten-Binärdatei fehlgeschlagen|Installieren Sie die AD DS-Rolle|  
|65|Heraufstufung wegen Fehler bei der Installation der Komponenten-Binärdatei fehlgeschlagen|Installieren Sie die AD DS-Rolle|  
|66|Heraufstufung wegen Fehler bei der Erkennung des Betriebssystems fehlgeschlagen|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle. Der Server gibt seine Betriebssystem-Version nicht zurück. Der Computer muss vermutlich neu installiert werden, da seine Gesamtintegrität wahrscheinlich beschädigt ist|  
|68|Ungültiger Replikationspartner|Verwenden Sie repadmin.exe oder **Get-ADReplication\***  Windows PowerShell zum Überprüfen der Integrität der Partner-Domänencontrollers|  
|69|Der benötigte Port wird bereits von einer anderen Anwendung verwendet|Verwenden Sie **netstat.exe -anob**, um Prozesse zu ermitteln, die fälschlicherweise reservierte AD DS-Ports verwenden|  
|70|Der Controller der Gesamtstruktur-Stammdomäne muss ein globaler Katalogserver sein|*Tritt nur bei Dcpromo / unattend, der veraltet ist. Finden Sie die ältere Dokumentation*|  
|71|DNS-Server ist bereits installiert|Geben Sie die Option "DNS installieren" (**-installDNS**) nicht an, falls der DNS-Dienst bereits installiert ist|  
|72|Computer führt Remotedesktopdienste nicht im Admin-Modus aus|Dieser Domänencontroller kann nicht heraufgestuft werden, da er auch als RDS-Server für mehr als zwei Admin-Benutzer konfiguriert ist. Entfernen Sie RDS erst, nachdem Sie dessen Nutzung sorgfältig erfasst haben. Falls dieser Dienst von Anwendungen oder Endbenutzern verwendet wird, führt seine Entfernung zu einem Ausfall|  
|73|Die angegebene Gesamtstrukturfunktionsebene ist ungültig.|Geben Sie eine gültige Gesamtstrukturfunktionsebene an|  
|74|Die angegebene Domänenfunktionsebene ist ungültig.|Geben Sie eine gültige Domänenfunktionsebene an|  
|75|Standard-Kennwortreplikationsrichtlinie konnte nicht ermittelt werden.|Vergewissern Sie sich, dass die RODC-Kennwortreplikationsrichtlinie existiert und zugänglich ist|  
|76|Angegebene replizierte/nicht replizierte Sicherheitsgruppen sind ungültig|Prüfen Sie, ob Sie bei der Angabe einer Kennwortreplikationsrichtlinie gültige Domänen- und Benutzerkonten angegeben haben|  
|77|Das angegebene Argument ist ungültig|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|78|Fehler bei der Prüfung der Active Directory-Gesamtstruktur|Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle|  
|79|RODC kann nicht heraufgestuft werden, da rodcprep nicht ausgeführt wurde|Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /rodcprep** aus|  
|80|Domainprep wurde nicht ausgeführt|Bereiten Sie die Domäne mit Windows Server 2012 vor oder führen Sie **adprep.exe /domainprep** aus|  
|81|Forestprep wurde nicht ausgeführt|Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /forestprep** aus|  
|82|Gesamtstrukturschema-Konflikt|Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /forestprep** aus|  
|83|Nicht unterstützte SKU|*Wahrscheinlich nicht um diesen Fehler zu erhalten.*|  
|84|Es wurde kein Domänencontroller-Konto gefunden|Prüfen Sie, ob das korrekte Benutzerkontensteuerungs-Attribut für die existierenden Domänencontroller gesetzt ist.|  
|85|Fehler beim Auswählen eines Domänencontroller-Kontos für Stufe 2|Wird zurückgegeben, wenn Sie "Vorhandenes Konto verwenden" angeben und entweder kein Konto gefunden wurde oder bei der Kontosuche ein Fehler aufgetreten ist. Stellen Sie sicher, dass Sie das korrekte gestaffelte RODC-Konto angegeben haben|  
|86|Heraufstufung Stufe 2 muss ausgeführt werden|Wird zurückgegeben, wenn Sie einen zusätzlichen Domänencontroller heraufstufen, jedoch bereits ein Konto existiert und "Erneute Installation erlauben" nicht angegeben wurde|  
|87|Ein in Konflikt stehendes Domänencontrollerkonto existiert|Benennen Sie den Computer vor der Heraufstufung um, falls Sie nicht versuchen, an einen nicht belegten Domänencontroller anzufügen. Anfügen an den nicht belegten Domänencontroller Konto mithilfe muss **- Useexistingaccount** und das korrekte schreibgeschützte oder beschreibbare Argument, je nach Kontotyp|  
|88|Der angegebene Serveradmin ist ungültig|Sie haben ein ungültiges Konto für die RODC Admin-Delegierung angegeben. Stellen Sie sicher, dass das angegebene Konto ein gültiger Benutzer ist bzw. zu einer gültigen Gruppe gehört|  
|89|RID-Master für die angegebene Domäne ist offline.|Führen Sie **netdom.exe query fsmo** aus, um den RID-Master zu bestimmen. Bringen Sie diesen online und machen Sie ihn für den Domänencontroller verfügbar, den Sie heraufstufen möchten|  
|90|Domänennamenmaster ist offline.|Führen Sie **netdom.exe query fsmo** aus, um den Domänennamenmaster zu bestimmen. Bringen Sie diesen online und machen Sie ihn für den Domänencontroller verfügbar, den Sie heraufstufen möchten|  
|91|Fehler bei der Ermittlung, ob es sich um einen wow64-Prozess handelt|*Nicht möglich, diese Fehlermeldung ist nicht mehr das Betriebssystem 64-bit*|  
|92|Wow64-Prozess wird nicht unterstützt|*Nicht möglich, diese Fehlermeldung ist nicht mehr das Betriebssystem 64-bit*|  
|93|Domänencontrollerdienst wird nicht ausgeführt für nichterzwungene Herabstufung|Starten Sie den AD DS-Dienst|  
|94|Lokales Admin-Kennwort erfüllt die Anforderung nicht: entweder leer oder nicht benötigt|Geben Sie ein nicht-leeres Kennwort ein und stellen Sie sicher, dass die lokale Kennwortrichtlinie ein Kennwort vorschreibt|  
|95|Letzter Domänencontroller unter Windows Server 2008 oder neuerer Version kann nicht gelöscht werden in der Domäne, in der Live-RODCs existieren|Sie müssen zunächst alle RODCs herabstufen, bevor Sie alle beschreibbaren Domänencontroller unter Windows Server 2008 oder neueren Versionen herabstufen können|  
|96|DS-Binärdateien konnten nicht deinstalliert werden|*Tritt nur bei Dcpromo / unattend, der veraltet ist. Finden Sie die ältere Dokumentation*|  
|97|Version der Gesamtstrukturfunktionsebene ist neuer als die des Betriebssystems der untergeordneten Domäne|Geben Sie eine untergeordnete Domäne mit derselben oder einer höheren Version als der Version der Gesamtstrukturfunktionsebene an|  
|98|Installation/Deinstallation der Komponenten-Binärdate wird ausgeführt.|*Tritt nur bei Dcpromo / unattend, der veraltet ist. Finden Sie die ältere Dokumentation*|  
|99|Die Funktionsebene der Gesamtstruktur ist zu niedrig (Fehler tritt nur unter Windows Server 2012 auf)|Setzen Sie die Gesamtstrukturfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt|  
|100|Die Domänenfunktionsebene ist zu niedrig (Fehler tritt nur unter Windows Server 2012 auf)|Setzen Sie die Domänenfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt|  
  
#### <a name="knownlikely-issues-and-support-scenarios"></a>Bekannte/Häufige Probleme und Support-Szenarien  
Es folgt eine Liste gängiger Probleme beim Windows Server 2012-Entwicklungsprozess. All diese Probleme sind entwurfsbedingt, und es gibt entweder eine gültige Problemumgehung oder eine geeignetere Methode, um diese komplett zu vermeiden. Viele dieser Verhaltensweisen sind identisch unter Windows Server 2008 R2 und älteren Betriebssystemen, haben jedoch durch die neue Version der AD DS-Bereitstellung neue Bedeutung erlangt.  
  
|Problem|Nach der Herabstufung eines Domänencontrollers bleibt DNS ohne Zonen zurück|  
|---------|-----------------------------------------------------------------|  
|Symptome|Server antwortet weiterhin auf DNS-Anfragen, hat jedoch keine Zoneninformationen|  
|Lösung und Hinweise|Entfernen Sie beim Löschen der AD DS-Rolle ebenfalls die DNS-Serverrolle oder markieren Sie den DNS-Serverdienst als deaktiviert. Der DNS-Client darf dabei nicht auf sich selbst als Server zeigen. Falls Sie Windows PowerShell verwenden, führen Sie nach der Herabstufung des Servers den folgenden Befehl aus:<br /><br />Code - deinstallieren-Windowsfeature-dns<br /><br />oder<br /><br />Code - Set-Service-Dns - Starttype deaktiviert<br />Stop-Service-dns|  
  
|Problem|Beim Heraufstufen eines Windows Server 2012 in eine existierende einteilige Domäne wird updatetopleveldomain=1 bzw. allowsinglelabeldnsdomain=1 nicht konfiguriert|  
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|  
|Symptome|Dynamische DNS-Eintragsregistrierung funktioniert nicht|  
|Lösung und Hinweise|Setzen Sie diese Werte über die Netlogon- und DNS-Gruppenrichtlinien. Microsoft hat ab Windows Server 2008 begonnen, die Erstellung einteiliger Domänen zu blockieren. Sie können ADMT oder das Domänenumbenennungstool verwenden, um zu einer erlaubten DNS-Domänenstruktur zu wechseln.|  
  
|Problem|Herabstufung des letzten Domänencontrollers in einer Domäne schlägt fehl, wenn vorab erstellte und nicht belegte RODC-Konten existieren|  
|---------|------------------------------------------------------------------------------------------------------------|  
|Symptome|Herabstufung schlägt mit der folgenden Nachricht fehl:<br /><br />**Dcpromo.General.54**<br /><br />Active Directory-Domänendienste konnten keinen weiteren Active Directory-Domänencontroller finden, um die verbleibenden Daten in der Verzeichnispartition CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com zu übertragen.<br /><br />"Das Format des angegebenen Domänennamens ist ungültig."|  
|Lösung und Hinweise|Entfernen Sie alle verbleibenden vorab erstellten RODC-Konten, bevor Sie eine Domäne herabstufen. Verwenden Sie dazu **Dsa.msc** oder **Ntdsutil.exe metadata cleanup**.|  
  
|Problem|Automatische Gesamtstruktur- und Domänenvorbereitung führt GPPREP nicht aus|  
|---------|---------------------------------------------------------------|  
|Symptome|Domänenübergreifende Planungsfunktion für Gruppenrichtlinien, Richtlinienergebnissatz (Resultant Set of Policy RSOP) Planungsmodus, benötigt ein aktualisiertes Dateisystem und Active Directory-Berechtigungen für existierende Gruppenrichtlinie. Ohne Gpprep können Sie keine domänenübergreifende RSOP-Planung verwenden.|  
|Lösung und Hinweise|Führen Sie **adprep.exe /gpprep** manuell für alle Domänen aus, die nicht zuvor für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Administratoren sollten GPPrep nur einmal über die Lebensdauer einer Domäne ausführen, und nicht bei jedem Upgrade. Dieser Befehl wird beim automatischen adprep nicht ausgeführt, wenn Sie bereits entsprechende benutzerdefinierte Berechtigungen eingestellt haben, da ansonsten der gesamte SYSVOL-Inhalt erneut auf alle Domänencontroller repliziert würde.|  
  
|Problem|Die Install from Media-Prüfung schlägt fehl, wenn ein UNC-Pfad verwendet wird|  
|---------|------------------------------------------------------------------|  
|Symptome|Zurückgegebener Fehler:<br /><br />Code – Medienpfad konnte nicht überprüft werden. Ausnahme, die beim Aufruf von "GetDatabaseInfo" mit "2" Argumenten. Der Ordner ist ungültig.|  
|Lösung und Hinweise|Sie müssen IFM-Dateien auf einem lokalen Laufwerk speichern, nicht auf einem remote UNC-Pfad. Diese beabsichtigte Sperre verhindert die teilweise Heraufstufung von Servern bei Netzwerkunterbrechungen.|  
  
|Problem|DNS-Delegierungswarnung wird bei der Domänencontroller-Heraufstufung zweimal angezeigt|  
|---------|-------------------------------------------------------------------------|  
|Symptome|Zurückgegebene Warnung *zweimal* bei der Ausführung von ADDSDeployment Windows PowerShell:<br /><br />Code - "kann nicht für den DNS-Server keine Delegierung erstellt werden, da die autorisierende übergeordnete Zone nicht gefunden, oder er nicht ausgeführt, die Windows-DNS wird-Server. Wenn Sie mit einer vorhandenen DNS-Infrastruktur integrieren, sollten Sie manuell eine Delegierung an den DNS-Server in der übergeordneten Zone, um sicherzustellen, dass zuverlässige namensauflösung von außerhalb der Domäne erstellen. Andernfalls ist keine Aktion erforderlich."|  
|Lösung und Hinweise|Ignorieren. ADDSDeployment Windows PowerShell zeigt die Warnung zuerst bei der Voraussetzungsprüfung und dann erneut bei der Konfiguration des Domänencontrollers an. Verwenden Sie dsas folgende Argument, falls Sie keine DNS-Delegierung konfigurieren möchten:<br /><br />Code - -creatednsdelegation:$false<br /><br />Überspringen Sie *niemals* die Voraussetzungsprüfung, um diese Nachricht zu unterdrücken|  
  
|Problem|Bei der Angabe von UPN-Anmeldeinformationen oder solchen, die nicht zu einer Domäne gehören, werden bei der Konfiguration irreführende Fehler zurückgegeben|  
|---------|--------------------------------------------------------------------------------------------|  
|Symptome|Server-Manager gibt den folgenden Fehler zurück:<br /><br />Code - Ausnahme beim Aufruf von "DNSOption", "6" Argumente<br /><br />ADDSDeployment Windows PowerShell gibt den folgenden Fehler zurück:<br /><br />Fehler bei der Code - Überprüfung der Benutzerberechtigungen. Sie müssen den Namen der Domäne angeben, zu denen dieses Benutzerkonto gehört.|  
|Lösung und Hinweise|Stellen Sie sicher, dass Sie gültige Domänen-Anmeldeinformationen im Format **domain\user** angegeben haben.|  
  
|Problem|Der Server startet nicht, nachdem die DirectoryServices-DomainController-Rolle mithilfe von Dism.exe entfernt wurde|  
|---------|---------------------------------------------------------------------------------------------------|  
|Symptome|Falls Sie Dism.exe zum Entfernen der AD DS-Rolle verwenden, bevor Sie einen Domänencontroller ordnungsgemäß herabgestuft haben, startet der Server nicht mehr normal und zeigt den folgenden Fehler an:<br /><br />Code - Status: 0x000000000<br />Info: Unerwarteter Fehler ist aufgetreten.|  
|Lösung und Hinweise|Drücken Sie *Umschalt+F8*, um den Verzeichnisdienst-Wiederherstellungsmodus zu starten. Fügen Sie die AD DS-Rolle wieder hinzu und erzwingen Sie die Herabstufung des Domänencontrollers. Alternativ können Sie das Systems mithilfe der Sicherung wiederherstellen. Verwenden Sie niemale Dism.exe zum Entfernen von AD DS-Rollen, da dieses Tool keine Kenntnis von Domänencontrollern hat.|  
  
|Problem|Die Installation einer neuen Gesamtstruktur mit dem Gesamtstrukturmodus Win2012 schlägt fehl|  
|---------|--------------------------------------------------------------------|  
|Symptome|Bei der Heraufstufung mit ADDSDeployment Windows PowerShell wird der folgende Fehler zurückgegeben:<br /><br />Code -  Test.VerifyDcPromoCore.DCPromo.General.74<br /><br />Fehler bei der Überprüfung der Voraussetzungen für die Domänencontroller-heraufstufung. Die angegebene Domänenfunktionsebene ist ungültig.|  
|Lösung und Hinweise|Verwenden Sie die Gesamtstrukturfunktionsebene Win2012 nur, wenn Sie *ebenfalls* die Domänenfunktionsebene Win2012 angeben. Hier ist ein Beispiel, das fehlerfrei funktioniert:<br /><br />Code - - Gesamtstrukturmodus Win2012 - Domainmode Win2012]|  
  
|||  
|-|-|  
|Problem|Wenn Sie im Bereich Install from Media auf "Prüfen" klicken, geschieht nichts|  
|Symptome|Wenn Sie einen Pfad zu einem IFM-Ordner angeben, wird beim Klicken auf die Schaltfläche **Prüfen** keine Nachricht zurückgegeben.|  
|Lösung und Hinweise|Die Schaltfläche **Prüfen** gibt nur Fehler zurück, wenn ein Problem vorliegt. Andernfalls wird die Schaltfläche **Weiter** aktiviert, falls Sie einen IFM-Pfad angegeben haben. Sie müssen **Prüfen** anklicken, um fortfahren zu können, wenn Sie IFM ausgewählt haben.|  
  
|||  
|-|-|  
|Problem|Bei der Herabstufung mit Server-Manager wird vor dem Abschluss kein Feedback zurückgegeben.|  
|Symptome|Wenn Sie Server-Manager zum Entfernen der AD DS-Rolle und zum Herabstufen eines Domänencontrollers verwenden, erhalten Sie keinerlei Feedback, bevor die Herabstufung fehlschlägt bzw. abgeschlossen ist.|  
|Lösung und Hinweise|Dies ist eine Einschränkung von Server-Manager. Verwenden Sie das ADDSDeployment Windows PowerShell-Cmdlet, um Feedback zu erhalten:<br /><br />Code - deinstallieren-addsdomaincontroller|  
  
|||  
|-|-|  
|Problem|Die Install from Media-Prüfung erkennt nicht, dass ein RODC-Medium für einen beschreibbaren Domänencontroller angegeben wurde, oder umgekehrt.|  
|Symptome|Wenn Sie einen neuen Domänencontroller mit IFM heraufstufen und dabei ein RODC-Medium für einen beschreibbaren Domänencontroller oder ein RWDC-Medium für einen RODC angeben, gibt die "Prüfen"-Schaltfläche keinen Fehler zurück. Später schlägt die Heraufstufung dann mit dem folgenden Fehler fehl:<br /><br />Code - Fehler beim Versuch, diesen Computer als Domänencontroller konfigurieren. <br />Die Install From Media heraufstufung eines schreibgeschützten Domänencontrollers kann nicht gestartet werden, da die angegebenen Quelldatenbank nicht zulässig ist. Nur für Datenbanken von anderen RODCs können für die IFM-heraufstufung eines RODC verwendet werden.|  
|Lösung und Hinweise|Die Prüfung prüft nur die Gesamtintegrität von IFM. Verwenden Sie immer den korrekten IFM-Typ für den jeweiligen Server. Starten Sie den Server neu, bevor Sie die Heraufstufung erneut mit dem korrekten Medium vornehmen.|  
  
|||  
|-|-|  
|Problem|Die Heraufstufung eines RODC mit einem vorab erstellten Computerkonto schlägt fehl|  
|Symptome|Beim Heraufstufen eines neuen RODC mit ADDSDeployment Windows PowerShell und einem gestaffelten Computerkonto erhalten Sie den folgenden Fehler:<br /><br />Code - Parametersatz kann nicht mit den angegebenen benannten Parametern aufgelöst werden.    <br />InvalidArgument: ParameterBindingException<br />    + FullyQualifiedErrorId : AmbiguousParameterSet,Microsoft.DirectoryServices.Deployment.PowerShell.Commands.Install|  
|Lösung und Hinweise|Geben Sie keine Parameter an, die bereits in einem vorab erstellten RODC-Konto vorhanden sind. Dazu gehören:<br /><br />Code - - readonlyreplica<br />-installdns<br />-donotconfigureglobalcatalog<br />-sitename<br />-installdns|  
  
|||  
|-|-|  
|Problem|Beim Aktivieren/Deaktivieren der Option "Zielserver bei Bedarf automatisch neu starten" geschieht nichts|  
|Symptome|Aktivieren (bzw. nicht auswählen) die Server-Manager-Option **automatisch neu starten Zielserver bei Bedarf** Whendemoting eines Domänencontrollers durch Entfernen der Rolle, der Server immer neu gestartet, unabhängig von Ihrer Auswahl.|  
|Lösung und Hinweise|Dies ist beabsichtigt. Der Herabstufungsprozess startet den Server unabhängig von dieser Einstellung immer neu.|  
  
|||  
|-|-|  
|Problem|Dcpromo.log enthält die Zeile "[Fehler] Sicherheitseinstellung für Serverdateien fehlgeschlagen mit 2"|  
|Symptome|Die Herabstufung eines Domänencontrollers läuft ohne Fehler ab, aber das dcpromo-Protokoll enthält den folgenden Fehler:<br /><br />Code - [Error] Festlegen der Sicherheit für Serverdateien fehlgeschlagen mit 2|  
|Lösung und Hinweise|Ignorieren, dieser Fehler ist zu erwarten und kosmetischer Natur.|  
  
|||  
|-|-|  
|Problem|Bei der adprep-Voraussetzungsprüfung wird der Fehler "Für die Domäne konnte keine Exchange-Schemakonfliktüberprüfung ausgeführt werden" angezeigt|  
|Symptome|Beim Versuch, einen Windows Server 2012-Domänencontroller in eine existierende Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2-Gesamtstruktur heraufzustufen, wird bei der Voraussetzungsprüfung der folgende Fehler angezeigt:<br /><br />Fehler bei der Code - Überprüfung der Voraussetzungen für die AD-datenvorbereitung. Kann nicht ausgeführt werden Exchange-schemakonfliktüberprüfung für Domäne *<domain name>* (Ausnahme: der RPC-Server ist nicht verfügbar)<br /><br />adprep.log enthält den folgenden Fehler:<br /><br />Code - Adprep Daten konnten nicht vom Server abgerufen *<domain controller>*<br /><br />durch die Windows-Verwaltungsinstrumentation (WMI).|  
|Lösung und Hinweise|Der neue Domänencontroller hat keinen Zugriff auf WMI über die DCOM/RPC-Protokolle für die existierenden Domänencontroller. Aktuell existieren drei Ursachen für diesen Fehler:<br /><br />– Eine Firewall blockiert den Zugriff auf den existierenden Domänencontrollern<br /><br />-Das NETZWERKDIENST-Konto fehlt der "Anmelden als Dienst" (SeServiceLogonRight)-Berechtigungen auf den existierenden Domänencontrollern<br /><br />-Für Domänencontroller NTLM deaktiviert ist, mithilfe von Sicherheitsrichtlinien, die in beschriebenen [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(WS.10).aspx)|  
  
|||  
|-|-|  
|Problem|Beim Erstellen einer neuen Gesamtstruktur wird immer eine DNS-Warnung angezeigt|  
|Symptome|Wenn Sie eine neue AD DS-Gesamtstruktur erstellen und die DNS-Zone auf dem neuen Domänencontroller für sich selbst erstellen, erhalten Sie immer die folgende Warnmeldung:<br /><br />In der DNS-Konfiguration wurde Code – ein Fehler erkannt. <br />Keiner der von diesem Computer verwendet DNS-Server hat innerhalb des Timeoutintervalls geantwortet.<br />(Fehlercode: 0x000005B4 "ERROR_TIMEOUT")|  
|Lösung und Hinweise|Ignorieren. Diese Warnung ist beabsichtigt für den ersten Domänencontroller in der Stammdomäne einer neuen Gesamtstruktur, für den Fall, dass Sie auf einen existierenden DNS-Server und eine existierende Zone verweisen möchten.|  
  
|||  
|-|-|  
|Problem|Das Windows PowerShell-Argument -whatif liefert falsche DNS-Serverinformationen zurück|  
|Symptome|Falls Sie das Argument **-whatif** beim Konfigurieren eines Domänencontrollers mit implizitem oder explizitem **-installdns:$true** verwenden, wird die folgende Ausgabe angezeigt:<br /><br />Code - "DNS-Server: No"|  
|Lösung und Hinweise|Ignorieren. DNS ist installiert und funktioniert korrekt.|  
  
|||  
|-|-|  
|Problem|Nach der Heraufstufung schlägt die Anmeldung fehl mit "Zum Verarbeiten des Befehls ist nicht genügend Speicherplatz verfügbar"|  
|Symptome|Wenn Sie sich nach der Heraufstufung eines neuen Domänencontrollers abmelden und anschließend versuchen, sich interaktiv anzumelden, erhalten Sie den folgenden Fehler:<br /><br />Code - steht nicht genügend Speicher zum Verarbeiten des Befehls|  
|Lösung und Hinweise|Der Domänencontroller wurde nach der Heraufstufung nicht neu gestartet, entweder aufgrund eines Fehlers oder weil Sie das ADDSDeployment Windows PowerShell-Argument **-norebootoncompletion** verwendet haben. Starten Sie den Domänencontroller neu.|  
  
|||  
|-|-|  
|Problem|Schaltfläche "Weiter" ist auf der Seite mit den Domänencontrolleroptionen nicht verfügbar|  
|Symptome|Die Schaltfläche **Weiter** auf der Seite **Domänencontrolleroptionen** in Server-Manager ist nicht verfügbar, obwohl Sie ein Kennwort eingestellt haben. Das Menü **Sitename** enthält keine Sites.|  
|Lösung und Hinweise|Sie haben mehrere AD DS-Sites, und mindestens einer dieser Sites fehlen Subnetze. Dieser zukünftige Domänencontroller gehört zu einem dieser Subnetze. Wählen Sie das Subnetz aus dem Dropdown-Menü Sitename manuell aus. Sie sollten außerdem alle AD-Sites mithilfe von DSSITE.MSC oder mit dem folgenden Windows PowerShell-Befehl prüfen, um alle fehlenden Subnetze zu identifizieren:<br /><br />Code - Get-Adreplicationsite – Filter *-Eigenschaft Subnetze &#124; Where-Object {! $_.subnets - Eq "\*"} &#124; Format-Table-Name|  
  
|||  
|-|-|  
|Problem|Herauf- oder Herabstufung schlägt fehl mit "Der Dienst kann nicht gestartet werden"|  
|Symptome|Beim Heraufstufen, Herabstufen oder Klonen eines Domänencontrollers erhalten Sie den folgenden Fehler:<br /><br />Code - der Dienst kann nicht gestartet werden, entweder weil ist deaktiviert "oder" Es wurde keine aktivierten Geräte zugeordnet"(0x80070422)<br /><br />Der Fehler kann interaktiv oder als Ereignis angezeigt oder in eines der Protokolle wie z. B. dcpromoui.log oder dcpromo.log geschrieben werden|  
|Lösung und Hinweise|Der DS-Rollenserverdienst (DsRoleSvc) ist deaktiviert. Dieser Dienst wird bei der Installation der AD DS-Rolle automatisch installiert und auf den Starttyp manuell gesetzt. Deaktivieren Sie diesen Dienst nicht. Setzen Sie den Starttyp wieder auf manuell und erlauben Sie den DS-Rollenoperationen, den Dienst bei Bedarf zu starten und anzuhalten. Dieses Verhalten ist entwurfsbedingt.|  
  
|||  
|-|-|  
|Problem|Sie erhalten weiterhin eine Warnung von Server-Manager, dass Sie den Domänencontroller heraufstufen müssen|  
|Symptome|Wenn Sie einen Domänencontroller mit dem veralteten Befehl dcpromo.exe /unattend heraufstufen oder ein Upgrade eines existierenden Windows Server 2008 R2-Domänencontrollers auf Windows Server 2012 vornehmen, zeigt Server-Manager weiterhin die Konfigurationsaufgabe **Server zu einem Domänencontroller heraufstufen** zur Ausführung nach der Heraufstufung an.|  
|Lösung und Hinweise|Wenn Sie auf den Warn-Link klicken, verschwindet die Nachricht endgültig. Dieses Verhalten ist zu erwarten und kosmetischer Natur.|  
  
|||  
|-|-|  
|Problem|Fehlende Rolleninstallation für Server-Manager-Bereitstellungsskript|  
|Symptome|Wenn Sie einen Domänencontroller mithilfe von Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, werden Cmdlet und Argumente für die Rolleninstallation (install-windowsfeature -name ad-domain-services -includemanagementtools) nicht mitgespeichert. Ohne die Rolle kann der Domänencontroller nicht konfiguriert werden.|  
|Lösung und Hinweise|Fügen Sie Cmdlet und Argumente manuell zu Ihren Skripts hinzu. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  
  
|||  
|-|-|  
|Problem|Server-Manager-Bereitstellungsskript ist keine PS1-Datei|  
|Symptome|Wenn Sie einen Domänencontroller mithilfe von Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, erhält die Datei einen zufälligen temporären Namen und wird nicht als PS1-Datei benannt.|  
|Lösung und Hinweise|Benennen Sie die Datei manuell um. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  
  
|Problem|Dcpromo /unattend erlaubt nicht unterstützte funktionale Ebenen|  
|-|-|  
|Symptome|Wenn Sie einen Domänencontroller mithilfe von dcpromo /unattend und der folgenden Beispiel-Antwortdatei heraufstufen:<br /><br />Code:<br /><br />[DCInstall]<br />NewDomain=Forest<br /><br />ReplicaOrNewDomain=Domain<br /><br />NewDomainDNSName=corp.contoso.com<br /><br />SafeModeAdminPassword=Safepassword@6<br /><br />DomainNetbiosName=corp<br /><br />DNSOnNetwork = Ja<br /><br />AutoConfigDNS=Yes<br /><br />RebootOnSuccess NoAndNoPromptEither =<br /><br />RebootOnCompletion=No<br /><br />*DomainLevel=0*<br /><br />*ForestLevel=0*<br /><br />Die Heraufstufung schlägt mit den folgenden Fehlern in dcpromoui.log fehl:<br /><br />Code - dcpromoui EA4.5B8 0089 13:31:50.783       Enter CArgumentsSpec::ValidateArgument DomainLevel<br /><br />Dcpromoui EA4.5B8 008A 13:31:50.783 DomainLevel Wert ist 0<br /><br />Dcpromoui EA4.5B8 008 b 13:31:50.783 Exitcode wird 77<br /><br />Dcpromoui EA4.5B8 008C 13:31:50.783 das angegebene Argument ist ungültig.<br /><br />Dcpromoui EA4.5B8 008D 13:31:50.783 schließende log<br /><br />Dcpromoui EA4.5B8 0032 13:31:50.830 Exitcode wird 77<br /><br />Level 0 steht für Windows 2000 und wird unter Windows Server 2012 nicht unterstützt.|  
|Lösung und Hinweise|Sie sollten den veralteten Befehl dcpromo /unattend nicht verwenden, da dieser die Angabe ungültiger Einstellungen erlaubt, die später zu Fehlern führen. Dieses Verhalten ist zu erwarten und entwurfsbedingt.|  

|Problem|Heraufstufung "hängt" über das Erstellen von NTDS-Einstellungsobjekt, niemals abgeschlossen wird.|  
|-|-|  
|Symptome|Wenn Sie ein Replikat-DC oder RODC heraufstufen, "erstellen NTDS-Einstellungsobjekts" erreicht die heraufstufung und nie fortgesetzt wird oder abgeschlossen ist. Die Protokolle werden ebenfalls nicht mehr aktualisiert.|  
|Lösung und Hinweise|Dies ist ein bekanntes Problem und entsteht, wenn die Anmeldeinformationen des integrierten lokalen Administratorkontos mit dem Kennwort des integrierten Domänenadministratorkontos angegeben werden. Dabei entsteht ein Fehler im zentralen Setupmodul und das Modul wird in eine Art Endlosschleife versetzt. Dies wird erwartet, – wenn auch nicht erwünscht - Verhalten.<br /><br />So reparieren Sie den Server:<br /><br />1.  Führen Sie einen Neustart durch.<br /><br />1.  In AD Löschen dieses Servers Mitglieds-Computerkonto (es wird nicht noch kein Domänencontroller-Konto.)<br /><br />1.  Erzwingen Sie eine Trennung des Servers von der Domäne<br /><br />1.  Entfernen Sie die AD DS-Rolle auf dem Server.<br /><br />1.  Neustart<br /><br />1.  Erneut die AD DS-Rolle, und wiederholen Promotion hinzufügen, um sicherzustellen, dass Sie immer angeben der ***Domain\admin*** Anmeldeinformationen heraufstufung an, und nicht nur die integrierte lokale Administratorkonto im Format|  
