---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: Konfigurieren von AD FS-Extranetsperrschutz
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 02/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 904b563da2f1404d873c7352db9eadb7bfe252f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869761"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS Extranet Lockout und intelligente Extranetsperre

# <a name="overview"></a>Übersicht

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

In AD FS unter Windows Server 2012 R2 ist eine Sicherheitsfunktion, die aufgerufen werden vorgestellt [vorläufig Extranetsperre](configure-ad-fs-extranet-soft-lockout-protection.md).  Mit diesem Feature wird AD FS Authentifizieren von Benutzern aus dem extranet für eine bestimmte Zeitspanne beendet.  Dadurch wird verhindert, dass Ihre Benutzerkonten in Active Directory gesperrt wird. Zusätzlich zum Schutz von Benutzern aus einer AD-kontosperrungen, schützt AD FS extranet Lockout auch Kennwortermittlung brute-Force-Angriffe.

Im Juni 2018 AD FS unter Windows Server 2016 eingeführt **Extranet Smart Lockout zusammenfassender Meldung**.  Zusammenfassender Meldung können AD FS, um die Anmeldeversuche scheinen von der gültigen Benutzer sein und bei Anmeldungen von einem Angreifer möglicherweise unterscheiden. Daher kann AD FS Angreifer Sperren während der gültigen Benutzer weiterhin ihren Konten zu verwenden. Dies verhindert Denial-of-Service für den Benutzer und schützt vor gezielten Angriffen wie z. B. "Kennwort-Sprühende"-Angriffe.  
Zusammenfassender Meldung ist für AD FS unter Windows Server 2016 verfügbar und AD FS unter Windows Server-2019 integriert ist.

> [!NOTE]
> Dieses Feature funktioniert nur für die **Extranetszenario** kommen Sie in der authentifizierungsanforderungen über den Webanwendungsproxy und gilt nur für **Benutzernamen-und Kennwortauthentifizierung**.

## <a name="advantages-of-extranet-smart-lockout-in-ad-fs-2016"></a>Vorteile von intelligenten Extranetsperren in AD FS 2016
Weiche extranetsperre in AD FS 2012 R2 bereitgestellt, die folgenden wichtigsten Vorteile:
- Schützt Ihre Benutzerkonten aus **Brute-force-Angriffe** in dem ein Angreifer versucht, das Kennwort eines Benutzers zu erraten, durch das Senden von authentifizierungsanforderungen kontinuierlich und von **Sprühende Kennwortangriffe** , in denen Angreifer versuchen häufig verwendeter Kennwörter mit vielen verschiedenen Konten verwenden
- Schützt Ihre Benutzerkonten aus **Active Directory-kontosperrung** böswillige authentifizierungsanforderungen durch falsche Kennwörter. In diesem Fall jedoch das Benutzerkonto, das für extranet-Zugriff gesperrt werden, die Benutzer kann weiterhin die Anmeldung bei AD vom Unternehmensnetzwerk. Dies bezeichnet man als ein **vorläufig Sperre**.

Extranet-Smart Lockout-Builds zu den Vorteilen von soft extranetsperren, indem Sie Folgendes hinzufügen:
- Schützt Ihre Benutzer vor Auftreten **extranet kontosperrung** böswillige authentifizierungsanforderungen.  Der Smart Lockout verhindert, dass potenziell schädliche Anforderungen von unbekannten Standorten gleichzeitig des echten Benutzers aus der vertrauten Standorte aus dem extranet anmelden (Standorte, die von dem der Benutzer erfolgreich angemeldet vor).
- Verfügt über einen Log-nur-Modus, sodass das System gute und potenziell bösartigen anmelden Aktivität erfahren kann, ohne das Deaktivieren von Konten

