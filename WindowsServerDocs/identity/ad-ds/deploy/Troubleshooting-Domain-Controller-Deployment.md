---
ms.assetid: 5ab76733-804d-4f30-bee6-cb672ad5075a
title: Problembehandlung der Domänencontrollerbereitstellung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/20/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e3f215abaccbd1f95ee46eca93a573aa1db9e065
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519408"
---
# <a name="troubleshooting-domain-controller-deployment"></a>Problembehandlung der Domänencontrollerbereitstellung

>Gilt für: Windows Server 2016

Dieser Artikel behandelt detaillierte Methoden für die Problembehandlung bei Konfiguration und Bereitstellung von Domänencontrollern.

## <a name="introduction-to-troubleshooting"></a>Einführung in die Problembehandlung

![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/adds_deploy_troubleshooting.png)

## <a name="built-in-logs-for-troubleshooting"></a>Integrierte Protokolle zur Problembehandlung

Die integrierten Protokolle sind das wichtigste Hilfsmittel für die Fehlerbehebung bei Herauf- und Herabstufung von Domänencontrollern. All diese Protokolle sind standardmäßig aktiviert und für maximale Ausführlichkeit konfiguriert.

| Phase | Log |
|--|--|
| Server-Manager- bzw. ADDSDeployment-Windows PowerShell-Operationen | -%systemroot%\debug\dcpromoui.log<p>-%systemroot%\debug\dcpromoui *. log |
| Installation/Heraufstufung des Domänencontrollers | -%systemroot%\debug\dcpromo.log<p>-%systemroot%\debug\dcpromo *. log<p>-Ereignisviewer\windows-Protokolle\System<p>-Ereignisviewer\windows-Protokolle\Anwendung<p>-Ereignisviewer\anwendungs-und dienstprotokolle\verzeichnisdienst<p>-Ereignisviewer\anwendungs-und dienstprotokolle\datei Replikations Dienst<p>-Ereignisviewer\anwendungs-und dienstprotokolle\dfs-Replikation |
| Upgrade von Gesamtstruktur oder Domäne | -%systemroot%\debug\adprep \\ <datetime> \adprep.log<p>-%systemroot%\debug\adprep \\ <datetime> \csv.log<p>-%systemroot%\debug\adprep \\ <datetime> \dspecup.log<p>-%systemroot%\debug\adprep \\ <datetime> \ldif.log * |
| Server-Manager ADDSDeployment Windows PowerShell Bereitstellungs-Engine | -Ereignisviewer\anwendungs-und dienstprotokolle\microsoft\windows\directoriyservices-deployment\operational |
| Windows-Wartung | -%systemroot%\Logs\CBS\\*<p>-% systemroot% \servicing\sessions\sessions.xml<p>-%systemroot%\winsxs\poqexec.log<p>-% systemroot% \winsxs\pending.xml |

### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Konfiguration von Domänencontrollern

Verwenden Sie zum Beheben von Problemen, die nicht von den Protokollen erklärt werden, die folgenden Tools als Ausgangspunkt:

-   Dcdiag.exe

-   Repadmin.exe

-   [AutoRuns.exe](/sysinternals/downloads/autoruns), Task-Manager und MSInfo32.exe

-   [Network Monitor 3.4](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=4865) (oder ein Drittanbietertool zu Netzwerkerfassung und -analyse)

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

## <a name="troubleshooting-events-and-error-messages"></a>Problembehandlung bei Ereignissen und Fehlermeldungen

Bei der Herauf- und Herabstufung von Domänencontrollern wird am Ende der Operation immer ein Code zurückgegeben, und im Gegensatz zu vielen Programmen steht der Code null nicht für Erfolg. Sie haben mehrere Optionen, um den abschließenden Code bei einer Domänencontroller-Konfiguration abzurufen:

1. Wenn Sie Server-Manager verwenden, wird das Heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart angezeigt.

2. Wenn Sie ADDSDeployment Windows PowerShell verwenden, wird das Heraufstufungsergebnis in den zehn Sekunden vor dem automatischen Neustart angezeigt. Alternativ können Sie sich entscheiden, nach Abschluss keinen automatischen Neustart durchzuführen. Sie sollten die **Format-List**-Pipeline hinzufügen, um die Ausgabe leichter lesbar zu machen. Beispiel:

   ```
   Install-addsdomaincontroller <options> -norebootoncompletion:$true | format-list
   ```

   Im Fehlerfall bei der Voraussetzungsprüfung wird kein Neustart durchgeführt, daher sind diese Fehler in jedem Fall sichtbar. Beispiel:

   ![Problembehandlung](media/Troubleshooting-Domain-Controller-Deployment/ADDS_PSPrereqError.png)

3. Prüfen Sie in jedem Szenario die Dateien dcpromo.log und dcpromoui.log.

   > [!NOTE]
   > Manche der unten genannten Fehler können aufgrund von Konfigurationsänderungen an Betriebssystem und Domänencontroller in späteren Betriebssystemen nicht mehr auftreten. Der neue ADDSDeployment Windows PowerShell-Code verhindert ebenfalls bestimmte Fehler im Gegensatz zu dcpromo.exe /unattend. Dies ist ein weiterer wichtiger Grund, warum Sie Ihre gesamte aktuelle Automatisierung vom veralteten DCPromo auf ADDSDeployment Windows PowerShell umstellen sollten.

### <a name="promotion-and-demotion-success-codes"></a>Erfolgs Codes für herauf Stufung und Herabstufung

| Fehlercode | Erklärung | Hinweis |
|--|--|--|
| 1 | Ende, Erfolg | Der Neustart muss dennoch ausgeführt werden. Dieser Code weist lediglich darauf hin, dass die Kennzeichnung für den automatischen Neustart entfernt wurde |
| 2 | Ende, Erfolg, Neustart erforderlich |  |
| 3 | Ende, Erfolg mit nicht-kritischem Fehler | Wird normalerweise bei einer DNS-Delegierungswarnung zurückgegeben. Verwenden Sie ohne DNS-Delegierung den folgenden Parameter:<p>-creatednsdelegation:$false |
| 4 | Ende, Erfolg mit nicht-kritischem Fehler, Neustart erforderlich | Wird normalerweise bei einer DNS-Delegierungswarnung zurückgegeben. Verwenden Sie ohne DNS-Delegierung den folgenden Parameter:<p>-creatednsdelegation:$false |

