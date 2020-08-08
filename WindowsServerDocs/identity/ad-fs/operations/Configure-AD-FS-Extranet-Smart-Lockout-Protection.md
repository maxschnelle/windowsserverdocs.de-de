---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: Konfigurieren des intelligenten AD FS-Extranetsperrschutzes
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 05/20/2019
ms.topic: article
ms.openlocfilehash: 707eeda20dda1297a168ae4a0597566a25593221
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962664"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS Extranet Lockout und Extranet Smart Lockout

## <a name="overview"></a>Übersicht

Extranet Smart Sperrungs (ESL) schützt Ihre Benutzer vor dem Auftreten einer Extranet-Konto Sperre von böswilligen Aktivitäten.

Mit ESL können AD FS zwischen Anmelde versuchen von einem vertrauten Speicherort für einen Benutzer und Anmelde versuchen von einem möglichen Angreifer unterscheiden. AD FS können Angreifer sperren, während gültige Benutzer weiterhin ihre Konten verwenden können. Dies verhindert und schützt vor Denial-of-Service-Angriffen und bestimmten Klassen von Kenn Wort Sprüh Angriffen für den Benutzer. ESL ist für AD FS in Windows Server 2016 verfügbar und ist in AD FS in Windows Server 2019 integriert.

ESL ist nur für die Authentifizierungsanforderungen für Benutzername und Kennwort verfügbar, die über das Extranet mit dem webanwendungsproxy oder einem Drittanbieter Proxy geliefert werden. Jeder Drittanbieter Proxy muss das MS-adfspip-Protokoll unterstützen, das anstelle des webanwendungsproxys verwendet wird, z. b. [F5 BIG-IP Access Policy Manager](https://devcentral.f5.com/s/articles/ad-fs-proxy-replacement-on-f5-big-ip-30191). Überprüfen Sie die Proxy Dokumentation von Drittanbietern, um zu ermitteln, ob der Proxy das MS-adfspip-Protokoll unterstützt.

## <a name="additional-features-in-ad-fs-2019"></a>Zusätzliche Features in AD FS 2019
Extranet Smart Lockout in AD FS 2019 bietet im Vergleich zu AD FS 2016 die folgenden Vorteile:
- Legen Sie unabhängige Sperr Schwellenwerte für vertraute und unbekannte Speicherorte fest, damit Benutzer an bekannten guten Standorten mehr Platz als Fehler aufweisen können als Anforderungen von verdächtigen Speicherorten.
- Aktivieren Sie den Überwachungsmodus für Smart Sperrungs, und setzen Sie das vorherige Verhalten der Soft Sperre fort. Auf diese Weise können Sie sich mit den vertrauten Benutzer Standorten vertraut machen und bleiben weiterhin durch das extranetsperrungsfeature geschützt, das in AD FS 2012r2 verfügbar ist.

## <a name="how-it-works"></a>Funktionsweise
### <a name="configuration-information"></a>Konfigurationsinformationen
Wenn ESL aktiviert ist, wird eine neue Tabelle in der artefaktdatenbank adfsartifactstore. accountactivity erstellt, und in der AD FS Farm wird ein Knoten als Master Benutzeraktivität ausgewählt. In einer wid-Konfiguration ist dieser Knoten immer der primäre Knoten. In einer SQL-Konfiguration wird ein Knoten als Benutzer Aktivitäts Master ausgewählt.

, Um den ausgewählten Knoten als Benutzer Aktivitäts Master anzuzeigen. (Get-adfsfarminformation). Farmrollen

Alle sekundären Knoten wenden sich bei jeder neuen Anmeldung über Port 80 an den Master Knoten, um den aktuellen Wert der Anzahl fehlerhafter Kenn Wörter und neuer bekannter Standort Werte zu ermitteln und den Knoten nach der Verarbeitung der Anmeldung zu aktualisieren.

![Konfiguration](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 Wenn der sekundäre Knoten den Master nicht kontaktieren kann, werden Fehlerereignisse in das AD FS Administrator Protokoll geschrieben. Authentifizierungen werden weiterhin verarbeitet, aber AD FS schreiben den aktualisierten Status nur lokal. AD FS wird alle 10 Minuten eine Verbindung mit dem Master hergestellt und wechselt zurück zum Master, sobald der Master verfügbar ist.

### <a name="terminology"></a>Terminologie
- **Familiarlocation**: während einer Authentifizierungsanforderung prüft ESL alle dargestellten IPS. Diese IPS bestehen aus einer Kombination aus Netzwerk-IP, weiter geleiteter IP-Adresse und der optionalen x-weitergeleiteten IP-Adresse. Wenn die Anforderung erfolgreich ist, werden alle IPS der Konto Aktivitäts Tabelle als "vertraute IPS" hinzugefügt. Wenn für die Anforderung alle IPS in den "vertrauten IPS" vorhanden sind, wird die Anforderung als "vertrauter"-Speicherort behandelt.
- **Unknownlocation**: Wenn eine Anforderung, die in enthalten ist, mindestens eine IP-Adresse nicht in der vorhandenen "familiarlocation"-Liste enthalten ist, wird die Anforderung als "Unbekannter" Speicherort behandelt. Dies dient zum Verarbeiten von Proxy Szenarien wie der Legacy Authentifizierung von Exchange Online, bei der Exchange Online-Adressen sowohl erfolgreiche als auch fehlgeschlagene Anforderungen verarbeiten.
- **BadPwdCount**: ein Wert, der angibt, wie oft ein falsches Kennwort übermittelt und die Authentifizierung nicht erfolgreich war. Für jeden Benutzer werden separate Indikatoren für vertraute Standorte und unbekannte Speicherorte aufbewahrt.
- **Unknownlockout**: ein boolescher Wert pro Benutzer, wenn der Benutzer für den Zugriff über unbekannte Speicherorte gesperrt ist. Dieser Wert wird auf der Grundlage der badpwdzähl-und extranetlockoutthreshold-Werte berechnet.
- **Extranetlockoutthreshold**: dieser Wert bestimmt die maximale Anzahl fehlerhafter Kenn Wort Versuche. Wenn der Schwellenwert erreicht ist, lehnt ADFS Anforderungen vom Extranet ab, bis das Überwachungs Fenster verstrichen ist.
- **Extranetobservationwindow**: dieser Wert bestimmt die Dauer, für die Benutzernamen-und Kenn Wort Anforderungen von unbekannten Speicherorten gesperrt werden. Wenn das Fenster verstrichen ist, startet ADFS die Benutzernamen-und Kenn Wort Authentifizierung von unbekannten Standorten erneut.
- **Extranetlockumquirepdc**: Wenn diese Option aktiviert ist, erfordert die extranetsperre einen primären Domänen Controller (PDC). Wenn diese Option deaktiviert ist, wird für den Fall, dass der PDC nicht verfügbar ist, die extranetsperre auf einen anderen Domänen Controller
- **Extranetlockoutmode**: steuert nur das Protokoll im Vergleich zum erzwungenen Modus der Extranet-Smart Lockout
    - **Adsssmartlockoutlogonly**: die Smart Lockout-Funktion in Extranet ist aktiviert, aber AD FS werden nur Administrator-und Überwachungs Ereignisse schreiben, aber keine Authentifizierungsanforderungen ablehnen. Dieser Modus soll zunächst aktiviert werden, damit "familiarlocation" ausgefüllt wird, bevor "adfssmartlockoutenforce" aktiviert ist.
    - **ADF-martlockoutenforce**: vollständige Unterstützung für das Blockieren von unbekannten Authentifizierungsanforderungen, wenn Schwellenwerte erreicht werden.

IPv4-und IPv6-Adressen werden unterstützt.

### <a name="anatomy-of-a-transaction"></a>Anatomie einer Transaktion
- **Vorauthentifizierungs Überprüfung**: während einer Authentifizierungsanforderung prüft ESL alle dargestellten IPS. Diese IPS bestehen aus einer Kombination aus Netzwerk-IP, weiter geleiteter IP-Adresse und der optionalen x-weitergeleiteten IP-Adresse. In den Überwachungsprotokollen werden diese IP-Adressen im <IpAddress> Feld in der Reihenfolge von "x-ms-weitergeleitet-Client-IP", "x-weitergeleitet-für", "x-ms-Proxy-Client-IP" aufgeführt.

  Basierend auf diesen IPS wird von ADFS ermittelt, ob die Anforderung von einem vertrauten oder unbekannten Speicherort aus erfolgt. Anschließend wird überprüft, ob der entsprechende BadPwdCount-Wert kleiner als der festgelegte Schwellenwert ist oder ob der letzte **fehlgeschlagene** Versuch länger als der Zeitrahmen des Beobachtungs Fensters erfolgt ist. Wenn eine dieser Bedingungen zutrifft, ermöglicht ADFS dieser Transaktion die weitere Verarbeitung und Überprüfung der Anmelde Informationen. Wenn beide Bedingungen false sind, befindet sich das Konto bereits in einem gesperrten Zustand, bis das Überwachungs Fenster vorbei ist. Nachdem das Überwachungs Fenster weitergeleitet wurde, ist der Benutzer berechtigt, sich zu authentifizieren. Beachten Sie, dass ADFS in 2019 anhand des entsprechenden Schwellenwerts überprüft, ob die IP-Adresse mit einem vertrauten Speicherort übereinstimmt oder nicht.
- **Erfolgreiche Anmeldung**: Wenn die Anmeldung erfolgreich ist, werden die IP-Adressen aus der Anforderung der vertrauten Standort-IP-Liste des Benutzers hinzugefügt.
- Fehler bei der **Anmeldung**: Wenn bei der Anmeldung ein Fehler auftritt, wird der Wert für BadPwdCount angehoben. Der Benutzer wechselt in einen Sperr Status, wenn der Angreifer mehr ungültige Kenn Wörter an das System sendet, als der Schwellenwert zulässt. (BadPwdCount > extranetlockoutthreshold)

![Konfiguration](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

Der Wert "unknownlockout" entspricht "true", wenn das Konto gesperrt ist. Dies bedeutet, dass der BadPwdCount-Wert des Benutzers über dem Schwellenwert liegt, d. h., jemand hat mehr Kenn Wörter versucht, als vom System zugelassen wurden. In diesem Zustand gibt es zwei Möglichkeiten, wie sich ein gültiger Benutzer anmelden kann.
- Der Benutzer muss warten, bis die observationwindow-Zeit abgelaufen ist.
- Setzen Sie "BadPwdCount" mit "Reset-adfsaccountlockout" auf 0 zurück, um den Sperr Status zurückzusetzen.

Wenn keine zurück Stellungen auftreten, wird dem Konto ein einzelner Kenn Wort Versuch für die Anzeige für jedes Überwachungs Fenster gestattet. Das Konto wird nach diesem Versuch in den gesperrten Status zurückversetzt, und das Überwachungs Fenster wird neu gestartet. Der BadPwdCount-Wert wird nach einer erfolgreichen Kenn Wort Anmeldung nur automatisch zurückgesetzt.

### <a name="log-only-mode-versus-enforce-mode"></a>Nur-Protokoll-Modus im Vergleich zum ' erzwingen '-Modus
Die Tabelle accountactivity wird im Modus "nur Protokoll" und im Modus "erzwingen" aufgefüllt. Wenn der Modus "nur Protokoll" umgangen wird und "ESL" ohne die empfohlene Wartezeit direkt in den Modus "erzwingen" verschoben wird, sind die vertrauten IP-Adressen der Benutzer ADFS nicht bekannt. In diesem Fall verhält sich "ESL" wie "adbadpasswordcounter", wodurch möglicherweise legitimer Benutzer Datenverkehr blockiert wird, wenn das Benutzerkonto mit einem aktiven Brute-Force-Angriff erfolgt. Wenn der Modus "nur Protokoll" umgangen wird und der Benutzer einen gesperrten Zustand mit "unknownlockout" = true eingibt und versucht, sich mit einem guten Kennwort von einer IP-Adresse zu anmelden, die nicht in der "vertrauten" IP-Liste enthalten ist, können Sie sich nicht anmelden. Der Modus "nur Protokoll" wird für 3-7 Tage empfohlen, um dieses Szenario zu vermeiden. Wenn Konten aktiv angegriffen werden, sind mindestens 24 Stunden im Modus "nur Protokoll" erforderlich, um Sperren für berechtigte Benutzer zu verhindern.

## <a name="extranet-smart-lockout-configuration"></a>Smart Lockout-Konfiguration für Extranet

### <a name="prerequisites-for-ad-fs-2016"></a>Voraussetzungen für AD FS 2016

1. **Installieren von Updates auf allen Knoten in der Farm**

   Stellen Sie zunächst sicher, dass alle Windows Server 2016-AD FS Server ab den Windows-Updates vom Juni 2018 auf dem neuesten Stand sind und dass die AD FS 2016-Farm auf der Ebene der 2016-Farm ausgeführt wird.
1. **Berechtigungen überprüfen**

   Extranet Smart Lockout erfordert, dass die Windows-Remote Verwaltung auf allen AD FS Server aktiviert ist.
3. **Aktualisieren von artefaktdatenbankberechtigungen**

   Extranet Smart Sperrungs erfordert, dass das AD FS-Dienst Konto über Berechtigungen zum Erstellen einer neuen Tabelle in der AD FS artefaktdatenbank verfügt. Melden Sie sich bei einem beliebigen AD FS Server als AD FS Administrator an, und erteilen Sie diese Berechtigung, indem Sie die folgenden Befehle in einem PowerShell-Eingabe Aufforderungs Fenster ausführen:

   ``` powershell
   PS C:\>$cred = Get-Credential
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
   ```
   >[!NOTE]
   >Der $cred Platzhalter ist ein Konto, das über AD FS Administrator Berechtigungen verfügt. Dies sollte die Schreibberechtigungen zum Erstellen der Tabelle bereitstellen.

   Die obigen Befehle können aufgrund fehlender ausreichender Berechtigungen nicht ausgeführt werden, da Ihre AD FS Farm SQL Server verwendet und die oben aufgeführten Anmelde Informationen nicht über die Administrator Berechtigung für Ihren SQL-Server verfügen. In diesem Fall können Sie die Daten Bank Berechtigungen manuell in SQL Server Datenbank konfigurieren, indem Sie den folgenden Befehl ausführen, wenn Sie mit der adfsartifactstore-Datenbank verbunden sind.
    ```
    # when prompted with “Are you sure you want to perform this action?”, enter Y.

    [CmdletBinding(SupportsShouldProcess=$true,ConfirmImpact = 'High')]
    Param()

    $fileLocation = "$env:windir\ADFS\Microsoft.IdentityServer.Servicehost.exe.config"

    if (-not [System.IO.File]::Exists($fileLocation))
    {
    write-error "Unable to open ADFS configuration file."
    return
    }

    $doc = new-object Xml
    $doc.Load($fileLocation)
    $connString = $doc.configuration.'microsoft.identityServer.service'.policystore.connectionString
    $connString = $connString -replace "Initial Catalog=AdfsConfigurationV[0-9]*", "Initial Catalog=AdfsArtifactStore"

    if ($PSCmdlet.ShouldProcess($connString, "Executing SQL command sp_addrolemember 'db_owner', 'db_genevaservice' "))
    {
    $cli = new-object System.Data.SqlClient.SqlConnection
    $cli.ConnectionString = $connString
    $cli.Open()

    try
    {

    $cmd = new-object System.Data.SqlClient.SqlCommand
    $cmd.CommandText = "sp_addrolemember 'db_owner', 'db_genevaservice'"
    $cmd.Connection = $cli
    $rowsAffected = $cmd.ExecuteNonQuery()
    if ( -1 -eq $rowsAffected )
    {
    write-host "Success"
    }
    }
    finally
    {
    $cli.CLose()
    }
    }
    ```

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>Sicherstellen, dass AD FS Protokollierung der Sicherheitsüberwachung aktiviert ist
Diese Funktion nutzt Sicherheits Überwachungs Protokolle, sodass die Überwachung sowohl in AD FS als auch in der lokalen Richtlinie auf allen AD FS Servern aktiviert werden muss.

### <a name="configuration-instructions"></a>Konfigurationsanweisungen
Extranet Smart Lockout verwendet die ADFS-Eigenschaft **extranetlockoutenabled**. Diese Eigenschaft wurde zuvor zum Steuern der "Extranet Soft Lockout" in Server 2012r2 verwendet. Wenn Extranet Soft Lockout aktiviert war, führen Sie aus, um die aktuelle Eigenschaften Konfiguration anzuzeigen ` Get-AdfsProperties` .

### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen
Wenn Sie die Smart Lockout-Extranet konfigurieren, befolgen Sie die bewährten Methoden zum Festlegen von Schwellenwerten:

`ExtranetObservationWindow (new-timespan -Minutes 30)`

`ExtranetLockoutThreshold: Half of AD Threshold Value`

AD-Wert: 20, extranetlockoutthreshold: 10

Active Directory Sperre funktioniert unabhängig von der Extranet Smart Sperrungs. Wenn Active Directory Sperre jedoch aktiviert ist, wird extranetlockoutthreshold in AD FS Schwellenwert für < Kontosperrung in AD

`ExtranetLockoutRequirePDC - $false`

Wenn diese Option aktiviert ist, erfordert die extranetsperre einen primären Domänen Controller (PDC). Wenn Sie deaktiviert und als falsch konfiguriert ist, wird für den Fall, dass der PDC nicht verfügbar ist, die extranetsperre auf einen anderen Domänen Controller Fall Back

Zum Festlegen dieser Eigenschaft führen Sie Folgendes aus:

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```
### <a name="enable-log-only-mode"></a>Nur-Protokoll-Modus aktivieren

Im nur-Protokoll-Modus füllt AD FS den Benutzern vertraute Standortinformationen auf und schreibt Sicherheits Überwachungs Ereignisse, blockiert jedoch keine Anforderungen. Dieser Modus wird verwendet, um zu überprüfen, ob Smart Sperrungs ausgeführt wird, und um AD FS zu ermöglichen, vertraute Orte für Benutzer zu "erlernen", bevor Sie den Modus "erzwingen" aktivieren. Wie AD FS lernt, speichert es die Anmelde Aktivität pro Benutzer (ob im Protokollmodus oder im Erzwingungs Modus).
Legen Sie das Sperr Verhalten so fest, dass es nur protokolliert wird, indem Sie das folgende Commandlet ausführen.

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly`

Der Modus "nur Protokoll" ist ein temporärer Zustand, damit das System das Anmeldeverhalten erlernen kann, bevor eine Sperr Erzwingung mit dem Smart Sperrungs-Verhalten eingeführt wird. Die empfohlene Dauer für den Modus "nur Protokoll" beträgt 3-7 Tage. Wenn Konten aktiv angegriffen werden, muss der nur-Protokoll-Modus mindestens 24 Stunden ausgeführt werden.

Wenn auf AD FS 2016 das Verhalten "Extranet Soft Lockout" in 2012r2 vor dem Aktivieren der Extranet-Smart Lockout aktiviert ist, wird das Verhalten des extranetsperrungs-Modus deaktiviert. Durch AD FS Smart Lockout werden Benutzer nicht im reinen Protokollmodus gesperrt. Allerdings kann der lokale Ad den Benutzer basierend auf der AD-Konfiguration sperren. Lesen Sie die AD Sperrungs-Richtlinien, um zu erfahren, wie lokale AD-Benutzer sperren können.

Ein zusätzlicher Vorteil bei AD FS 2019 besteht darin, dass Sie in der Lage sein können, den nur-Protokoll-Modus für Smart Sperrungs zu aktivieren, während Sie weiterhin das vorherige Soft Lock-Verhalten mit dem folgenden PowerShell-Befehl erzwingen.

`Set-AdfsProperties -ExtranetLockoutMode 3`

Damit der neue Modus wirksam wird, starten Sie den AD FS-Dienst auf allen Knoten in der Farm neu.

`Restart-service adfssrv`

Nachdem der Modus konfiguriert wurde, können Sie die Smart Sperrungs mithilfe des Parameters "enableextranetlockout" aktivieren.

`Set-AdfsProperties -EnableExtranetLockout $true`

### <a name="enable-enforce-mode"></a>Erzwingungs Modus aktivieren

Wenn Sie mit dem Sperr Schwellenwert und dem Überwachungs Fenster vertraut sind, können Sie mithilfe des folgenden PSH-Cmdlets in den Modus "erzwingen" verschoben werden:

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce`

Damit der neue Modus wirksam wird, starten Sie den AD FS-Dienst auf allen Knoten in der Farm neu, indem Sie den folgenden Befehl verwenden.

`Restart-service adfssrv`

## <a name="manage-user-account-activity"></a>Aktivität "Benutzerkonto verwalten"
AD FS stellt drei Cmdlets zum Verwalten von Konto Aktivitätsdaten bereit. Diese Cmdlets stellen automatisch eine Verbindung mit dem Knoten in der Farm her, der die Master Rolle innehat.
>[!NOTE]
>Just Enough Administration (Jea) kann verwendet werden, um AD FS Cmdlets zum Zurücksetzen von Konto Sperrungen zu delegieren. Beispielsweise können Helpdeskmitarbeiter Berechtigungen zur Verwendung von ESL-Commandlets delegieren. Weitere Informationen zum Delegieren von Berechtigungen für die Verwendung dieser Cmdlets finden [Sie unter Delegieren AD FS PowerShell-Commandlets Zugriff auf Benutzer ohne Administrator](delegate-ad-fs-pshell-access.md) Rechte.

Dieses Verhalten kann überschrieben werden, indem der-Server-Parameter übergeben wird.

- Get-adfsaccountactivity-userPrincipalName

  Lesen Sie die aktuelle Kontoaktivität für ein Benutzerkonto. Das Cmdlet stellt mithilfe des Rest-Endpunkts für die Kontoaktivität immer automatisch eine Verbindung mit dem Farm Master her. Daher sollten alle Daten immer einheitlich sein.

`Get-ADFSAccountActivity user@contoso.com`

  Eigenschaften:
    - Badpwdzählvertraute: wird inkrementiert, wenn eine Authentifizierung von einem bekannten Speicherort aus erfolgreich ist.
    - Badpwdrattunknown: inkrementiert, wenn eine Authentifizierung an einem unbekannten Speicherort nicht erfolgreich ist
    - Lastfailedauthvertraute: Wenn die Authentifizierung an einem vertrauten Speicherort nicht erfolgreich war, ist lastfailedauthunknown auf die Zeit der nicht erfolgreichen Authentifizierung festgelegt.
    - Lastfailedauthunknown: Wenn die Authentifizierung an einem unbekannten Speicherort nicht erfolgreich war, ist lastfailedauthunknown auf die Zeit der nicht erfolgreichen Authentifizierung festgelegt.
    - Familiarlockout: Boolescher Wert, der "true" lautet, wenn "badpwdrattvertraute" > extranetlockoutthreshold
    - Unknownlockout: Boolescher Wert, der "true" lautet, wenn "badpwdrattunknown" > extranetlockoutthreshold
    - Vertrautheit: maximale Anzahl von 20 IPS, die dem Benutzer bekannt sind. Wenn dieser Wert überschritten wird, wird die älteste IP-Adresse in der Liste entfernt.
-    Set-adfsaccountactivity

     Fügt neue vertraute Speicherorte hinzu. Die vertraute IP-Liste enthält maximal 20 Einträge. wenn diese überschritten wird, wird die älteste IP-Adresse in der Liste entfernt.

`Set-ADFSAccountActivity user@contoso.com -AdditionalFamiliarIps “1.2.3.4”`

- Reset-adfsaccountlockout

  Setzt den Sperrungs Zähler für ein Benutzerkonto für jeden vertrauten Speicherort (badpwdzähltvertraute) oder für unbekannte Location-Indikatoren (badpwdantunvertraute) zurück. Durch das Zurücksetzen eines Zählers wird der Wert "familiarlockout" oder "unfamiliarlockout" aktualisiert, da der zurückgesetzte Wert kleiner als der Schwellenwert ist.

`Reset-ADFSAccountLockout user@contoso.com -Location Familiar`
`Reset-ADFSAccountLockout user@contoso.com -Location Unknown`

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>Ereignisprotokollierung & Benutzer Aktivitäts Informationen für AD FS extranetsperre

### <a name="connect-health"></a>Connect Health
Die empfohlene Vorgehensweise zum Überwachen der Benutzerkonto Aktivität erfolgt über Connect Health. Connect Health generiert eine herunterladbare Berichterstellung für riskante IPS und ungültige Kenn Wort Versuche. Jeder Eintrag im Bericht über riskante IP-Adressen enthält aggregierte Informationen zu fehlgeschlagenen AD FS-Anmeldeaktivitäten, für die der angegebene Schwellenwert überschritten wurde. E-Mail-Benachrichtigungen können mithilfe von anpassbaren e-Mail-Einstellungen auf Benachrichtigungs Administratoren festgelegt werden. Weitere Informationen und Installationsanweisungen finden Sie in der [Connect Health-Dokumentation](/azure/active-directory/hybrid/how-to-connect-health-adfs).

### <a name="ad-fs-extranet-smart-lockout-events"></a>AD FS Extranet-Smart Lockout-Ereignisse.

>[!NOTE]
> Problembehandlung für die Extranet-Smart Sperrungs mit dem Handbuch zur Problembehandlung für die [AD FS-Hilfe-Extranet](https://adfshelp.microsoft.com/TroubleshootingGuides/Workflow/a73d5843-9939-4c03-80a1-adcbbf3ccec8)

Für das Schreiben von extranetsmarlockout-Ereignissen muss die Funktion im Modus "nur Protokoll" oder "erzwingen" aktiviert werden, und die ADFS-Sicherheitsüberwachung ist aktiviert.
AD FS schreibt extranetsperrungsereignisse in das Sicherheits Überwachungs Protokoll:
- Wenn ein Benutzer gesperrt ist (erreicht den Sperr Schwellenwert für fehlgeschlagene Anmeldeversuche)
- Wenn AD FS einen Anmeldeversuch für einen Benutzer empfängt, der sich bereits im Sperr Zustand befindet

Im Modus "nur Protokoll" können Sie das Sicherheits Überwachungs Protokoll auf Sperr Ereignisse überprüfen. Für gefundene Ereignisse können Sie den Benutzer Zustand mithilfe des Cmdlets Get-adfsaccountactivity überprüfen, um festzustellen, ob die Sperre von vertrauten oder unbekannten IP-Adressen aufgetreten ist, und die Liste der vertrauten IP-Adressen für diesen Benutzer zu überprüfen.


|Ereignis-ID|BESCHREIBUNG|
|-----|-----|
|1203|Dieses Ereignis wird für jeden ungültigen Kennwort-Versuch geschrieben. Sobald BadPwdCount den in extranetlockoutthreshold angegebenen Wert erreicht, wird das Konto für die in extranetobservationwindow angegebene Dauer in ADFS gesperrt.</br>Aktivitäts-ID: %1</br>XML: %2|
|1201|Dieses Ereignis wird jedes Mal geschrieben, wenn ein Benutzer gesperrt wird. </br>Aktivitäts-ID: %1</br>XML: %2|
|557 (ADFS 2019)| Fehler beim Versuch, mit dem Konto Speicher-Rest-Dienst auf dem Knoten %1 zu kommunizieren. Wenn es sich um eine wid-Farm handelt, ist der primäre Knoten möglicherweise offline. Wenn es sich um eine SQL-Farm handelt, wählt ADFS automatisch einen neuen Knoten zum Hosten der Benutzerspeicher-Master Rolle aus.|
|562 (ADFS 2019)|Fehler bei der Kommunikation mit dem Konto Speicher Endpunkt auf Server "%1".</br>Ausnahme Meldung: %2|
|563 (ADFS 2019)|Beim Berechnen des extranetsperrungsstatus ist ein Fehler aufgetreten. Aufgrund des Werts der Einstellung %1 wird die Authentifizierung für diesen Benutzer zugelassen, und die Tokenausstellung wird fortgesetzt. Wenn es sich um eine wid-Farm handelt, ist der primäre Knoten möglicherweise offline. Wenn es sich um eine SQL-Farm handelt, wählt ADFS automatisch einen neuen Knoten zum Hosten der Benutzerspeicher-Master Rolle aus.</br>Name des Konto Speicher Servers: %2</br>Benutzer-ID: %3</br>Ausnahme Meldung: %4|
|512|Das Konto für den folgenden Benutzer ist gesperrt. Ein Anmeldeversuch ist aufgrund der Systemkonfiguration zulässig.</br>Aktivitäts-ID: %1 </br>Benutzer: %2 </br>Client-IP: %3 </br>Anzahl fehlerhafter Kenn Wörter: %4  </br>Letzter fehlerhafter Kenn Wort Versuch: %5|
|515|Das folgende Benutzerkonto befand sich in einem gesperrten Zustand, und es wurde nur das richtige Kennwort angegeben. Dieses Konto ist möglicherweise kompromittiert.</br>Zusätzliche Daten </br>Aktivitäts-ID: %1 </br>Benutzer: %2 </br>Client-IP: %3 |
|516|Das folgende Benutzerkonto wurde aufgrund zu vieler fehlerhafter Kenn Wort Versuche gesperrt.</br>Aktivitäts-ID: %1  </br>Benutzer: %2  </br>Client-IP: %3  </br>Anzahl fehlerhafter Kenn Wörter: %4  </br>Letzter fehlerhafter Kenn Wort Versuch: %5|

## <a name="esl-frequently-asked-questions"></a>Häufig gestellte Fragen zu ESL

**Wird eine AD FS-Farm mit Extranet Smart Lockout im Erzwingungs Modus jemals böswillige Benutzer sperren sehen?** 

A: Wenn für die AD FS-Smart Lockout der Modus "erzwingen" festgelegt ist, wird das Konto des berechtigten Benutzers nie durch Brute-Force-oder Denial-of-Service gesperrt. Die einzige Möglichkeit, dass eine böswillige Konto Sperre verhindert, dass eine Benutzeranmeldung möglich ist, besteht darin, dass der ungültige Akteur über das Benutzer Kennwort verfügt oder Anforderungen von einer bekannten, vertrauten (vertrauten) IP-Adresse für diesen Benutzer senden kann. 

**Was geschieht, wenn ESL aktiviert ist und der ungültige Akteur ein Benutzer Kennwort hat?** 

A: das typische Ziel des Brute-Force-Angriffs Szenarios besteht darin, ein Kennwort zu erraten und sich erfolgreich anzumelden.Wenn ein Benutzer ein Kennwort enthält oder ein Kennwort erraten wird, blockiert das ESL-Feature den Zugriff nicht, da die Anmeldung den "erfolgreichen" Kriterien des korrekten Kennworts und der neuen IP-Adresse entspricht. Die IP-Adresse des ungültigen Actors würde dann als "vertrauter" angezeigt werden.Die beste Entschärfung in diesem Szenario besteht darin, die Aktivität des Benutzers in AD FS zu löschen und die Multi-Factor Authentication für die Benutzer anzufordern. Es wird dringend empfohlen, den Aad-Kenn Wort Schutz zu installieren, mit dem sichergestellt wird, dass die Kenn Wörter nicht in das System

**Wenn sich der Benutzer nie erfolgreich von einer IP-Adresse angemeldet hat und dann mehrmals versucht, sich mit einem falschen Kennwort anzumelden?** 

A: Wenn ein Benutzer mehrere ungültige Kenn Wörter übermittelt (d. h. die falsche Typisierung) und bei folgendem Versuch das Kennwort richtig ist, wird der Benutzer sich sofort erfolgreich anmelden. Dadurch wird die Anzahl fehlerhafter Kenn Wörter gelöscht und dieser IP-Adresse hinzugefügt.Wenn Sie jedoch den Schwellenwert fehlerhafter Anmeldungen über den unbekannten Speicherort überschreiten, werden Sie in den Sperr Zustand versetzt, und Sie müssen auf das Überwachungs Fenster warten und sich mit einem gültigen Kennwort anmelden, oder es muss ein Administrator Eingriff erforderlich sein, um Ihr Konto zurückzusetzen.

**Funktioniert ESL auch im Intranet?**

A: Wenn die Clients eine direkte Verbindung mit den AD FS-Servern herstellen und nicht über webanwendungsproxy-Server, gilt das ESL-Verhalten nicht. 

**Ich sehe Microsoft-IP-Adressen im Feld "Client-IP". Blockiert die ESL-Angriffe mit Brute-Force-Angriffen.**  

A: ESL funktioniert gut, um Exchange Online-oder andere ältere Authentifizierungs Szenarien für Brute-Force-Angriffe zu verhindern. Eine Legacy Authentifizierung hat eine "Aktivitäts-ID" von 00000000-0000-0000-0000-000000000000.In diesen Angriffen nutzt der schlechte Akteur die Exchange Online-Standard Authentifizierung (auch als ältere Authentifizierung bezeichnet), sodass die Client-IP-Adresse als Microsoft-Adresse angezeigt wird. Die Exchange Online-Server im cloudproxy die Authentifizierungs Überprüfung für den Outlook-Client. In diesen Szenarien wird die IP-Adresse des bösartigen submitters in "x-ms-weitergeleitet-Client-IP" angezeigt, und die IP-Adresse von Microsoft Exchange Online Server ist im Wert x-MS-Client-IP.
Extranet Smart Lockout überprüft Netzwerk-IP-Adressen, weitergeleitete IPS, den Wert x-weitergeleitete Client-IP und den Wert x-MS-Client-IP. Wenn die Anforderung erfolgreich ist, werden alle IPS der vertrauten Liste hinzugefügt. Wenn eine Anforderung empfangen wird und eine der dargestellten IPS nicht in der vertrauten Liste enthalten ist, wird die Anforderung als unbekannt gekennzeichnet. Der vertraute Benutzer kann sich erfolgreich anmelden, während Anforderungen von den unbekannten Standorten blockiert werden.

**Kann ich die Größe von „ADFSArtifactStore“ vor dem Aktivieren von ESL schätzen?**

A: bei aktiviertem ESL werden AD FS die Kontoaktivität und die bekannten Speicherorte für Benutzer in der adfsartifactstore-Datenbank nachverfolgt. Die Größe dieser Datenbank wird relativ zur Anzahl der nachverfolgten Benutzer und bekannten Standorte skaliert. Beim Planen der Aktivierung von ESL können Sie die Größenzunahme für die ADFSArtifactStore-Datenbank auf eine Rate von bis zu 1 GB pro 100.000 Benutzer schätzen. Wenn die AD FS-Farm die interne Windows-Datenbank (WID) verwendet, lautet der Standard Speicherort für die Datenbankdateien c:\windows\wid\data\. Um das Auffüllen dieses Laufwerks zu verhindern, stellen Sie sicher, dass mindestens 5 GB freier Speicherplatz verfügbar sind, bevor Sie ESL aktivieren. Planen Sie zusätzlich zum Datenträgerspeicher, dass der gesamte Prozessspeicher nach der Aktivierung von ESL um bis zu weitere 1 GB RAM für Benutzerauffüllungen von maximal 500.000 größer wird.


## <a name="additional-references"></a>Weitere Verweise
[Bewährte Methoden zum Sichern von Active Directory-Verbunddienste (AD FS)](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-ADF sproperties](/powershell/module/adfs/set-adfsproperties?view=win10-ps)

[AD FS-Vorgänge](../ad-fs-operations.md)