## <a name="additional-advantages-of-extranet-smart-lockout-in-ad-fs-2019"></a>Weitere Vorteile von intelligenten Extranetsperren in AD FS-2019
Extranet Smart Lockout in AD FS-2019 fügt die folgenden Vorteile im Vergleich zu AD FS 2016 hinzu:
- Legen Sie unabhängige Sperre Schwellenwerte für die bekannten und unbekannten Standorten, damit Benutzer in gut an bekannten Speicherorten von verdächtigen Standorten mehr Platz für Fehler als Anforderungen haben
- Aktivieren des Überwachungsmodus für smart Lockout und weiterhin die vorherige vorläufig Sperre Verhalten zu erzwingen

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2016"></a>Voraussetzungen für die intelligente Extranetsperre in AD FS 2016
Die folgenden Voraussetzungen müssen für zusammenfassender Meldung mit AD FS-2019.

### <a name="install-updates-on-all-nodes-in-the-farm"></a>Installieren von Updates auf allen Knoten in der farm
Stellen Sie zunächst sicher, alle Windows Server 2016 AD FS-Server auf dem neuesten Stand zum Zeitpunkt der Windows-Updates von Juni 2018 sind und dass die AD FS 2016-Farm an die verhaltensebene 2016-Farm ausgeführt wird.

### <a name="update-artifact-database-permissions"></a>Aktualisieren der Artefakt-Datenbankberechtigungen
Der smart Lockout Extranet erfordert der AD FS-Dienstkonto Berechtigungen für eine neue Tabelle in der AD FS-Artefakt-Datenbank verfügen.  Erteilen Sie diese Berechtigung, indem Sie den folgenden Befehl in einem PowerShell-Befehlsfenster ausführen:
``` powershell
PS C:\>$cred = Get-Credential
PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
```
Wo `$cred` ist ein Konto mit Administratorberechtigungen für die AD FS (AD FS-Administratorberechtigungen sind erforderlich, um die Datenbank zu ändern.)

>[!NOTE]
>In einer Farm mit mehreren Servern, die die WID-Datenbank verwendet, muss das oben aufgeführte Cmdlet auf jedem AD FS-Server Windows-Remoteverwaltung aktiviert sein

Wenn Sie nicht über AD FS-Administratorberechtigungen verfügen, können Sie Berechtigungen für die Datenbank manuell in SQL oder WID konfigurieren mithilfe des folgenden Befehls beim Verbinden mit der Datenbank AdfsArtifactStore.
```
sp_addrolemember 'db_owner', 'db_genevaservice'
```
### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>Stellen Sie sicher, dass AD FS-Sicherheit-Überwachungsprotokollierung aktiviert ist
Dieses Feature macht Sicherheitsüberwachung verwenden, die in AD FS als auch für die lokale Richtlinie für alle AD FS-Server anmeldet, also die Überwachung aktiviert werden müssen.

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2019"></a>Voraussetzungen für die intelligente Extranetsperre in AD FS 2019
Die folgenden Voraussetzungen sind für zusammenfassender Meldung in AD FS 2016 erforderlich.

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>Stellen Sie sicher, dass AD FS-Sicherheit-Überwachungsprotokollierung aktiviert ist
Dieses Feature macht Sicherheitsüberwachung verwenden, die in AD FS als auch für die lokale Richtlinie für alle AD FS-Server anmeldet, also die Überwachung aktiviert werden müssen.

## <a name="lockout-settings"></a>Einstellungen für die kontosperrung
Intelligente extranetsperre besteht aus einer Reihe neuer Funktionen, die durch AD FS-Eigenschaften für neue und vorhandene geregelt.

### <a name="extranet-lockout-enabled"></a>Extranetsperre aktiviert
Intelligente extranetsperre verwendet die gleiche AD FS-Eigenschaft, die zuvor verwendet wurde, um "soft" extranetsperre steuern.  Die Eigenschaft ExtranetLockoutEnabled aufgerufen wird und über Get-AdfsProperties angezeigt werden kann.