### <a name="promotion-and-demotion-failure-codes"></a>Fehlercodes für herauf Stufung und Herabstufung

Bei Herauf- und Herabstufung werden die folgenden Ergebnis-Fehlercodes zurückgegeben. Zusätzlich existiert vermutlich eine erweiterte Fehlermeldung. Lesen Sie stets die gesamte Fehlermeldung sorgfältig, nicht nur den numerischen Teil.

| Fehlercode | Erklärung | Lösungsvorschlag |
|--|--|--|
| 11 | Domänencontroller-Heraufstufung wird bereits ausgeführt | Führen Sie niemals mehr als eine Domänencontroller-Heraufstufung gleichzeitig für denselben Zielcomputer aus |
| 12 | Benutzer muss Administrator sein | Melden Sie sich mit einem integrierten Administratorkonto an und heben Sie die Rechte mit UAC an |
| 13 | Zertifizierungsstelle ist installiert | Sie können diesen Domänencontroller nicht herabstufen, da dieser auch als Zertifizierungsstelle fungiert. Entfernen Sie die ZS erst, nachdem Sie deren Nutzung sorgfältig erfasst haben. Falls die ZS Zertifikate ausstellt, wird deren Entfernung zu einem Ausfall führen. Es wird davon abgeraten, ZS auf Domänencontrollern zu betreiben |
| 14 | Ausführen im abgesicherten Modus | Starten Sie den Server im normalen Modus |
| 15 | Die Rollenänderung wird durchgeführt, oder der Computer muss neu gestartet werden | Sie müssen den Server vor der Heraufstufung neu starten (aufgrund vorheriger Konfigurationsänderungen) |
| 16 | Ausführung auf falscher Plattform | *Dieser Fehler ist sehr unwahrscheinlich* |
| 17 | Keine NTFS 5-Laufwerke vorhanden | Dieser Fehler kann unter Windows Server 2012 nicht auftreten, da in diesem Fall zumindest %systemdrive% mit NTFS formatiert sein muss |
| 18 | Nicht genügend Speicher in "windir" | Geben Sie mithilfe von cleanmgr.exe Speicherplatz auf dem %systemdrive%-Laufwerk frei |
| 19 | Namensänderung steht aus. Neustart erforderlich | Starten Sie den Server neu |
| 20 | Ungültige Syntax in Computername | Benennen Sie den Computer mit einem gültigen Namen |
| 21 | Dieser Domänencontroller enthält FSMO-Rollen, ist ein globaler Katalog und/oder ein DNS-Server | Add **-demoteoperationmasterrole** bei Verwendung von **-forceremoval**. |
| 22 | TCP/IP muss installiert werden oder funktioniert nicht | Prüfen Sie, ob TCP/IP auf dem Computer konfiguriert und gebunden ist und korrekt funktioniert |
| 23 | DNS-Client muss zunächst konfiguriert werden | Konfigurieren Sie beim Hinzufügen eines neuen Domänencontrollers zu einer Domäne einen primären DNS-Server |
| 24 | Eingegebene Anmeldeinformationen sind ungültig oder unvollständig | Überprüfen Sie Benutzername und Kennwort |
| 25 | Domänencontroller für die angegebene Domäne wurde nicht gefunden | Prüfen Sie DNS-Clienteinstellungen und Firewallregeln |
| 26 | Liste der Domänen konnte nicht aus der Gesamtstruktur abgerufen werden | Prüfen Sie DNS-Clienteinstellungen, LDAP-Funktionalität und Firewallregeln |
| 27 | Fehlender Domänenname | Geben Sie bei Herauf- und Herabstufung eine Domäne an |
| 28 | Ungültiger Domänenname | Wählen Sie bei der Heraufstufung einen anderen, gültigen Domänennamen aus |
| 29 | Übergeordnete Domäne existiert nicht | Prüfen Sie die bei der Erstellung einer neuen untergeordneten Domäne oder Gesamtstrukturdomäne angegebene übergeordnete Domäne |
| 30 | Domäne nicht Teil der Gesamtstruktur | Prüfen Sie den angegebenen Domänennamen |
| 31 | Untergeordnete Domäne existiert bereits | Geben Sie einen anderen Domänennamen an |
| 32 | Ungültiger NetBIOS-Domänenname | Geben Sie einen gültigen NetBIOS-Domänennamen an |
| 33 | Pfad der IFM-Dateien ist ungültig | Prüfen Sie Ihren Pfad zum Install From Media-Ordner |
| 34 | Ungültige IFM-Datenbank | Verwenden SIe die korrekte Install From Media-Option für Betriebssystem und Rolle (gleiche Betriebssystem-Version, gleicher Typ von Domänencontroller - RODC oder RWDC) |
| 35 | SYSKEY fehlt | Install from Media ist verschlüsselt, und Sie müssen einen gültigen SYSKEY eingeben |
| 37 | Ungültiger Pfad für NTDS-Datenbank oder deren Protokolle | Ändern Sie die Pfade für Datenbank und Protokolle zu einem festen NTFS-Laufwerk (kein zugeordnetes Laufwerk oder UNC-Pfad) |
| 38 | Nicht genügend Speicherplatz für NTDS-Datenbank oder Protokolle | Geben Sie Speicherplatz mit cleanmgr.exe frei, erweitern Sie den Speicherplatz oder schaffen Sie Speicherplatz, indem Sie nicht benötigte Daten an einen anderen Ort verschieben |
| 39 | Ungültiger Pfad für SYSVOL | Ändern Sie den SYSVOL-Pfad zu einem festen NTFS-Laufwerk (kein zugeordnetes Laufwerk oder UNC-Pfad) |
| 40 | Ungültiger Sitename | Geben Sie einen existierenden Sitenamen an |
| 41 | Kennwort für abgesicherten Modus erforderlich | Geben Sie ein Kennwort für das DSRM-Konto ein. Dieses Kennwort darf unabhängig von der Kennwortrichtlinie nicht leer sein |
| 42 | Kennwort für abgesicherten Modus erfüllt die Kriterien nicht (nur Heraufstufung) | Geben Sie ein Kennwort für das DSRM-Konto ein, das die Regeln für die Kennwortrichtlinie erfüllt |
| 43 | Admin-Kennwort erfüllt die Kriterien nicht (nur Heraufstufung) | Geben Sie ein Kennwort für das lokale Administratorkonto ein, das die Regeln für die Kennwortrichtlinie erfüllt |
| 44 | Der angegebene Name für die Gesamtstruktur ist ungültig | Geben Sie einen gültigen DNS-Namen für die Gesamtstruktur-Stammdomäne an |
| 45 | Eine Gesamtstruktur mit diesem Namen ist bereits vorhanden | Wählen Sie einen anderen DNS-Namen für die Gesamtstruktur-Stammdomäne |
| 46 | Der angegebene Name für die Struktur ist ungültig | Geben Sie einen gültigen DNS-Domänennamen für die Struktur an |
| 47 | Eine Struktur mit diesem Namen ist bereits vorhanden | Wählen Sie einen anderen DNS-Domänennamen für die Struktur |
| 48 | Der Strukturname passt nicht in die Gesamtstruktur | Wählen Sie einen anderen DNS-Domänennamen für die Struktur |
| 49 | Die angegebene Domäne existiert nicht | Prüfen Sie den eingegebenen Domänennamen |
| 50 | Bei der Herabstufung wurde ein nicht angegebener letzter Domänencontroller entdeckt bzw. der letzte Domänencontroller wurde fälschlicherweise angegeben | Geben Sie **Letzter Domänencontroller in der Domäne** (**-lastdomaincontrollerindomain**) nur an, wenn dieser Wert wahr ist. Verwenden Sie **-ignorelastdcindomainmismatch** zum überschreiben, wenn dies wirklich der letzte Domänen Controller ist und Phantom-Domänen Controller-Metadaten vorhanden sind. |
| 51 | Anwendungspartitionen existieren auf diesem Domänencontroller | Markieren Sie **Anwendungspartitionen entfernen** (**-removeapplicationpartitions**) |
| 52 | Benötigtes Befehlszeilenargument fehlt (d. h. eine Antwortdatei muss in der Befehlszeile angegeben werden) | *Wird nur mit dcpromo/unattend erkannt, das veraltet ist. Siehe ältere Dokumentation* |
| 53 | Herauf-/Herabstufung fehlgeschlagen, Computer muss zur Bereinigung neu gestartet werden | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 54 | Herauf-/Herabstufung fehlgeschlagen | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 55 | Herauf-/Herabstufung wurde vom Benutzer abgebrochen | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 56 | Herauf-/Herabstufung wurde vom Benutzer abgebrochen, Computer muss zur Bereinigung neu gestartet werden | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 58 | Bei der RODC-Heraufstufung muss ein Sitename angegeben werden | Sie müssen eine Site für einen RODC angeben, da dieser nicht wie bei RWDC automatisch erkannt wird |
| 59 | Bei der Herabstufung ist dieser Domänencontroller der letzte DNS-Server für eine der betroffenen Zonen | Markieren Sie die Opeion **Letzter DNS-Server in der Domäne** oder verwenden Sie **-ignorelastdnsserverfordomain** |
| 60 | Für die Heraufstufung des RODC muss ein Domänencontroller unter Windows Server 2008 oder neuer in der Domäne vorhanden sein | Stufen Sie mindestens einen beschreibbaren Domänencontroller unter Windows Server 2008 oder neuer herauf |
| 61 | Sie können Active Directory-Domänendienste mit DNS nicht in einer existierenden Domäne installieren, die nicht bereits DNS hostet | *Dieser Fehler kann nicht auftreten* |
| 62 | Antwortdatei hat keinen [DCInstall]-Bereich | *Wird nur mit dcpromo/unattend erkannt, das veraltet ist. Siehe ältere Dokumentation.* |
| 63 | Die Funktionsebene der Gesamtstruktur entspricht nicht mindestens Windows Server 2003 | Setzen Sie die Domänenfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt |
| 64 | Heraufstufung wegen Fehler bei der Erkennung der Komponenten-Binärdatei fehlgeschlagen | Installieren Sie die AD DS-Rolle |
| 65 | Heraufstufung wegen Fehler bei der Installation der Komponenten-Binärdatei fehlgeschlagen | Installieren Sie die AD DS-Rolle |
| 66 | Heraufstufung wegen Fehler bei der Erkennung des Betriebssystems fehlgeschlagen | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle. Der Server gibt seine Betriebssystem-Version nicht zurück. Der Computer muss vermutlich neu installiert werden, da seine Gesamtintegrität wahrscheinlich beschädigt ist |
| 68 | Ungültiger Replikationspartner | Verwenden Sie repadmin.exe oder die Windows PowerShell **Get-adreplication \\ ** zum Überprüfen der Integrität des \* Partner Domänen Controllers. |
| 69 | Der benötigte Port wird bereits von einer anderen Anwendung verwendet | Verwenden Sie **netstat.exe -anob**, um Prozesse zu ermitteln, die fälschlicherweise reservierte AD DS-Ports verwenden |
| 70 | Der Controller der Gesamtstruktur-Stammdomäne muss ein globaler Katalogserver sein | *Wird nur mit dcpromo/unattend erkannt, das veraltet ist. Siehe ältere Dokumentation* |
| 71 | DNS-Server ist bereits installiert | Geben Sie die Option "DNS installieren" (**-installDNS**) nicht an, falls der DNS-Dienst bereits installiert ist |
| 72 | Computer führt Remotedesktopdienste nicht im Admin-Modus aus | Dieser Domänencontroller kann nicht heraufgestuft werden, da er auch als RDS-Server für mehr als zwei Admin-Benutzer konfiguriert ist. Entfernen Sie RDS erst, nachdem Sie dessen Nutzung sorgfältig erfasst haben. Falls dieser Dienst von Anwendungen oder Endbenutzern verwendet wird, führt seine Entfernung zu einem Ausfall |
| 73 | Die angegebene Gesamtstrukturfunktionsebene ist ungültig. | Geben Sie eine gültige Gesamtstrukturfunktionsebene an |
| 74 | Die angegebene Domänenfunktionsebene ist ungültig. | Geben Sie eine gültige Domänenfunktionsebene an |
| 75 | Standard-Kennwortreplikationsrichtlinie konnte nicht ermittelt werden. | Vergewissern Sie sich, dass die RODC-Kennwortreplikationsrichtlinie existiert und zugänglich ist |
| 76 | Angegebene replizierte/nicht replizierte Sicherheitsgruppen sind ungültig | Prüfen Sie, ob Sie bei der Angabe einer Kennwortreplikationsrichtlinie gültige Domänen- und Benutzerkonten angegeben haben |
| 77 | Das angegebene Argument ist ungültig | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 78 | Fehler bei der Prüfung der Active Directory-Gesamtstruktur | Untersuchen Sie erweiterte Fehlerbeschreibung und Protokolle |
| 79 | RODC kann nicht heraufgestuft werden, da rodcprep nicht ausgeführt wurde | Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /rodcprep** aus |
| 80 | Domainprep wurde nicht ausgeführt | Bereiten Sie die Domäne mit Windows Server 2012 vor oder führen Sie **adprep.exe /domainprep** aus |
| 81 | Forestprep wurde nicht ausgeführt | Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /forestprep** aus |
| 82 | Gesamtstrukturschema-Konflikt | Bereiten Sie die Gesamtstruktur mit Windows Server 2012 vor oder führen Sie **adprep.exe /forestprep** aus |
| 83 | Nicht unterstützte SKU | *Dieser Fehler ist sehr unwahrscheinlich* |
| 84 | Es wurde kein Domänencontroller-Konto gefunden | Prüfen Sie, ob das korrekte Benutzerkontensteuerungs-Attribut für die existierenden Domänencontroller gesetzt ist. |
| 85 | Fehler beim Auswählen eines Domänencontroller-Kontos für Stufe 2 | Wird zurückgegeben, wenn Sie "Vorhandenes Konto verwenden" angeben und entweder kein Konto gefunden wurde oder bei der Kontosuche ein Fehler aufgetreten ist. Stellen Sie sicher, dass Sie das korrekte gestaffelte RODC-Konto angegeben haben |
| 86 | Heraufstufung Stufe 2 muss ausgeführt werden | Wird zurückgegeben, wenn Sie einen zusätzlichen Domänencontroller heraufstufen, jedoch bereits ein Konto existiert und "Erneute Installation erlauben" nicht angegeben wurde |
| 87 | Ein in Konflikt stehendes Domänencontrollerkonto existiert | Benennen Sie den Computer vor der Heraufstufung um, falls Sie nicht versuchen, an einen nicht belegten Domänencontroller anzufügen. Sie müssen mit **-UseExistingAccount** und je nach Kontotyp das korrekte schreibgeschützte oder beschreibbare Argument an das nicht belegte Domänen Controller Konto anfügen. |
| 88 | Der angegebene Serveradmin ist ungültig | Sie haben ein ungültiges Konto für die RODC Admin-Delegierung angegeben. Stellen Sie sicher, dass das angegebene Konto ein gültiger Benutzer ist bzw. zu einer gültigen Gruppe gehört |
| 89 | RID-Master für die angegebene Domäne ist offline. | Führen Sie **netdom.exe query fsmo** aus, um den RID-Master zu bestimmen. Bringen Sie diesen online und machen Sie ihn für den Domänencontroller verfügbar, den Sie heraufstufen möchten |
| 90 | Domänennamenmaster ist offline. | Führen Sie **netdom.exe query fsmo** aus, um den Domänennamenmaster zu bestimmen. Bringen Sie diesen online und machen Sie ihn für den Domänencontroller verfügbar, den Sie heraufstufen möchten |
| 91 | Fehler bei der Ermittlung, ob es sich um einen wow64-Prozess handelt | *Dieser Fehler ist nicht mehr möglich, da es sich um ein 64-Bit-Betriebssystem handelt* |
| 92 | Wow64-Prozess wird nicht unterstützt | *Dieser Fehler ist nicht mehr möglich, da es sich um ein 64-Bit-Betriebssystem handelt* |
| 93 | Domänencontrollerdienst wird nicht ausgeführt für nichterzwungene Herabstufung | Starten Sie den AD DS-Dienst |
| 94 | Lokales Admin-Kennwort erfüllt die Anforderung nicht: entweder leer oder nicht benötigt | Geben Sie ein nicht-leeres Kennwort ein und stellen Sie sicher, dass die lokale Kennwortrichtlinie ein Kennwort vorschreibt |
| 95 | Letzter Domänencontroller unter Windows Server 2008 oder neuerer Version kann nicht gelöscht werden in der Domäne, in der Live-RODCs existieren | Sie müssen zunächst alle RODCs herabstufen, bevor Sie alle beschreibbaren Domänencontroller unter Windows Server 2008 oder neueren Versionen herabstufen können |
| 96 | DS-Binärdateien konnten nicht deinstalliert werden | *Wird nur mit dcpromo/unattend erkannt, das veraltet ist. Siehe ältere Dokumentation* |
| 97 | Version der Gesamtstrukturfunktionsebene ist neuer als die des Betriebssystems der untergeordneten Domäne | Geben Sie eine untergeordnete Domäne mit derselben oder einer höheren Version als der Version der Gesamtstrukturfunktionsebene an |
| 98 | Installation/Deinstallation der Komponenten-Binärdate wird ausgeführt. | *Wird nur mit dcpromo/unattend erkannt, das veraltet ist. Siehe ältere Dokumentation* |
| 99 | Die Funktionsebene der Gesamtstruktur ist zu niedrig (Fehler tritt nur unter Windows Server 2012 auf) | Setzen Sie die Gesamtstrukturfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt |
| 100 | Die Domänenfunktionsebene ist zu niedrig (Fehler tritt nur unter Windows Server 2012 auf) | Setzen Sie die Domänenfunktionsebene mindestens auf Windows Server 2003 im einheitlichen Modus herauf. Die Betriebssysteme Windows 2000 und Windows NT 4.0 werden nicht mehr unterstützt |

