---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: Konfigurieren von AD FS-Extranetsperrschutz
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 05/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eb31a76dbd7ccdff3ea3ee0d6bb26f9ee16ae93f
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280704"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS Extranet Lockout und intelligente Extranetsperre

## <a name="overview"></a>Übersicht

Extranet Smart Lockout zusammenfassender Meldung schützt Ihre Benutzer über das extranet kontosperrung vor bösartigen Aktivitäten auftreten.  

Zusammenfassender Meldung können AD FS zwischen Anmeldeversuchen von einem bekannten Speicherort für einen Benutzer und Anmeldeversuchen von Angreifern möglicherweise unterscheiden. AD FS können Angreifer Sperren während der gültigen Benutzer weiterhin ihren Konten zu verwenden. Dies verhindert und schützt vor Denial-of-Service und bestimmte Klassen von Sprühende Angriffe auf Kennwörter für den Benutzer. Zusammenfassender Meldung ist für AD FS unter Windows Server 2016 verfügbar und AD FS unter Windows Server-2019 integriert ist.

Zusammenfassender Meldung ist nur verfügbar, für den Benutzernamen und Kennwort-authentifizierungsanforderungen, die über das extranet, mit der Web Application Proxy oder a 3rd stammen party Proxy. Alle 3rd Party Proxy muss das MS-ADFSPIP Protokoll anstelle des Webanwendungsproxys, verwendet werden, z. B. unterstützen [F5 BIG-IP Access Policy Manager](https://devcentral.f5.com/s/articles/ad-fs-proxy-replacement-on-f5-big-ip-30191). Der Dokumentation 3rd Party Proxy um festzustellen, ob der Proxy des MS-ADFSPIP-Protokolls unterstützt.   

## <a name="additional-features-in-ad-fs-2019"></a>Zusätzliche Funktionen in AD FS 2019
Extranet Smart Lockout in AD FS-2019 fügt die folgenden Vorteile im Vergleich zu AD FS 2016 hinzu:
- Legen Sie unabhängige Sperre Schwellenwerte für die bekannten und unbekannten Standorten, damit Benutzer in gut an bekannten Speicherorten von verdächtigen Standorten mehr Platz für Fehler als Anforderungen haben
- Aktivieren der smart Lockout-Überwachungsmodus und weiterhin die vorherige vorläufig Sperre Verhalten zu erzwingen. Dadurch können Sie zu erfahren Sie mehr über die Benutzer vertrauten Standorte noch durch die extranetsperre-Funktion, die in AD FS 2012 R2 geschützt werden.  

## <a name="how-it-works"></a>So funktioniert es
### <a name="configuration-information"></a>Informationen zur Konfiguration
Wenn zusammenfassender Meldung aktiviert ist, wird eine neue Tabelle in der Datenbank AdfsArtifactStore.AccountActivity, Artefakt wird erstellt, und ein Knoten in der AD FS-Farm als Master "Benutzeraktivität" ausgewählt ist. In einer WID-Konfiguration ist diesem Knoten immer dem primären Knoten. In einer SQL-Konfiguration wird ein Knoten ausgewählt, werden von der Benutzeraktivität Master.  

Als Master Benutzeraktivität ausgewählten Knotens an. Get-AdfsFarmInformation.FarmRoles

Alle sekundären Knoten werden wenden Sie sich an den Masterknoten für jede neue melden Sie sich über Port 80, um den aktuellen Wert der Zählungen ungültiger Kennwörter und neuen Werte der bekannten Speicherort zu erfahren, und Sie diesen Knoten zu aktualisieren, nachdem die Anmeldung verarbeitet wurde.

![Konfiguration](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 Wenn den Master der sekundäre Knoten hergestellt werden kann, wird es Fehlerereignisse in das AD FS-Admin-Protokoll schreiben. Authentifizierungen weiterhin verarbeitet werden, aber AD FS wird nur den aktualisierten Zustand lokal schreiben. AD FS wenden Sie sich an den Master alle 10 Minuten wiederholt, und wechselt zurück zum Master, sobald der Master verfügbar ist.

### <a name="terminology"></a>Terminologie
- **FamiliarLocation**: Während eine Authentifizierungsanforderung überprüft zusammenfassender Meldung an, dass alle IP-Adressen angezeigt. Diese IP-Adressen wird eine Kombination von Netzwerk-IP, IP-Adresse weitergeleitet und die optionale X-forwarded-for IP-Adresse sein. Wenn die Anforderung erfolgreich ist, werden alle der IP-Adressen der Kontoaktivität-Tabelle als "bekannte IP-Adressen" hinzugefügt. Wenn die Anforderung alle IP-Adressen in den "bekannte IP-Adressen" vorhanden ist, wird die Anforderung als "Vertraute" Speicherort behandelt.
- **UnknownLocation**: Wenn eine eingehende Anforderung mindestens eine IP-Adresse nicht vorhanden ist, in der Liste der vorhandenen "FamiliarLocation" verfügt, wird die Anforderung als "Unbekannt" Standort behandelt werden. Dies ist für Proxyfunktion Szenarios wie z. B. ältere Exchange Online-Authentifizierung, in dem Exchange Online Adressen erfolgreiche und fehlerhafte Anforderungen verarbeiten.  
- **badPwdCount**: Ein Wert, der Anzahl der Häufigkeit, mit die ein falsches Kennwort übermittelt wurde und die Authentifizierung war nicht erfolgreich. Für jeden Benutzer werden separate Leistungsindikatoren für die vertrauten Standorte und unbekannte Standorte beibehalten.
- **UnknownLockout**: Ein boolescher Wert pro Benutzer, wenn der Benutzer den Zugriff auf von unbekannten Standorten gesperrt ist. Dieser Wert wird basierend auf den ExtranetLockoutThreshold-Werten und BadPwdCountUnfamiliar berechnet.
- **ExtranetLockoutThreshold**: Dieser Wert bestimmt die maximale Anzahl der Versuche mit falschem Kennwort. Wenn der Schwellenwert erreicht wird, lehnt AD FS Anforderungen aus dem extranet, bis das Fenster Beobachtung verstrichen ist.
- **ExtranetObservationWindow**: Dieser Wert bestimmt die Dauer, die Benutzernamen und das Kennwort-Anforderungen von unbekannten Standorten gesperrt sind. Wenn das Fenster verstrichen ist, startet der AD FS Authentifizierung mit Benutzername und Kennwort erneut von unbekannten Standorten durchführen.
- **ExtranetLockoutRequirePDC**: Wenn aktiviert, erfordert extranetsperre primärer Domänencontroller (PDC). Wenn deaktiviert, extranetsperre erfolgt ein Fallback auf einen anderen Domänencontroller für den Fall, dass der PDC nicht verfügbar ist.  
- **ExtranetLockoutMode**: Melden Sie Steuerelemente nur erzwungen und Modus der Extranet Smart Lockout
    - **ADFSSmartLockoutLogOnly**: Extranet Smart Lockout ist aktiviert, aber AD FS nur Admin zu schreiben und Überwachen von Ereignissen, aber die authentifizierungsanforderungen nicht ablehnen. In diesem Modus anfänglich für FamiliarLocation aufgefüllt werden, bevor 'ADFSSmartLockoutEnforce' aktiviert ist, aktiviert werden soll.
    - **ADFSSmartLockoutEnforce**: Vollständige Unterstützung für unbekannte authentifizierungsanforderungen blockiert, wenn Schwellenwerte erreicht sind.

IPv4 und IPv6-Adressen werden unterstützt.

### <a name="anatomy-of-a-transaction"></a>Anatomie einer Transaktion
- **Überprüfen Sie vor der Authentifizierung**: Während eine Authentifizierungsanforderung überprüft zusammenfassender Meldung an, dass alle IP-Adressen angezeigt. Diese IP-Adressen wird eine Kombination von Netzwerk-IP, IP-Adresse weitergeleitet und die optionale X-forwarded-for IP-Adresse sein. In den Überwachungsprotokollen finden Sie diese IP-Adressen in der <IpAddress> Feld in der Reihenfolge der X-ms-forwarded-Client-Ip, X-forwarded-for, X-ms-Proxy-Client-Ip.

  AD FS auf Grundlage dieser IP-Adressen bestimmt werden, wenn die Anforderung von einem Standort vertraut sind oder nicht vertraut stammt, und klicken Sie dann überprüft, ob die entsprechenden BadPwdCount kleiner als der festgelegte Schwellenwert-Limit, oder wenn die letzte **Fehler** Versuch aufgetreten ist, ist länger als die Zeitrahmen Beobachtung-Fenster. Wenn eine der folgenden Bedingungen wahr ist, wird AD FS können diese Transaktion zur weiteren Verarbeitung und Überprüfung von Anmeldeinformationen. Wenn beide Bedingungen false sind, ist das Konto bereits in einem gesperrten Zustand, bis das Fenster Beobachtung übergibt. Nachdem das Fenster Beobachtung erfolgreich ist, darf der Benutzer einem Wiederholungsversuch für die Authentifizierung. Beachten Sie, dass in 2019, AD FS auf die geeignete schwellenwertbeschränkung basierend auf geprüft wird, wenn die IP-Adresse einen bekannten Speicherort, oder nicht entspricht.
- **Erfolgreiche Anmeldung**: Wenn die Anmeldung erfolgreich ausgeführt wird, klicken Sie dann die IP-Adressen aus der Anforderung werden des Benutzers bekannten Speicherort IP-Liste hinzugefügt.  
- **Fehler bei der Anmeldung**: Wenn die Anmeldung die BadPwdCount schlägt fehl, wird erhöht. Der Benutzer wird in den Status der Sperre wechseln, wenn der Angreifer mehrere falsche Kennwörter auf das System sendet als der Schwellenwert zulässt. (BadPwdCount > ExtranetLockoutThreshold)  

![Konfiguration](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

Auf "true" wird der Wert "UnknownLockout" entspricht, wenn das Konto gesperrt ist. Dies bedeutet, dass des Benutzers BadPwdCount über dem Schwellenwert. d. h., dass eine Person mehr Kennwörter als vom System zugelassen wird versucht. In diesem Status sind 2 Methoden, mit denen ein gültiger Benutzer anmelden kann.
- Der Benutzer muss die ObservationWindow Zeit verstreichen warten oder
- Um den Status der Sperre zurücksetzen zu können, müssen zurücksetzen Sie die BadPwdCount auf 0 (null) mit "Reset-ADFSAccountLockout".

Wenn kein Zurücksetzen von Kennwörtern auftreten, wird das Konto einen einziges kennwortantwortversuch in AD für jedes Fenster Beobachtung zugelassen. Das Konto gibt zurück, die in den gesperrten Zustand nach, die versuchen, um das Fenster Beobachtung neu gestartet werden. Der Wert BadPwdCount wird nur automatisch nach einer Anmeldung Kennwort erfolgreich zurückgesetzt.

### <a name="log-only-mode-versus-enforce-mode"></a>Nur-Log-Modus im Vergleich zu "Erzwingen"-Modus
In der Tabelle AccountActivity wird sowohl während der "Nur Log" und "Erzwingen" Modus aufgefüllt. Wenn "Nur Log"-Modus wird umgangen, und zusammenfassender Meldung direkt in den Modus "Erzwingen", ohne die empfohlene Wartezeit verschoben wird, wird die bekannte IP-Adressen der Benutzer auf AD FS nicht bekannt ist. In diesem Fall würde zusammenfassender Meldung Verhalten sich wie "ADBadPasswordCounter" berechtigten Benutzer-Datenverkehr möglicherweise blockiert, wenn das Benutzerkonto, das eine aktive brute-Force-Angriff ausgesetzt ist. Wenn der Modus 'Log-Only' umgangen wird, und der Benutzer einen gesperrten Zustand mit "UnknownLockout gibt" = "true", und versucht, melden Sie sich mit einem sicheren Kennwort von einer IP-Adresse, die nicht in der Liste der "vertraute" IP-, dann ist sie nicht anmelden können. Modus "nur Log" empfiehlt sich 3 – 7 Tage lang, um dieses Szenario zu vermeiden. Wenn Konten aktiv einem Angriff ausgesetzt sind, ist mindestens 24 Stunden 'Log-Only'-Modus erforderlich, um Sperrungen auf berechtigte Benutzer zu verhindern.  

## <a name="extranet-smart-lockout-configuration"></a>Der Smart Lockout Extranet-Konfiguration  

### <a name="prerequisites-for-ad-fs-2016"></a>Voraussetzungen für AD FS 2016

1. **Installieren von Updates auf allen Knoten in der farm**

   Stellen Sie zunächst sicher, alle Windows Server 2016 AD FS-Server auf dem neuesten Stand zum Zeitpunkt der Windows-Updates von Juni 2018 sind und dass die AD FS 2016-Farm an die verhaltensebene 2016-Farm ausgeführt wird.
1. **Überprüfen Sie die Berechtigungen**

   Der Smart Lockout Extranet erfordert, dass es sich bei Windows-Remoteverwaltung ist auf jedem AD FS-Server aktiviert.
3. **Aktualisieren der Artefakt-Datenbankberechtigungen**

   Der smart Lockout Extranet erfordert der AD FS-Dienstkonto Berechtigungen zum Erstellen einer neuen Tabelle in der AD FS-Artefakt-Datenbank verfügen. Melden Sie sich bei jedem AD FS-Server als AD FS-Administrator, und klicken Sie dann mit dieser Berechtigung durch Ausführen der folgenden Befehle in einem PowerShell-Eingabeaufforderungsfenster aus:

   ``` powershell
   PS C:\>$cred = Get-Credential
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
   ```
   >[!NOTE]
   >Der Platzhalter $cred ist ein Konto, das AD FS über Administratorberechtigungen verfügt. Dies sollte die Write-Berechtigungen zum Erstellen der Tabelle bereitstellen.

   Die oben genannten Befehle können aufgrund der über ausreichende Berechtigungen verfügen, da AD FS-Farm von SQL Server mithilfe wird und die oben angegebene Anmeldeinformationen keine Administratorberechtigungen auf dem SQLServer nicht. In diesem Fall können Sie Berechtigungen für die Datenbank manuell konfigurieren in SQL Server-Datenbank durch den folgenden Befehl ausführen, wenn Sie mit der Datenbank AdfsArtifactStore verbunden sind.
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

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>Stellen Sie sicher, dass AD FS-Sicherheit-Überwachungsprotokollierung aktiviert ist
Dieses Feature macht Sicherheitsüberwachung verwenden, die in AD FS als auch für die lokale Richtlinie für alle AD FS-Server anmeldet, also die Überwachung aktiviert werden müssen.

### <a name="configuration-instructions"></a>Konfigurationsanweisungen
Extranet Smart Lockout verwendet, die AD FS-Eigenschaft **ExtranetLockoutEnabled**. Diese Eigenschaft wurde zuvor in Steuerelement "Soft Extranetsperrung" in Server 2012 R2 verwendet. Wenn weiche Extranetsperre aktiviert wurde, führen Sie zum Anzeigen der aktuellen Eigenschaftenkonfiguration ` Get-AdfsProperties` .

### <a name="configuration-recommendations"></a>Konfigurationsempfehlungen
Wenn Sie das Extranet Smart Lockout zu konfigurieren, führen Sie die best Practices für das Festlegen von Schwellenwerten für:  

`ExtranetObservationWindow (new-timespan -Minutes 30)`

`ExtranetLockoutThreshold: – 2x AD Threshold Value`

AD-Wert: 20, ExtranetLockoutThreshold: 10

Active Directory-kontosperrung ist unabhängig von der Extranet-Smart Lockout verwendet werden. Jedoch, wenn Active Directory-Sperre aktiviert ist, ExtranetLockoutThreshold in AD FS < Kontensperrungsschwelle in Active Directory

`ExtranetLockoutRequirePDC - $false`

Wenn aktiviert, erfordert extranetsperre primärer Domänencontroller (PDC). Wenn deaktiviert, und als "false" konfiguriert, extranetsperre erfolgt ein Fallback auf einen anderen Domänencontroller für den Fall, dass der PDC nicht verfügbar ist.

So legen Sie diese Eigenschaft führen fest:

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```
### <a name="enable-log-only-mode"></a>Nur-Log-Modus aktivieren

Im Log-Modus nur AD FS liefern Informationen für Benutzer bekannten Speicherort und schreibt Sicherheitsüberwachungsereignisse, aber keine Anforderungen blockiert. Dieser Modus wird verwendet, um sicherzustellen, dass der smart Lockout ausgeführt wird, und zum Aktivieren von AD FS "vertrauten Standorte für Benutzer vor dem Aktivieren der erfahren," "erzwingen". Wie AD FS lernt, speichert er Anmeldeaktivität pro Benutzer (angibt, ob im Protokollmodus oder im).
Legen Sie die Sperre Verhaltens, melden Sie sich nur durch das folgende Cmdlet ausführen.  

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly`

Nur den Protokollmodus richtet sich an einen temporären Zustand sein, damit das System Anmeldung Verhalten vor der Einführung in die Erzwingung der Sperre mit dem Verhalten der smart Lockout erfahren kann. Die empfohlene Dauer für eine nur-Log-Modus ist 3 – 7 Tage. Wenn Konten aktiv einem Angriff ausgesetzt sind, muss der Modus "nur Log" für mindestens 24 Stunden ausgeführt werden.

AD FS 2016 Wenn 2012R2 "Soft Extranetsperre" Verhalten aktiviert ist, vor der Aktivierung der Smart Lockout Extranet, wird nur Log-Modus das "Vorläufig Extranetsperre" Verhalten deaktiviert. Smart Lockout für AD FS wird Benutzer im Modus "nur Log" nicht gesperrt werden. Allerdings das lokale AD den Benutzer basierend auf der AD-Konfiguration sperren kann. Überprüfen Sie die AD-Kontosperrungsrichtlinien zu erfahren, wie für lokale AD können Benutzer der Sperre.

AD FS-2019 ein weiterer Vorteil besteht, können Protokolldateien reiner Schutzmodus für smart Lockout zu aktivieren, während Sie weiterhin das vorherige vorläufig Sperre Verhalten mit erzwingen die unterhalb von Powershell.

`Set-AdfsProperties -ExtranetLockoutMode 3`

Starten Sie für den neuen Modus wirksam wird die AD FS-Dienst auf allen Knoten in der Farm neu

`Restart-service adfssrv`

Sobald der Modus konfiguriert ist, können Sie mithilfe des Parameters EnableExtranetLockout der smart Lockout aktivieren.

`Set-AdfsProperties -EnableExtranetLockout $true`

### <a name="enable-enforce-mode"></a>Enable erzwingen

Nachdem Sie mit der Sperre Schwellenwert und die Beobachtung Fenster vertraut sind, kann zusammenfassender Meldung verschoben werden, im Modus "erzwingen", mit dem folgenden PSH-Cmdlet:

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce`

Für den neuen Modus wirksam wird starten Sie den AD FS-Dienst auf allen Knoten in der Farm mithilfe des folgenden Befehls neu.

`Restart-service adfssrv`

## <a name="manage-user-account-activity"></a>Verwalten von Aktivitäten der Benutzer-Konto
AD FS bietet drei Cmdlets zum Verwalten von Kontodaten-Aktivität. Diese Cmdlets verbinden sich automatisch auf den Knoten in der Farm, die die Rolle enthält.
>[!NOTE]
>Just Enough Administration (JEA) Dient zum Delegieren von AD FS-Cmdlets, um kontosperrungen zurückzusetzen. Helpdesk-Personal können z. B. delegierten Berechtigungen zusammenfassender Meldung-Cmdlets zu verwenden sein. Weitere Informationen über das Delegieren von Berechtigungen für die Verwendung dieser Cmdlets finden Sie unter [delegieren AD FS Powershell-Cmdlet des Zugriffs auf Benutzer ohne Administratorrechte](delegate-ad-fs-pshell-access.md)

Dieses Verhalten kann überschrieben werden, übergeben den - Server-Parameter.

- Get-ADFSAccountActivity -UserPrincipalName

  Lesen Sie die aktuellen Konto-Aktivität für ein Benutzerkonto an. Das Cmdlet verbindet sich mit dem Konto Aktivität REST-Endpunkt immer automatisch mit dem Master für die Farm. Aus diesem Grund sollten alle Daten stets konsistent sein.

`Get-ADFSAccountActivity user@contoso.com`

  Eigenschaften:
    - BadPwdCountFamiliar: Inkrementiert, wenn eine Authentifizierung erfolgreich, aus einem bekannten Speicherort ist.
    - BadPwdCountUnknown: Inkrementiert, wenn eine Authentifizierung von einem unbekannten Speicherort nicht erfolgreich ist.
    - LastFailedAuthFamiliar: Wenn die Authentifizierung von einem bekannten Speicherort nicht erfolgreich war, wird LastFailedAuthUnknown zum Zeitpunkt der nicht erfolgreichen Authentifizierung festgelegt.
    - LastFailedAuthUnknown: Wenn die Authentifizierung von einem unbekannten Speicherort nicht erfolgreich war, wird LastFailedAuthUnknown zum Zeitpunkt der nicht erfolgreichen Authentifizierung festgelegt.
    - FamiliarLockout: Boolescher Wert, der "True" werden wird, wenn die "BadPwdCountFamiliar" > ExtranetLockoutThreshold
    - UnknownLockout: Boolescher Wert, der "True" werden wird, wenn die "BadPwdCountUnknown" > ExtranetLockoutThreshold  
    - FamiliarIPs: bis zu 20 IP-Adressen für den Benutzer vertraut sind. Wenn dieser Wert überschritten wird, wird die älteste IP-Adresse in der Liste entfernt werden.
-    Set-ADFSAccountActivity

     Fügt neue vertrauten Standorte hinzu. Der bekannte IP-Liste verfügt maximal möglichen 20 Einträgen, wenn diese überschritten wird, die älteste IP-Adresse in der Liste entfernt werden.

`Set-ADFSAccountActivity user@contoso.com -AdditionalFamiliarIps “1.2.3.4”`

- Reset-ADFSAccountLockout

  Der Zähler für kontosperrung für ein Benutzerkonto für jeden bekannten Speicherort (BadPwdCountFamiliar) oder einen unbekannten Ort Leistungsindikatoren (BadPwdCountUnfamiliar) zurückgesetzt. Wenn Sie einen Indikator zurücksetzen, wird der Wert "FamiliarLockout" oder "UnfamiliarLockout" aktualisiert, da Zähler zurücksetzen kleiner als der Schwellenwert sind.  

`Reset-ADFSAccountLockout user@contoso.com -Location Familiar`
`Reset-ADFSAccountLockout user@contoso.com -Location Unknown`

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>Protokollierung von Komponentenereignissen und Aktivität der Benutzerinformationen für AD FS Extranet Lockout

### <a name="connect-health"></a>Connect Health
Die empfohlene Methode zum Überwachen der Benutzeraktivität-Konto erfolgt über Connect Health. Connect Health generiert herunterladbare Berichte zu riskanten IP-Adressen und erfolgte Eingaben falscher Kennwörter. Jedes Element im Bericht riskante IP-Adresse zeigt zusammengefasste Informationen zu fehlgeschlagenen AD FS-Anmeldeaktivitäten, die angegebene Schwellenwert überschritten. E-Mail-Benachrichtigungen können Administratoren festgelegt werden, als dies mit anpassbaren e-Mail-Einstellungen auftritt. Weitere Informationen und Anweisungen zur Einrichtung finden Sie auf die [Connect Health-Dokumentation](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs).

### <a name="ad-fs-extranet-smart-lockout-events"></a>AD FS Extranet Smart Lockout-Ereignisse.
Für Extranet Smart Lockout-Ereignisse zu schreibender zusammenfassender Meldung muss aktiviert sein, im Modus "nur Log" oder "erzwingen" aus, und AD FS-sicherheitsüberwachung aktiviert ist.
AD FS werden extranet Lockout Ereignisse in das Sicherheitsprotokoll für die Überwachung geschrieben werden:
- Wenn ein Benutzer gesperrt ist (der Schwellenwert für kontosperrung erreicht, für nicht erfolgreiche Anmeldeversuche) Out
- Wenn AD FS ein Anmeldeversuch eines Benutzers erhält, die bereits im Zustand der Sperre ist

Klicken Sie im Protokollmodus, können Sie das Sicherheitsprotokoll für Sperrereignisse überprüfen. Für alle Ereignisse, die gefunden wird können Sie überprüfen, den Benutzerzustand mit, dass das Cmdlet Get-ADFSAccountActivity zu bestimmen, ob die Sperre von vertraut sind oder unbekannten IP-Adressen, und überprüfen die Liste der vertrauten IP-Adressen für diesen Benutzer aufgetreten ist.


|Ereignis-ID|Beschreibung|
|-----|-----|
|1203|Dieses Ereignis wird für jede Kennworteingabeversuchen geschrieben. Werden, sobald die BadPwdCount in ExtranetLockoutThreshold angegebenen Wert erreicht, wird das Konto werden in AD FS für die festgelegte ExtranetObservationWindow gesperrt.</br>Aktivitäts-ID: %1</br>XML: %2|
|1201|Dieses Ereignis wird jedes Mal ein Benutzer gesperrt wird geschrieben. </br>Aktivitäts-ID: %1</br>XML: %2|
|557 (ADFS 2019)| Fehler beim Versuch, die Kommunikation mit dem Konto Speicher-Rest-Dienst auf Knoten %1. Ist dies eine WID-Farm kann der primäre Knoten offline sein. Wählen Sie einen neuen Knoten zum Hosten der master-Speicher-Benutzerrolle, wenn es sich um eine SQL-Farm handelt, die AD FS automatisch wird.|
|562 (ADFS 2019)|Fehler beim Speichern Anschlussnummer, mit dem Konto Endpunkt auf dem Server %1.</br>Ausnahmemeldung: %2|
|563 (ADFS 2019)|Fehler beim Berechnen der extranet Lockout Status. Weil der Wert von %1 Einstellung Authentifizierung kann für diesen Benutzer aus, und tokenausstellung wird fortgesetzt. Ist dies eine WID-Farm kann der primäre Knoten offline sein. Wählen Sie einen neuen Knoten zum Hosten der master-Speicher-Benutzerrolle, wenn es sich um eine SQL-Farm handelt, die AD FS automatisch wird.</br>Kontoname für Store-Server: %2</br>Benutzer-Id: %3</br>Ausnahmemeldung: %4|
|512|Das Konto für die folgenden ist gesperrt. Aufgrund der Systemkonfiguration wird ein Anmeldeversuch kann.</br>Aktivitäts-ID: %1 </br>Benutzer: %2 </br>Client-IP-: %3 </br>Anzahl falscher Kennwörter: %4  </br>Der letzten fehlerhaften Kennworteingabe: %5|
|515|Das folgende Benutzerkonto wurde in einem gesperrten Zustand aus, und das richtige Kennwort nur bereitgestellt wurde. Dieses Konto möglicherweise beeinträchtigt.</br>Weitere Daten </br>Aktivitäts-ID: %1 </br>Benutzer: %2 </br>Client-IP-: %3 |
|516|Das folgende Benutzerkonto wurde aufgrund von zu viele Versuche mit falschem Kennwort gesperrt wurde.</br>Aktivitäts-ID: %1  </br>Benutzer: %2  </br>Client-IP-: %3  </br>Anzahl falscher Kennwörter: %4  </br>Der letzten fehlerhaften Kennworteingabe: %5|

## <a name="esl-frequently-asked-questions"></a>Zusammenfassender Meldung – häufig gestellte Fragen

**Erzwingt eine AD FS-Farm mithilfe der Smart Lockout im Extranet Modus böswilliger Benutzer Sperrungen jemals feststellen?** 

A: Wenn AD FS-Smart Lockout "im durchsetzungsmodus erreicht," das berechtigte Konto des Benutzers gesperrt durch brute-Force- oder einen Denial of Service nie angezeigt festgelegt ist. Die einzige Möglichkeit, die, der einen böswilligen kontosperrung eine Benutzeranmeldung verhindern kann, ist, wenn die böswilliger Benutzer das Kennwort des Benutzers oder kann Anforderungen für diesen Benutzer aus einer bekannten guten (vertraut) IP-Adresse senden. 

**Was geschieht, zusammenfassender Meldung aktiviert ist und die böswilliger Benutzer ein Benutzerkennwort?** 

A: Typische Ziel des brute-Force-Angriffsszenarios ist es, ein Kennwort zu erraten, und melden Sie sich erfolgreich.  Wenn ein Benutzer phishingziel ist oder ein Kennwort erraten wird Klicken Sie dann blockiert die zusammenfassender Meldung-Funktion nicht den Zugriff, da die Anmeldung "war erfolgreich." das richtige Kennwort und die neue IP-Adresse Kriterium wird. Die Angreifer IP-Adresse wird dann als "vertraute" angezeigt. In diesem Szenario die beste Lösung ist, löschen die Aktivität des Benutzers in AD FS und Multi-Factor Authentication für den Benutzer erforderlich machen. Es wird dringend empfohlen, installieren die AAD-Kennwortschutz, die sicherstellt, dass keine zu erraten von Kennwörtern in das System erhalten.

**Wenn meine Benutzer noch nie angemeldet wurde erfolgreich von einer IP hat- und dann versucht, die mit einem falschen Kennwort mehrmals werden mehr anmelden, nachdem sie ihr Kennwort richtig Geben Sie zum Schluss?** 

A: Wenn ein Benutzer mehrere falsche Kennwörter (d. h. legitimen falsch eingibt) übermittelt auf der folgende Versuch Ruft das Kennwort richtig ab, und der Benutzer sind sofort erfolgreich, um sich anzumelden.  Wird die Anzahl falscher Kennwörter zu löschen und Hinzufügen dieser IP-Adresse der FamiliarIPs-Liste.  Jedoch wenn sie über dem Schwellenwert für fehlerhafte Anmeldungen von unbekannten Speicherort navigieren, sie Lockout Status wechselt, und sie müssen warten, hinter die Beobachtung-Fenster und melden Sie sich mit der ein gültiges Kennwort oder Administrator eingreifen, um ihr Konto zurückzusetzen.  

**Funktioniert zusammenfassender Meldung im Intranet zu?**   
A: Wenn die Clients direkt auf die AD FS-Server und nicht durch eine Webanwendungs-Proxyserver verbinden wird das Verhalten zusammenfassender Meldung nicht angewendet. 

**Ich sehe, dass Microsoft-IP-Adressen in das Client-IP-Feld. Erzwingt die zusammenfassender Meldung Block EXO-Proxy Brute Angriffen?**  

A: Zusammenfassender Meldung funktioniert gut, um Exchange Online oder anderen älteren Authentifizierungsszenarien brute-Force-Angriff zu verhindern. Eine ältere Authentifizierung hat "Aktivitäts-ID" 00000000-0000-0000-0000-000000000000. In diese Angriffe ab und ist die böswilliger Benutzer Exchange Online-Standardauthentifizierung (auch bekannt als legacy-Authentifizierung) nutzen, damit die Client-IP-Adresse als Microsoft eine angezeigt wird. Exchange online-Server an den Cloud-Proxy für den Outlook-Client die Überprüfung der Authentifizierung. In diesen Szenarien werden die IP-Adresse des Absenders böswillige in der X-ms-weitergeleitet-Client-Ip und die Microsoft Exchange Online-Server, den IP-Adresse in der X-ms-Client-Ip-Wert sein wird.
Extranet Smart Lockout überprüft Netzwerk IP-Adressen weitergeleitet, IP-Adressen, die X-forwarded-Client-IP und die X-ms-Client-Ip-Wert. Wenn die Anforderung erfolgreich ist, werden alle IP-Adressen, das die bekannte Liste hinzugefügt. Wenn eine Anforderung eingeht, und der angegebene IP-Adressen nicht in die bekannte Liste sind wird die Anforderung als unbekannte gekennzeichnet. Der Benutzer vertraute werden erfolgreich anmelden können, während die Anforderungen von unbekannten Standorten werden blockiert.  


## <a name="additional-references"></a>Weitere Verweise  
[Bewährte Methoden zum Schützen von Active Directory Federation Services](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