### <a name="extranet-smart-lockout-mode"></a>Der Smart Lockout Extranet-Modus
ExtranetLockoutMode Namens eine neue AD FS-Eigenschaft wurde hinzugefügt, um intelligente Vs "soft" Sperrung Verhalten zu steuern.  Es kann festgelegt werden, über die Set-AdfsProperties und 3 Werte enthält:

    - **ADPasswordCounter** – Dies ist der Vorgängerversion, die AD FS "soft extranetsperrung" Modus nicht unterscheidet, auf dem Standort basierend.  Dies ist der Standardwert.

    - **ADFSSmartLockoutLogOnly** – das Extranet Smart Lockout ist, aber ablehnen authentifizierungsanforderungen, AD FS nur Schreibzugriff Verwaltung und Überwachung Ereignisse.

    - **ADFSSmartLockoutEnforce** – Dies ist der Smart Lockout Extranet mit voller Unterstützung für unbekannte Anforderungen blockieren, wenn die Schwellenwerte erreicht sind.

In AD FS-2019 können die Werte ADPasswordCounter und ADFSSmartLockoutLogOnly kombiniert werden, damit diese vorläufigen Sperre erzwungen werden weiterhin, während Sie für die smart Lockout vorbereiten.

### <a name="lockout-threshold-and-observation-window"></a>Schwellenwert für computerkontosperrung und Beobachtung-Fenster
Der Smart Lockout in AD FS-2019 verwendet die gleichen zwei AD FS-Eigenschaften als weiche Sperre, die zuvor verwendet haben: ExtranetObservationWindow "und" ExtranetLockoutThreshold ".

- **ExtranetLockoutThreshold &lt;Ganzzahl&gt;**  definiert die maximale Anzahl der Versuche mit falschem Kennwort. Sobald der Schwellenwert erreicht wird, wird in ADFSSmartLockoutEnforce Modus AD FS Anforderungen aus dem extranet ablehnen, Fenster Beobachtung verstrichen ist.  Im Modus "ADFSSmartLockoutLogOnly" wird die AD FS nur Protokolleinträge geschrieben.  
- **ExtranetObservationWindow &lt;TimeSpan&gt;**  Dadurch wird bestimmt, für wie lange Benutzername und Kennwort die Anforderungen von unbekannten Standorten gesperrt werden. AD FS wird gestartet, Benutzername und Kennwort-Authentifizierung erneut durchgeführt, wenn das Fenster übergeben wird.

> [!NOTE]
> AD FS extranet Lockout Funktionen unabhängig von der AD-Kontosperrungsrichtlinien. Es wird empfohlen, Sie legen die **ExtranetLockoutThreshold** Parameterwert ein Wert, der kleiner ist als der Schwellenwert für AD-kontosperrung. Ist dies nicht der Fall würde dazu führen, dass AD FS nicht verhindern, dass Konten in Active Directory gesperrt wird. 

In AD FS-2019 haben wir eine neue bestimmte Sperrschwelle zu gut an bekannten Speicherorten eingeführt: ExtranetLockoutThresholdFamiliarLocation.
- **ExtranetLockoutThresholdFamiliarLocation &lt;Ganzzahl&gt;**  definiert die maximale Anzahl der Versuche mit falschem Kennwort aus der vertrauten Standorte. Unbekannte Standorte (IP-Adressen nicht gut bekannt) gilt der ursprüngliche Parameter ExtranetLockoutThreshold, in AD FS-2019.

### <a name="primary-domain-controller-requirement"></a>Primäre Domäne-Controller-Anforderung
AD FS 2016 bietet es sich um einen Parameter, der fallback auf einen anderen Domänencontroller ermöglicht, wenn der primäre Domänencontroller nicht verfügbar ist.

- **ExtranetLockoutRequirePDC &lt;booleschen&gt;**  Wenn aktiviert, erfordert extranetsperre primärer Domänencontroller (PDC). Wenn deaktiviert, extranetsperre erfolgt ein Fallback auf einen anderen Domänencontroller für den Fall, dass der PDC nicht verfügbar ist.

   Das folgende Beispiel zeigt das-Cmdlet zum Aktivieren der Sperre mit der PDC-Anforderung deaktiviert:

    ```powershell
    Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
    ```