## <a name="known-issues-and-common-support-scenarios"></a>Bekannte Probleme und häufige Support Szenarien

Im Folgenden sind bekannte Probleme aufgeführt, die während des Windows Server 2012-Bereitstellungsprozesses auftreten können. All diese Probleme sind entwurfsbedingt und verfügen entweder über eine gültige Problemumgehung oder eine geeignetere Technik, um sie von vornherein zu vermeiden. Viele dieser Verhaltensweisen sind identisch unter Windows Server 2008 R2 und älteren Betriebssystemen, haben jedoch durch die neue Version der AD DS-Bereitstellung neue Bedeutung erlangt.

| Problem | Nach der Herabstufung eines Domänencontrollers bleibt DNS ohne Zonen zurück |
|--|--|
| Symptome | Server antwortet weiterhin auf DNS-Anfragen, hat jedoch keine Zoneninformationen |
| Lösung und Hinweise | Entfernen Sie beim Löschen der AD DS-Rolle ebenfalls die DNS-Serverrolle oder markieren Sie den DNS-Serverdienst als deaktiviert. Der DNS-Client darf dabei nicht auf sich selbst als Server zeigen. Falls Sie Windows PowerShell verwenden, führen Sie nach der Herabstufung des Servers den folgenden Befehl aus:<p>Code-Uninstall-Windows Feature DNS<p>oder<p>Codesatz-Dienst-DNS-StartType deaktiviert<br />Dienst-DNS-Dienst |

