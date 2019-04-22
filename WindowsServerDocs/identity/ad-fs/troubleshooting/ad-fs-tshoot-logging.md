---
title: AD FS-Problembehandlung – Überwachung der Ereignisse und Protokollierung
description: Dieses Dokument beschreibt, wie die verschiedenen Protokolle der AD FS verwenden, um Probleme zu beheben
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 20e2d0747b98e7c7728230d0768506261f5b0d50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825121"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS-Problembehandlung – Ereignisse und Protokollierung
AD FS bietet zwei primäre Protokolle, die bei der Problembehandlung verwendet werden können.  Die Überladungen sind:

- das Admin-Protokoll
- das Ablaufverfolgungsprotokoll  
 
Jedes dieser Protokolle werden unten erläutert.

## <a name="admin-log"></a>Administratoranmeldung
Das Admin-Protokoll bietet detaillierte Informationen zu Problemen, die auftreten, und ist standardmäßig aktiviert.

### <a name="to-view-the-admin-log"></a>Das Administratorprotokoll anzeigen
1.  Öffnen Sie die Ereignisanzeige
2.  Erweitern Sie **Anwendungen und Services Log**.
3.  Erweitern Sie **AD FS**.
4.  Klicken Sie auf **Admin**.

![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>Die Ablaufverfolgung
Das Ablaufverfolgungsprotokoll ist, in dem ausführliche Meldungen werden protokolliert und werden das am nützlichsten Protokoll aus, bei der Problembehandlung. Da viele Ablaufverfolgungsinformationen in kurzer Zeit generiert werden kann, auf die Systemleistung auswirken können, sind die Ablaufverfolgungsprotokolle standardmäßig deaktiviert. 

### <a name="to-enable-and-view-the-trace-log"></a>Zum Aktivieren und das Ablaufverfolgungsprotokoll anzeigen
1.  Öffnen Sie die Ereignisanzeige
2.  Mit der rechten Maustaste auf **Anwendungen und Services Log** Ansicht auswählen, und klicken Sie auf **analytische und Debugprotokolle**.  Dadurch werden weitere Knoten auf der linken Seite angezeigt.
![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/event2.PNG)  
3.  Erweitern Sie die AD FS-Ablaufverfolgung
4.  Mit der rechten Maustaste auf Debuggen, und wählen **Protokoll aktivieren**.
![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Ereignis Überwachungsinformationen für AD FS unter Windows Server 2016  
Standardmäßig verfügt die AD FS unter Windows Server 2016 einen grundlegenden Servicelevel-Überwachung aktiviert.  Bei der grundlegenden Überwachung werden Administratoren 5 oder weniger Ereignisse für eine einzelne Anforderung finden Sie unter.  Kennzeichnet eine deutliche Verringerung der Anzahl der Ereignisse, die Administratoren haben, betrachten, um eine einzelne Anforderung finden Sie unter.   Die Überwachungsebene kann ausgelöst werden, oder gesenkt werden, mithilfe der PowerShell-Cmdlet:  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

In der folgenden Tabelle erläutert die verfügbaren Überwachungsebenen dienen.  

|Überwachungsebene|PowerShell-syntax|Beschreibung|  
|----- | ----- | ----- |
|Keine|Set-AdfsProperties - AuditLevel keine|Die Überwachung ist deaktiviert, und keine Ereignisse protokolliert werden.|  
|Basic (Standard)|Set-AdfsProperties - AuditLevel Basic|Nicht mehr als 5 Ereignisse werden für eine einzelne Anforderung protokolliert|  
|Ausführlich|Set-AdfsProperties - AuditLevel-Verbose|Alle Ereignisse werden protokolliert.  Dadurch wird eine beträchtliche Menge an Daten pro Anforderung protokolliert.|  
  
Zum Anzeigen der aktuellen Ebene für die Überwachung können Sie die PowerShell-Cmdlet verwenden:  Get-AdfsProperties.  
  
![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
Die Überwachungsebene kann ausgelöst werden, oder gesenkt werden, mithilfe der PowerShell-Cmdlet:  Set-AdfsProperties -AuditLevel.  
  
![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>Typen von Ereignissen  
AD FS-Ereignisse können verschiedener Typen, die basierend auf die verschiedenen Typen von Anforderungen, die von AD FS verarbeitet werden. Jeder Ereignistyp hat bestimmte ihm zugeordnete Daten.  Der Typ von Ereignissen kann zwischen anmeldeanforderungen (d. h. tokenanforderungen) im Vergleich zu den Anforderungen des Systems (einschließlich Konfigurationsinformationen abrufen Servern-Aufrufe) unterschieden werden.    

Die folgende Tabelle beschreibt die grundlegenden Typen von Ereignissen.  
  
|Ereignistyp|Ereignis-ID|Beschreibung| 
|----- | ----- | ----- | 
|Neue Anmeldeinformationen Validierung erfolgreich|1202|Eine Anforderung, in dem neue Anmeldeinformationen erfolgreich vom Verbunddienst überprüft werden. Dies schließt die WS-Trust, WS-Federation, SAML-P (ersten Abschnitt zum Generieren von SSO) und Autorisieren von OAuth-Endpunkte.|  
|Überprüfungsfehler für die neuen Anmeldeinformationen|1203|Eine Anforderung, in dem neue Anmeldeinformationen für den Verbunddienst Fehler bei der Überprüfung. Dies schließt die WS-Trust, WS-Fed-, SAML-P (ersten Abschnitt zum Generieren von SSO) und Autorisieren von OAuth-Endpunkte.|  
|Anwendung Token erfolgreich|1200|Eine Anforderung, in denen ein Sicherheitstoken vom Verbunddienst erfolgreich ausgegeben wird. Für WS-Verbund, SAML-P-dies protokolliert, wenn es sich bei der Verarbeitung der Anforderung mit der SSO-Element. (z. B. das SSO-Cookie).|  
|Fehler bei der Anwendung Token|1201|Eine Anforderung, an der tokenausstellung Sicherheit für den Verbunddienst fehlgeschlagen ist. Für WS-Verbund, SAML-P-dies protokolliert, wenn die Anforderung, mit der SSO-Element verarbeitet wurde. (z. B. das SSO-Cookie).|  
|Anforderung wurde erfolgreich von Kennwort geändert|1204|Eine Transaktion, in denen Anforderung der kennwortänderung, wurde erfolgreich vom Verbunddienst verarbeitet.|  
|Kennwort ändern-Anforderungsfehler|1205|Eine Transaktion, in denen Anforderung der kennwortänderung, nicht durch den Verbunddienst verarbeitet werden konnten.| 
|Melden Sie sich erfolgreich|1206|Beschreibt eine erfolgreiche Anforderung zur Abmelde.|  
|Fehler beim Abmelden|1207|Beschreibt eine Anforderung zur Abmelde und Fehler an.|  

## <a name="security-auditing"></a>Sicherheitsüberwachung
Von der AD FS-Dienstkonto die sicherheitsüberwachung kann manchmal bei der Probleme bei der Aktualisierung von Kennwörtern "," Anforderung/Antwort-Protokollierung "," context-Header für Anforderung "und" Gerät Registrierung Ergebnisse aufspüren.  Überwachung der AD FS-Dienstkonto ist standardmäßig deaktiviert.

### <a name="to-enable-security-auditing"></a>Zum Aktivieren der sicherheitsüberwachung
1.       Klicken Sie auf Start, zeigen Sie auf **Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Local Security Policy**.
2.       Navigieren Sie zum Ordner **Sicherheitseinstellungen\Lokale Richtlinien\User Rights Management** und doppelklicken dann auf **Generieren von Sicherheitsüberwachungen**.
3.       Auf der **lokale Sicherheitseinstellung** Registerkarte, stellen Sie sicher, dass das AD FS-Dienstkonto aufgeführt wird. Wenn es nicht vorhanden ist, klicken Sie auf Benutzer oder Gruppe hinzufügen zur Liste fügen Sie hinzu und klicken Sie dann auf OK.
4.       Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie den folgenden Befehl zum Aktivieren der Überwachung auditpol.exe/set/SubCategory: "Anwendung wurde generiert" Success /success:enable 5.       Schließen **Local Security Policy**, und öffnen Sie dann das AD FS-Verwaltungs-Snap-in.
 
Um das AD FS-Verwaltungs-Snap-in zu öffnen, klicken Sie auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS-Verwaltung.
 
6.       Klicken Sie im Bereich Aktionen auf Bearbeiten Federation Service Eigenschaften 7.       Klicken Sie in das Dialogfeld "Verbunddiensteigenschaften" auf der Registerkarte "Ereignisse". 8.       Wählen Sie die **erfolgsüberwachungen** und **Fehlerüberwachungen** Kontrollkästchen.
9.       Klicken Sie auf „OK“.

![die Verbesserte Überwachung](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>Nur, wenn AD FS auf einem eigenständigen Mitgliedsserver ist, werden die obigen Anweisungen verwendet.  Wenn AD FS, auf einem Domänencontroller, anstatt der lokalen Sicherheitsrichtlinie ausgeführt wird, verwenden Sie die **Standarddomänencontroller-Richtlinie** befindet sich in **Group Policy Management/Gesamtstruktur/Domänen/Domain Controller**.  Klicken Sie auf Bearbeiten, und navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation und Windows Identity Foundation-Nachrichten
Zusätzlich zur standardprotokollierung der Ablaufverfolgung manchmal müssen Sie möglicherweise an der Windows Communication Foundation (WCF) und Windows Identity Foundation (WIF) Nachrichten aus, um ein Problem zu beheben. Dies ist möglich durch Ändern der **Microsoft.IdentityServer.ServiceHost.Exe.Config** -Datei auf dem AD FS-Server. 

Diese Datei befindet sich im **< System Stamm % > \Windows\ADFS** und im XML-Format. Die relevanten Abschnitte der Datei werden unten angezeigt: 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


Nachdem Sie diese Änderungen vorgenommen haben, speichern Sie die Konfiguration, und starten Sie den AD FS-Dienst neu. Nachdem Sie diese ablaufverfolgungen durch Festlegen der entsprechenden Switches aktivieren, werden sie in das AD FS-Ablaufverfolgungsprotokoll in der Windows-Ereignisanzeige angezeigt.

## <a name="correlating-events"></a>Korrelieren von Ereignissen
Eine der schwierigsten Aufgaben zur Problembehandlung ist Probleme, die einen Großteil der Fehler generiert und debug-Ereignisse.

Um dies zu vereinfachen, korreliert AD FS für alle Ereignisse, die aufgezeichnet werden, in der Ereignisanzeige, in der Administrator und die Debugprotokolle, die auf eine bestimmte Anforderung zu entsprechen, mit der eine eindeutige Bezeichner (GLOBALLY Unique) wird aufgerufen, der die Aktivität-ID Diese ID wird generiert, wenn die Anforderung der tokenausstellung zunächst auf die Webanwendung (für Anwendungen, die über das passive Requestor-Profil) oder die Anforderungen direkt an die Anspruchsanbieter-Vertrauensstellung gesendet wurden (für Anwendungen, die mit WS-Trust) dargestellt wird. 

![activityid](media/ad-fs-tshoot-logging/activityid1.png)

Diese Aktivitäts-ID bleibt unverändert für die gesamte Dauer der Anforderung, und es wird protokolliert, Teil jedes Ereignisses im Event Viewer für diese Anforderung aufgezeichnet wurden. Dies bedeutet Folgendes:
 - Filtern oder durchsuchen die Ereignisanzeige, die mit dieser Aktivität ID kann alle verwandten Ereignisse mitverfolgen, die die Anforderung des Tokens entsprechen
 - dieselbe Aktivitäts-ID wird auf unterschiedlichen Computern Dadurch haben Sie die Problembehandlung bei einer benutzeranforderung auf mehreren Computern wie z. B. den Federation Server Proxy (FSP) protokolliert.
 - die Aktivitäts-ID wird auch in den Browser des Benutzers angezeigt, wenn den AD FS-Anforderungsfehler in keiner Weise, sodass des Benutzers, diese ID dem Helpdesk oder IT-Support zu kommunizieren.

![activityid](media/ad-fs-tshoot-logging/activityid2.png)

Zur Unterstützung bei der Problembehandlung protokolliert AD FS auch die Aufrufer-ID-Ereignis, wenn der tokenausstellung auf AD FS-Server kann nicht ausgeführt. Dieses Ereignis enthält den Anspruchstyp und den Wert eines der folgenden Anspruchstypen, vorausgesetzt, dass diese Informationen als Teil einer tokenanforderung an den Verbunddienst übergeben wurde:
- http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountnameh
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upnh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/upn
- http://schemas.xmlsoap.org/claims/UPN
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddressh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/emailaddress 
- http://schemas.xmlsoap.org/claims/EmailAddress
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
- http://schemas.microsoft.com/ws/2008/06/identity/claims/name
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier 

Der Aufrufer-ID-Ereignis protokolliert auch die Aktivitäts-ID können Sie diese Aktivitäts-ID zum Filtern oder durchsuchen die Ereignisprotokolle für eine bestimmte Anforderung verwenden.




## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)