## <a name="configuring-ad-fs-with-smart-lockout-in-log-only-mode"></a>Konfigurieren von AD FS mit der Smart Lockout im Protokollmodus

### <a name="ad-fs-2016"></a>AD FS 2016
Es wird empfohlen, dass Sie zuerst die Sperre Verhalten sich nur durch das folgende Cmdlet ausführen festlegen:

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly
 ```

In diesem Modus kann AD FS liefern Informationen für Benutzer bekannten Speicherort und schreibt Sicherheitsüberwachungsereignisse, aber keine Anforderungen blockiert.  Dieser Modus wird verwendet, um sicherzustellen, dass der smart Lockout ausgeführt wird, und zum Aktivieren von AD FS "vertrauten Standorte für Benutzer vor dem Aktivieren der erfahren," "erzwingen".
Wie AD FS lernt, speichert er Anmeldeaktivität pro Benutzer (angibt, ob im Protokollmodus oder im). 

>[!NOTE]
>Konfigurieren von `ExtranetLockoutMode` zu `AdfsSmartlockoutLogOnly` bewirkt, dass das AD FS "soft extranetsperrung" Legacyverhalten sollen nicht mehr aktiviert ist, auch wenn die `EnableExtranetLockout` Eigenschaft auf "true" festgelegt ist.  Dies bedeutet, dass Benutzer, die Sperre Schwellenwerte von vertraut sind oder unbekannten IP-Adressen überschreiten nicht per AD FS-Smart Lockout gesperrt werden. Allerdings das lokale AD Sperre der Benutzer auf Basis der Konfiguration gibt es möglicherweise.   Finden Sie unter [Kontosperrungsrichtlinien](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/account-lockout-policy) , erfahren, wie für lokale AD können Benutzer der Sperre. "  Dies richtet sich an einen temporären Zustand sein, damit das System Login-Verhalten vor neueinführung Sperre Erzwingung mit dem neuen Verhalten von der smart Lockout erfahren kann.

Starten Sie für den neuen Modus wirksam wird die AD FS-Dienst auf allen Knoten in der Farm neu
  
  ``` powershell
PS C:\>Restart-service adfssrv
  ```
Sobald der Modus konfiguriert ist, können Sie mit der smart Lockout das `EnableExtranetLockout` Parameter


``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $true
```

Beachten Sie, dass Sie das gleiche Cmdlet verwenden können, um Sperre deaktivieren

Beispiel: Sperre deaktivieren

``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $false
```
### <a name="ad-fs-2019"></a>AD FS 2019
Wenn Sie AD FS Extranet vorläufig Lockout derzeit nicht verwenden, empfehlen wir, dass Sie die gleiche Anweisungen wie bei AD FS 2016 oben folgen.
Wenn Sie vorläufig Sperre verwenden, allerdings sollten Sie festlegen, dass das AD FS-2019 Sperre Verhalten sich der smart Lockout, aber behalten soft-Sperre zu erzwingen, indem der folgende Powershell:

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode 3
 ```

Nachdem Sie dieses Cmdlet ausgeführt haben, können Sie Get-AdfsProperties dann verwenden, um den Wert der Eigenschaft ExtranetLockoutMode AD FS abzufragen.  Sie sehen, dass der Wert auf eine bitweise Kombination von ADPasswordCounter und ADFSSmartLockoutLogOnly aktualisiert wurde.

## <a name="observing-audit-events"></a>Beobachten von Überwachungsereignissen
AD FS werden extranet Lockout Ereignisse in das Sicherheitsprotokoll für die Überwachung geschrieben werden:
-   Wenn ein Benutzer gesperrt ist (der Schwellenwert für kontosperrung erreicht, für nicht erfolgreiche Anmeldeversuche) Out
-   Wenn AD FS ein Anmeldeversuch eines Benutzers erhält, die bereits im Zustand der Sperre ist