| Problem | Beim Heraufstufen eines Windows Server 2012 in eine existierende einteilige Domäne wird updatetopleveldomain=1 bzw. allowsinglelabeldnsdomain=1 nicht konfiguriert |
|--|--|
| Symptome | Dynamische DNS-Eintragsregistrierung funktioniert nicht |
| Lösung und Hinweise | Setzen Sie diese Werte über die Netlogon- und DNS-Gruppenrichtlinien. Microsoft hat ab Windows Server 2008 begonnen, die Erstellung einteiliger Domänen zu blockieren. Sie können ADMT oder das Domänenumbenennungstool verwenden, um zu einer erlaubten DNS-Domänenstruktur zu wechseln. |

| Problem | Herabstufung des letzten Domänencontrollers in einer Domäne schlägt fehl, wenn vorab erstellte und nicht belegte RODC-Konten existieren |
|--|--|
| Symptome | Herabstufung schlägt mit der folgenden Nachricht fehl:<p>**Dcpromo.General.54**<p>Active Directory-Domänendienste konnten keinen weiteren Active Directory-Domänencontroller finden, um die verbleibenden Daten in der Verzeichnispartition CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com zu übertragen.<p>"Das Format des angegebenen Domänennamens ist ungültig." |
| Lösung und Hinweise | Entfernen Sie alle verbleibenden vorab erstellten RODC-Konten, bevor Sie eine Domäne herabstufen. Verwenden Sie dazu **Dsa.msc** oder **Ntdsutil.exe metadata cleanup**. |

| Problem | Automatische Gesamtstruktur- und Domänenvorbereitung führt GPPREP nicht aus |
|--|--|
| Symptome | Domänenübergreifende Planungsfunktion für Gruppenrichtlinien, Richtlinienergebnissatz (Resultant Set of Policy RSOP) Planungsmodus, benötigt ein aktualisiertes Dateisystem und Active Directory-Berechtigungen für existierende Gruppenrichtlinie. Ohne Gpprep können Sie keine domänenübergreifende RSOP-Planung verwenden. |
| Lösung und Hinweise | Führen Sie **adprep.exe /gpprep** manuell für alle Domänen aus, die nicht zuvor für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Administratoren sollten GPPrep nur einmal über die Lebensdauer einer Domäne ausführen, und nicht bei jedem Upgrade. Dieser Befehl wird beim automatischen adprep nicht ausgeführt, wenn Sie bereits entsprechende benutzerdefinierte Berechtigungen eingestellt haben, da ansonsten der gesamte SYSVOL-Inhalt erneut auf alle Domänencontroller repliziert würde. |

| Problem | Die Install from Media-Prüfung schlägt fehl, wenn ein UNC-Pfad verwendet wird |
|--|--|
| Symptome | Zurückgegebener Fehler:<p>Code-der Medien Pfad konnte nicht überprüft werden. Ausnahme beim Aufrufen von "getDatabaseInfo" mit "2"-Argumenten. Der Ordner ist ungültig. |
| Lösung und Hinweise | Sie müssen IFM-Dateien auf einem lokalen Laufwerk speichern, nicht auf einem remote UNC-Pfad. Diese beabsichtigte Sperre verhindert die teilweise Heraufstufung von Servern bei Netzwerkunterbrechungen. |

| Problem | DNS-Delegierungswarnung wird bei der Domänencontroller-Heraufstufung zweimal angezeigt |
|--|--|
| Symptome | Die Warnung wurde bei der herauf Stufung mit addsdeployment Windows PowerShell *zweimal* zurückgegeben:<p>Code: "eine Delegierung für diesen DNS-Server kann nicht erstellt werden, da die autorisierende übergeordnete Zone nicht gefunden werden kann oder kein Windows-DNS-Server ausgeführt wird. Wenn Sie eine Integration in eine vorhandene DNS-Infrastruktur durchführen, sollten Sie manuell eine Delegierung zu diesem DNS-Server in der übergeordneten Zone erstellen, um eine zuverlässige Namensauflösung von außerhalb der Domäne sicherzustellen. Andernfalls ist keine Aktion erforderlich. " |
| Lösung und Hinweise | Ignorieren. ADDSDeployment Windows PowerShell zeigt die Warnung zuerst bei der Voraussetzungsprüfung und dann erneut bei der Konfiguration des Domänencontrollers an. Verwenden Sie dsas folgende Argument, falls Sie keine DNS-Delegierung konfigurieren möchten:<p>Code--kreatednsdelegation: $false<p>Überspringen Sie *niemals* die Voraussetzungsprüfung, um diese Nachricht zu unterdrücken |