Klicken Sie im Protokollmodus, können Sie das Sicherheitsprotokoll für Sperrereignisse überprüfen.  Für alle Ereignisse, die gefunden wird können Sie überprüfen, den Benutzerzustand mit, dass das Cmdlet Get-ADFSAccountActivity zu bestimmen, ob die Sperre von vertraut sind oder unbekannten IP-Adressen, und überprüfen die Liste der vertrauten IP-Adressen für diesen Benutzer aufgetreten ist.

Beispielereignis:
```
Log Name:      Security
Source:        AD FS Auditing
Date:          5/21/2018 12:55:59 AM
Event ID:      1210
Task Category: (3)
Level:         Information
Keywords:      Classic,Audit Failure
User:          CONTOSO\adfssvc
Computer:      ADFS2016FS1.corp.contoso.com
Description:
An extranet lockout event has occurred. See XML for failure details. 

Activity ID: fa7a8052-0694-48f0-84e2-b51cde40ac3d 

Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>
Event Xml:
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="AD FS Auditing" />
    <EventID Qualifiers="0">1210</EventID>
    <Level>0</Level>
    <Task>3</Task>
    <Keywords>0x8090000000000000</Keywords>
    <TimeCreated SystemTime="2018-05-21T00:55:59.921880300Z" />
    <EventRecordID>35521235</EventRecordID>
    <Channel>Security</Channel>
    <Computer>ADFS2016FS1.contoso.com</Computer>
    <Security UserID="S-1-5-21-1156273042-1594504307-2076964089-1104" />
  </System>
  <EventData>
    <Data>fa7a8052-0694-48f0-84e2-b51cde40ac3d</Data>
    <Data><?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase></Data>
  </EventData>
</Event>
```

## <a name="observing-user-activity"></a>Überwachen der Benutzeraktivität
AD FS bietet Powershell-Cmdlets zum Anzeigen und Verwalten von Benutzerkontodaten-Aktivität.  Um die aktuellen Konto-Aktivität für ein Benutzerkonto zu lesen.  Verwenden Sie das unten angegebene cmdlet

``` powershell
PS C:\>Get-ADFSAccountActivity user@contoso.com
```

Beispielausgabe
```
Identifier             : CONTOSO\user
BadPwdCountFamiliar    : 0
BadPwdCountUnknown     : 0
LastFailedAuthFamiliar : 1/1/0001 12:00:00 AM
LastFailedAuthUnknown  : 1/1/0001 12:00:00 AM
FamiliarLockout        : False
UnknownLockout         : False
FamiliarIps            : {}
```

Die aktuelle aktivitätsausgabe enthält die folgenden Daten:

**Bezeichner**: Dies ist der Benutzername

**BadPwdCountFamiliar**: Dies ist die aktuelle Anzahl der falschen Kennwort Anmeldeversuche über IP-Adressen, die in der Liste der "FamiliarIps" zum Zeitpunkt des Versuchs

**BadPwdCountUnknown**: Dies ist die aktuelle Anzahl der falschen Kennwort Anmeldeversuche über IP-Adressen, die nicht in der Liste der "FamiliarIps" zum Zeitpunkt des Versuchs waren

**LastFailedAuthFamiliar**: Dies ist der Zeitpunkt der letzten falsches Kennwort Anmeldeversuch von einer IP-Adresse, die in der Liste der "FamiliarIps" zum Zeitpunkt des Versuchs

**LastFailedAuthUnknown**: Dies ist der Zeitpunkt der letzten Anmeldung falsches Kennwort von einer IP-Adresse, die nicht in der Liste der "FamiliarIps" zum Zeitpunkt des Versuchs des

**FamiliarLockout**: Dies gibt an, ob der Benutzer derzeit in einem Zustand der Sperre für die richtige Kennwortversuche von IP-Adressen in der Liste der "FamiliarIps" 