| Problem | Bei der Angabe von UPN-Anmeldeinformationen oder solchen, die nicht zu einer Domäne gehören, werden bei der Konfiguration irreführende Fehler zurückgegeben |
|--|--|
| Symptome | Server-Manager gibt den folgenden Fehler zurück:<p>Code Ausnahme Aufruf von "dnsoption" mit "6"-Argumenten<p>ADDSDeployment Windows PowerShell gibt den folgenden Fehler zurück:<p>Code-Überprüfung der Benutzerberechtigungen ist fehlgeschlagen. Sie müssen den Namen der Domäne angeben, zu der dieses Benutzerkonto gehört. |
| Lösung und Hinweise | Stellen Sie sicher, dass Sie gültige Domänen-Anmeldeinformationen im Format **domain\user** angegeben haben. |

| Problem | Der Server startet nicht, nachdem die DirectoryServices-DomainController-Rolle mithilfe von Dism.exe entfernt wurde |
|--|--|
| Symptome | Falls Sie Dism.exe zum Entfernen der AD DS-Rolle verwenden, bevor Sie einen Domänencontroller ordnungsgemäß herabgestuft haben, startet der Server nicht mehr normal und zeigt den folgenden Fehler an:<p>Code-Status: 0x000000000<br />Info: ein unerwarteter Fehler ist aufgetreten. |
| Lösung und Hinweise | Drücken Sie *Umschalt+F8*, um den Verzeichnisdienst-Wiederherstellungsmodus zu starten. Fügen Sie die AD DS-Rolle wieder hinzu und erzwingen Sie die Herabstufung des Domänencontrollers. Alternativ können Sie das Systems mithilfe der Sicherung wiederherstellen. Verwenden Sie niemale Dism.exe zum Entfernen von AD DS-Rollen, da dieses Tool keine Kenntnis von Domänencontrollern hat. |

| Problem | Die Installation einer neuen Gesamtstruktur mit dem Gesamtstrukturmodus Win2012 schlägt fehl |
|--|--|
| Symptome | Bei der Heraufstufung mit ADDSDeployment Windows PowerShell wird der folgende Fehler zurückgegeben:<p>Code-Test. verifydcpromocore. Dcpromo. General. 74<p>Fehler bei der Überprüfung der Voraussetzungen für die Domänen Controller- Die angegebene Domänen Funktionsebene ist ungültig. |
| Lösung und Hinweise | Verwenden Sie die Gesamtstrukturfunktionsebene Win2012 nur, wenn Sie *ebenfalls* die Domänenfunktionsebene Win2012 angeben. Hier ist ein Beispiel, das fehlerfrei funktioniert:<p>Code--ForestMode Win2012-DomainMode Win2012] |

| Problem | Wenn Sie im Bereich Install from Media auf "Prüfen" klicken, geschieht nichts |
|--|--|
| Symptome | Wenn Sie einen Pfad zu einem IFM-Ordner angeben, wird beim Klicken auf die Schaltfläche **Prüfen** keine Nachricht zurückgegeben. |
| Lösung und Hinweise | Die Schaltfläche **Prüfen** gibt nur Fehler zurück, wenn ein Problem vorliegt. Andernfalls wird die Schaltfläche **Weiter** aktiviert, falls Sie einen IFM-Pfad angegeben haben. Sie müssen **Prüfen** anklicken, um fortfahren zu können, wenn Sie IFM ausgewählt haben. |

| Problem | Bei der Herabstufung mit Server-Manager wird vor dem Abschluss kein Feedback zurückgegeben. |
|--|--|
| Symptome | Wenn Sie Server-Manager zum Entfernen der AD DS-Rolle und zum Herabstufen eines Domänencontrollers verwenden, erhalten Sie keinerlei Feedback, bevor die Herabstufung fehlschlägt bzw. abgeschlossen ist. |
| Lösung und Hinweise | Dies ist eine Einschränkung von Server-Manager. Verwenden Sie das ADDSDeployment Windows PowerShell-Cmdlet, um Feedback zu erhalten:<p>Code-Uninstall-addsdomaincontroller |

| Problem | Die Install from Media-Prüfung erkennt nicht, dass ein RODC-Medium für einen beschreibbaren Domänencontroller angegeben wurde, oder umgekehrt. |
|--|--|
| Symptome | Wenn Sie einen neuen Domänencontroller mit IFM heraufstufen und dabei ein RODC-Medium für einen beschreibbaren Domänencontroller oder ein RWDC-Medium für einen RODC angeben, gibt die "Prüfen"-Schaltfläche keinen Fehler zurück. Später schlägt die Heraufstufung dann mit dem folgenden Fehler fehl:<p>Code: Fehler beim Konfigurieren dieses Computers als Domänen Controller. <br />Die herauf Stufung des schreibgeschützten Domänen Controllers kann nicht gestartet werden, da die angegebene Quelldatenbank nicht zulässig ist. Nur Datenbanken aus anderen RODCs können für die IFM-herauf Stufung eines RODC verwendet werden. |
| Lösung und Hinweise | Die Prüfung prüft nur die Gesamtintegrität von IFM. Verwenden Sie immer den korrekten IFM-Typ für den jeweiligen Server. Starten Sie den Server neu, bevor Sie die Heraufstufung erneut mit dem korrekten Medium vornehmen. |

| Problem | Die Heraufstufung eines RODC mit einem vorab erstellten Computerkonto schlägt fehl |
|--|--|
| Symptome | Beim Heraufstufen eines neuen RODC mit ADDSDeployment Windows PowerShell und einem gestaffelten Computerkonto erhalten Sie den folgenden Fehler:<p>Der Code Parametersatz kann mit den angegebenen benannten Parametern nicht aufgelöst werden.    <br />Invalidargument: parameterbindingexception<br />    + Fullyqualifiederrorid: ambiguousparameterset, Microsoft. Director yservices. Deployment. PowerShell. Commands. Install |
| Lösung und Hinweise | Geben Sie keine Parameter an, die bereits in einem vorab erstellten RODC-Konto vorhanden sind. Dazu gehören:<p>Code--"leseronlyreplica"<br />-InstallDNS<br />-donotkonfigurireglobalcatalog<br />-Sitename<br />-InstallDNS |

| Problem | Beim Aktivieren/Deaktivieren der Option "Zielserver bei Bedarf automatisch neu starten" geschieht nichts |
|--|--|
| Symptome | Wenn Sie die Option Server-Manager auswählen (bzw. nicht auswählen), **müssen Sie jeden Zielserver bei Bedarf automatisch neu starten, wenn** Sie einen Domänen Controller durch Rollen Entfernung herabstufen. der Server wird unabhängig von Ihrer Wahl immer neu gestartet. |
| Lösung und Hinweise | Dies ist beabsichtigt. Der Herabstufungsprozess startet den Server unabhängig von dieser Einstellung immer neu. |