**UnknownLockout**: Dies gibt an, ob der Benutzer derzeit in einem Zustand der Sperre für das richtige Kennwort von IP-Adressen nicht in der Liste der "FamiliarIps" FamiliarIps versucht: Dies ist die aktuelle Liste der vertrauten IP-Adressen für den Benutzer

## <a name="adjust-threshold-and-window"></a>Passen Sie Schwellenwert und Fenster
Nachdem Sie im Protokollmodus für eine ausreichende Zeitspanne für AD FS für die Anmeldung Informationen ausgeführt haben, möchten Sie möglicherweise anpassen, das Fenster Schwellenwert oder Beobachtung von den Standardeinstellungen abweichen.  Dies erfolgt mit `Set-AdfsProperties` wie in den folgenden Beispielen:

Die Beobachtung Fenster festgelegt, wobei `ExtranetObservationWindow`:

Beispiel: 

``` powershell
PS C:\>Set-AdfsProperties -ExtranetObservationWindow ( new-timespan -minutes 30 )
```

Der Wert ist ein TimeSpan-Objekt

### <a name="setting-threshold-value-in-ad-fs-2016"></a>Festlegen des Schwellenwerts für in AD FS 2016
In AD FS 2016 wird der Schwellenwert mit ExtranetLockoutThreshold festgelegt:

Beispiel:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

### <a name="setting-threshold-values-in-ad-fs-2019"></a>Festlegen von Schwellenwerten in AD FS-2019
In AD FS-2019 stehen unterschiedliche Schwellenwerte für bekannte gute und unbekannten Speicherorte

Um den Schwellenwert für unbekannte Standorte zu festzulegen, verwenden Sie die gleiche Eigenschaft, die für die AD FS 2016 oben verwendet:

Beispiel:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

Verwenden Sie die neue Eigenschaft ExtranetLockoutThresholdFamiliarLocation, um den Schwellenwert für gute an bekannten Speicherorten festzulegen, wie im folgenden Beispiel gezeigt:

Beispiel:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThresholdFamiliarLocation 10
```


## <a name="enable-enforce-mode"></a>Enable erzwingen
Sobald Sie haben genügend Zeit für AD FS-Anmeldung erfahren, und beobachten Sie alle Aktivitäten der Sperre im Protokollmodus ausgeführt wurde, und sobald Sie mit der Sperre Schwellenwert und die Beobachtung Fenster vertraut sind, kann der smart Lockout "im Modus mit erzwingen" verschoben werden die PSH-Cmdlet aus:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce
```

Starten Sie für den neuen Modus wirksam wird die AD FS-Dienst auf allen Knoten in der Farm neu

``` powershell
PS C:\>Restart-service adfssrv
```


## <a name="manage-user-account-activity"></a>Verwalten von Aktivitäten der Benutzer-Konto
AD FS bietet 3 Cmdlets zum Verwalten von Benutzerkontodaten-Aktivität.  Diese Cmdlets automatisch verbinden, auf den Knoten in der Farm, die die Rolle enthält (Obwohl dieses Verhalten kann, übergeben überschrieben werden den - Server-Parameter).

> [!NOTE] 
> Weitere Informationen über das Delegieren von Berechtigungen für die Verwendung dieser Cmdlets finden Sie unter [delegieren AD FS Powershell-Cmdlet des Zugriffs auf Benutzer ohne Administratorrechte](delegate-ad-fs-pshell-access.md)

Diese Cmdlets sind:

`Get-ADFSAccountActivity`

Lesen Sie die aktuellen Konto-Aktivität für ein Benutzerkonto an.  Das Cmdlet verbindet sich immer automatisch mit dem Farm-Master mit der Konto-Aktivität-REST-Endpunkt, damit alle Daten stets konsistent sein sollen

``` powershell
Get-ADFSAccountActivity user@contoso.com
```
`
Set-ADFSAccountActivity
`

Aktualisieren Sie die Kontoaktivität für ein Benutzerkonto an.  Dies dient zum Hinzufügen von neuen vertrauten Standorte oder Status für alle Konten gelöscht werden