| Problem | Dcpromo.log enthält die Zeile "[Fehler] Sicherheitseinstellung für Serverdateien fehlgeschlagen mit 2" |
|--|--|
| Symptome | Die Herabstufung eines Domänencontrollers läuft ohne Fehler ab, aber das dcpromo-Protokoll enthält den folgenden Fehler:<p>Code-[Fehler] Fehler beim Festlegen der Sicherheit für Server Dateien mit 2 |
| Lösung und Hinweise | Ignorieren, dieser Fehler ist zu erwarten und kosmetischer Natur. |

| Problem | Bei der adprep-Voraussetzungsprüfung wird der Fehler "Für die Domäne konnte keine Exchange-Schemakonfliktüberprüfung ausgeführt werden" angezeigt |
|--|--|
| Symptome | Beim Versuch, einen Windows Server 2012-Domänencontroller in eine existierende Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2-Gesamtstruktur heraufzustufen, wird bei der Voraussetzungsprüfung der folgende Fehler angezeigt:<p>Code-Überprüfung der Voraussetzungen für AD prep fehlgeschlagen. Die Exchange-Schema Konflikt Überprüfung für die Domäne kann nicht ausgeführt werden *<domain name>* (Ausnahme: der RPC-Server ist nicht verfügbar).<p>adprep.log enthält den folgenden Fehler:<p>Code-Adprep konnte keine Daten vom Server abrufen.*<domain controller>*<p>über Windows-Verwaltungsinstrumentation (WMI). |
| Lösung und Hinweise | Der neue Domänencontroller hat keinen Zugriff auf WMI über die DCOM/RPC-Protokolle für die existierenden Domänencontroller. Aktuell existieren drei Ursachen für diesen Fehler:<p>-Eine Firewallregel blockiert den Zugriff auf die vorhandenen Domänen Controller.<p>-Das Netzwerkdienst Konto fehlt in der Berechtigung "Anmelden als Dienst" (SeServiceLogonRight) auf den vorhandenen Domänen Controllern.<p>-NTLM ist auf Domänen Controllern mithilfe von Sicherheitsrichtlinien, [die in Einführung der Einschränkung der NTLM-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10)) beschrieben werden, deaktiviert. |

| Problem | Beim Erstellen einer neuen Gesamtstruktur wird immer eine DNS-Warnung angezeigt |
|--|--|
| Symptome | Wenn Sie eine neue AD DS-Gesamtstruktur erstellen und die DNS-Zone auf dem neuen Domänencontroller für sich selbst erstellen, erhalten Sie immer die folgende Warnmeldung:<p>Code: in der DNS-Konfiguration wurde ein Fehler erkannt. <br />Keiner der von diesem Computer verwendeten DNS-Server hat innerhalb des Timeout Intervalls geantwortet.<br />(Fehlercode 0x000005b4 "ERROR_TIMEOUT") |
| Lösung und Hinweise | Ignorieren. Diese Warnung ist beabsichtigt für den ersten Domänencontroller in der Stammdomäne einer neuen Gesamtstruktur, für den Fall, dass Sie auf einen existierenden DNS-Server und eine existierende Zone verweisen möchten. |

| Problem | Das Windows PowerShell-Argument -whatif liefert falsche DNS-Serverinformationen zurück |
|--|--|
| Symptome | Falls Sie das Argument **-whatif** beim Konfigurieren eines Domänencontrollers mit implizitem oder explizitem **-installdns:$true** verwenden, wird die folgende Ausgabe angezeigt:<p>Code: "DNS-Server: Nein" |
| Lösung und Hinweise | Ignorieren. DNS ist installiert und funktioniert korrekt. |

| Problem | Nach der Heraufstufung schlägt die Anmeldung fehl mit "Zum Verarbeiten des Befehls ist nicht genügend Speicherplatz verfügbar" |
|--|--|
| Symptome | Wenn Sie sich nach der Heraufstufung eines neuen Domänencontrollers abmelden und anschließend versuchen, sich interaktiv anzumelden, erhalten Sie den folgenden Fehler:<p>Der Code ist nicht genügend Speicher verfügbar, um diesen Befehl zu verarbeiten. |
| Lösung und Hinweise | Der Domänencontroller wurde nach der Heraufstufung nicht neu gestartet, entweder aufgrund eines Fehlers oder weil Sie das ADDSDeployment Windows PowerShell-Argument **-norebootoncompletion** verwendet haben. Starten Sie den Domänencontroller neu. |

| Problem | Schaltfläche "Weiter" ist auf der Seite mit den Domänencontrolleroptionen nicht verfügbar |
|--|--|
| Symptome | Die Schaltfläche **Weiter** auf der Seite **Domänencontrolleroptionen** in Server-Manager ist nicht verfügbar, obwohl Sie ein Kennwort eingestellt haben. Das Menü **Sitename** enthält keine Sites. |
| Lösung und Hinweise | Sie haben mehrere AD DS-Sites, und mindestens einer dieser Sites fehlen Subnetze. Dieser zukünftige Domänencontroller gehört zu einem dieser Subnetze. Wählen Sie das Subnetz aus dem Dropdown-Menü Sitename manuell aus. Sie sollten außerdem alle AD-Sites mithilfe von DSSITE.MSC oder mit dem folgenden Windows PowerShell-Befehl prüfen, um alle fehlenden Subnetze zu identifizieren:<p>Code-Get-adreplicationsite-Filter \* -eigenschaftensubnetze &#124; Where-Object {! $ _. Subnetze-EQ " \* "} &#124; Format-Tabellenname |