``` powershell
Set-ADFSAccountActivity user@upnsuffix.com -FamiliarLocation “1.2.3.4”
```
`Reset-ADFSAccountLockout`

Setzt den Zähler für kontosperrung für ein Benutzerkonto

``` powershell
Reset-ADFSAccountLockout user@upnsuffix.com -Familiar
```

## <a name="troubleshooting-esl"></a>Problembehandlung bei zusammenfassender Meldung
Die folgenden unterstützen Sie bei der Problembehandlung der extranet der smart Lockout-Funktion.

### <a name="updating-database-permissions-for-esl"></a>Aktualisieren von Berechtigungen für die Datenbank für zusammenfassender Meldung
Wenn keine Fehler zurückgegeben werden, aus der `Update-AdfsArtifactDatabasePermission` -Cmdlet, überprüfen Sie die folgenden

1.  Die Liste der farmknoten ist richtig.  Patch-Überprüfung schlägt fehl, wenn ein Knoten in der Liste des AD FS-Farm jedoch nicht mehr aktiv ist.  Dies kann durch Ausführen von behoben werden `remove-adfsnode <node name >`
2.  Stellen Sie sicher, dass der Patch auf allen Knoten in der Farm bereitgestellt wird
3.  Vergewissern Sie sich die Anmeldeinformationen, die an das Cmdlet übergeben, die eine Berechtigung zum Ändern des Besitzers des Ad fs-Artefakt-Datenbankschemas.  

### <a name="logging--auditing"></a>Protokollierung / Überwachung
AD FS wird geschrieben, wenn eine Authentifizierungsanforderung abgelehnt wird, weil das Konto den Sperrschwellenwert überschreitet, eine `ExtranetLockoutEvent` in den Security Audit-Stream.  

Beispielereignis:

Ein extranetsperre-Ereignis ist aufgetreten. Fehlerdetails finden Sie in der XML. 

**Aktivitäts-ID: 172332e1-1301-4e56-0e00-0080000000db**

```
Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>TQDFTD\Administrator</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Intranet</NetworkLocation>
      <IpAddress>4.4.4.4</IpAddress>
      <ForwardedIpAddress />
      <ProxyIpAddress>1.2.3.4</ProxyIpAddress>
      <NetworkIpAddress>1.2.3.4</NetworkIpAddress>
      <ProxyServer>N/A</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>02/07/2018 21:47:44</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>

```

## <a name="banned-ip-addresses"></a>Gesperrte IP-Adressen
Zusätzlich zu den Funktionen der smart Lockout extranet des AD FS-Juni 2018-Updates können Sie eine Gruppe von IP-Adressen Global in AD FS konfigurieren, damit Anforderungen von diesen IP-Adressen, oder dass die IP-Adressen haben, in der **X-forwarded-for**  oder **X-ms-forwarded-Client-IP-** -Header von AD FS blockiert werden.

##### <a name="adding-banned-ips"></a>Hinzufügen von IP-Adressen gesperrt
Um gesperrte IP-Adressen auf die globale Liste hinzuzufügen, verwenden die folgenden Powershell-Cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

Zulässige Formate

1.  IPv4
2.  IPv6
3.  CIDR-Format mit IPv4- oder IPv6
4.  IP-Adressbereich mit IPv4- oder IPv6 (d. h. 1.2.3.4-1.2.3.6)

#### <a name="removing-banned-ips"></a>Entfernen von IP-Adressen gesperrt
Um gesperrte IP-Adressen aus der globalen Liste zu entfernen, verwenden Sie die folgenden Powershell-Cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>Lesen gesperrt, IP-Adressen
Um den aktuellen Satz von gesperrten IP-Adressen zu lesen, verwenden Sie die folgenden Powershell-Cmdlet:

``` powershell
PS C:\ >Get-AdfsProperties 
```

Beispielausgabe:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>Weitere Verweise  
[Bewährte Methoden zum Schützen von Active Directory Federation Services](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)

    