| Problem | Herauf- oder Herabstufung schlägt fehl mit "Der Dienst kann nicht gestartet werden" |
|--|--|
| Symptome | Beim Heraufstufen, Herabstufen oder Klonen eines Domänencontrollers erhalten Sie den folgenden Fehler:<p>Code-der Dienst kann nicht gestartet werden, da er entweder deaktiviert ist oder ihm keine aktivierten Geräte zugeordnet sind "(0x80070422.)<p>Der Fehler kann interaktiv oder als Ereignis angezeigt oder in eines der Protokolle wie z. B. dcpromoui.log oder dcpromo.log geschrieben werden |
| Lösung und Hinweise | Der DS-Rollenserverdienst (DsRoleSvc) ist deaktiviert. Dieser Dienst wird bei der Installation der AD DS-Rolle automatisch installiert und auf den Starttyp manuell gesetzt. Deaktivieren Sie diesen Dienst nicht. Setzen Sie den Starttyp wieder auf manuell und erlauben Sie den DS-Rollenoperationen, den Dienst bei Bedarf zu starten und anzuhalten. Dieses Verhalten ist beabsichtigt. |

| Problem | Sie erhalten weiterhin eine Warnung von Server-Manager, dass Sie den Domänencontroller heraufstufen müssen |
|--|--|
| Symptome | Wenn Sie einen Domänencontroller mit dem veralteten Befehl dcpromo.exe /unattend heraufstufen oder ein Upgrade eines existierenden Windows Server 2008 R2-Domänencontrollers auf Windows Server 2012 vornehmen, zeigt Server-Manager weiterhin die Konfigurationsaufgabe **Server zu einem Domänencontroller heraufstufen** zur Ausführung nach der Heraufstufung an. |
| Lösung und Hinweise | Wenn Sie auf den Warn-Link klicken, verschwindet die Nachricht endgültig. Dieses Verhalten ist zu erwarten und kosmetischer Natur. |

| Problem | Fehlende Rolleninstallation für Server-Manager-Bereitstellungsskript |
|--|--|
| Symptome | Wenn Sie einen Domänencontroller mithilfe von Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, werden Cmdlet und Argumente für die Rolleninstallation (install-windowsfeature -name ad-domain-services -includemanagementtools) nicht mitgespeichert. Ohne die Rolle kann der Domänencontroller nicht konfiguriert werden. |
| Lösung und Hinweise | Fügen Sie Cmdlet und Argumente manuell zu Ihren Skripts hinzu. Dieses Verhalten ist zu erwarten und entwurfsbedingt. |

| Problem | Server-Manager-Bereitstellungsskript ist keine PS1-Datei |
|--|--|
| Symptome | Wenn Sie einen Domänencontroller mithilfe von Server-Manager heraufstufen und das Windows PowerShell-Bereitstellungsskript speichern, erhält die Datei einen zufälligen temporären Namen und wird nicht als PS1-Datei benannt. |
| Lösung und Hinweise | Benennen Sie die Datei manuell um. Dieses Verhalten ist zu erwarten und entwurfsbedingt. |

| Problem | Dcpromo /unattend erlaubt nicht unterstützte funktionale Ebenen |
|--|--|
| Symptome | Wenn Sie einen Domänencontroller mithilfe von dcpromo /unattend und der folgenden Beispiel-Antwortdatei heraufstufen:<p>Ordnung<p>[DCInstall]<br />NewDomain = Gesamtstruktur<p>Replicaornewdomain = Domäne<p>NewDomainDNSName = Corp. Configuration. com<p>SafeModeAdminPassword =Safepassword@6<p>DomainNetbiosName = Corp<p>Dnsonnetwork = ja<p>AutoConfigDNS = ja<p>Rebootonsuccess = noandnoprompteither<p>RebootOnCompletion = Nein<p>*DomainLevel = 0*<p>*ForestLevel = 0*<p>Die Heraufstufung schlägt mit den folgenden Fehlern in dcpromoui.log fehl:<p>Code-Dcpromoui EA 4.5 B8 0089 13:31:50.783 Enter cargumentsspec:: validateargument DomainLevel<p>Dcpromoui EA 4.5 B8 008a 13:31:50.783 Wert für DomainLevel ist 0<p>Dcpromoui EA 4.5 B8 008b 13:31:50.783 Exitcode ist 77<p>Dcpromoui EA 4.5 B8 008c 13:31:50.783 das angegebene Argument ist ungültig.<p>Dcpromoui EA 4.5 B8 008d 13:31:50.783 Schließ Endes Protokoll<p>Dcpromoui EA 4.5 B8 0032 13:31:50.830 Exitcode ist 77<p>Level 0 steht für Windows 2000 und wird unter Windows Server 2012 nicht unterstützt. |
| Lösung und Hinweise | Sie sollten den veralteten Befehl dcpromo /unattend nicht verwenden, da dieser die Angabe ungültiger Einstellungen erlaubt, die später zu Fehlern führen. Dieses Verhalten ist zu erwarten und entwurfsbedingt. |

| Problem | Herauf Stufung "hängt" beim Erstellen des NTDS-Einstellungs Objekts, nie abgeschlossen |
|--|--|
| Symptome | Wenn Sie einen Replikat-DC oder RODC herauf Stufen, erreicht die herauf Stufung das "Erstellen eines NTDS-Einstellungs Objekts" und wird nie fortgesetzt oder abgeschlossen Die Protokolle werden ebenfalls nicht mehr aktualisiert. |
| Lösung und Hinweise | Dies ist ein bekanntes Problem und entsteht, wenn die Anmeldeinformationen des integrierten lokalen Administratorkontos mit dem Kennwort des integrierten Domänenadministratorkontos angegeben werden. Dabei entsteht ein Fehler in der zentralen Setup-Engine und die Engine wird in eine Art Endlosschleife versetzt. Dies wird erwartet, auch wenn unerwünschtes Verhalten.<p>So reparieren Sie den Server:<p>1. Starten Sie ihn neu.<p>1. löschen Sie in AD das Mitglieds Computer Konto dieses Servers (es ist noch kein DC-Konto).<p>1. deaktivieren Sie auf diesem Server das Aufheben der Verknüpfung von der Domäne.<p>1. entfernen Sie auf diesem Server die AD DS Rolle.<p>1. Neustart<p>1. Fügen Sie die AD DS Rolle erneut hinzu, und wiederholen Sie die herauf Stufung, und stellen Sie sicher, dass Sie die Anmelde Informationen für ***Domänen \ Administratoren*** immer für die DC-herauf Stufung und nicht nur für das integrierte lokale Administrator Konto angeben |
