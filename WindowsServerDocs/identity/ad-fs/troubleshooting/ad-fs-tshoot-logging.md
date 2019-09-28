---
title: 'AD FS Problembehandlung: Überwachungs Ereignisse und Protokollierung'
description: In diesem Dokument wird beschrieben, wie Sie die verschiedenen AD FS Protokolle verwenden, um Probleme zu beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5985fc022a084e0e36e12ea60f18d1650c8c6b51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366199"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS Problembehandlung: Ereignisse und Protokollierung
In AD FS werden zwei primäre Protokolle bereitgestellt, die bei der Problembehandlung verwendet werden können.  Die Überladungen sind:

- das Administrator Protokoll
- Das Ablauf Verfolgungs Protokoll  
 
Diese Protokolle werden im folgenden erläutert.

## <a name="admin-log"></a>Administrator Protokoll
Das Administrator Protokoll bietet allgemeine Informationen zu auftretenden Problemen und ist standardmäßig aktiviert.

### <a name="to-view-the-admin-log"></a>So zeigen Sie das Administrator Protokoll an
1.  Öffnen Sie die Ereignisanzeige
2.  Erweitern Sie **Anwendungs-und Dienst Protokoll**.
3.  Erweitern Sie **AD FS**.
4.  Klicken Sie auf **Admin**.

![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>Ablauf Verfolgungs Protokoll
Im Ablauf Verfolgungs Protokoll werden ausführliche Meldungen protokolliert, die bei der Problembehandlung am nützlichsten protokolliert werden. Da viele Ablauf Verfolgungs Protokoll-Informationen in kurzer Zeit generiert werden können, was sich auf die Systemleistung auswirken kann, sind die Ablauf Verfolgungs Protokolle standardmäßig deaktiviert. 

### <a name="to-enable-and-view-the-trace-log"></a>So aktivieren und anzeigen Sie das Ablauf Verfolgungs Protokoll
1.  Öffnen Sie die Ereignisanzeige
2.  Klicken Sie mit der rechten Maustaste auf **Anwendungs-und Dienst Protokoll** , und wählen Sie anzeigen aus, und klicken Sie auf **analytische und Debugprotokolle**  Dadurch werden zusätzliche Knoten auf der linken Seite angezeigt.
![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/event2.PNG)  
3.  AD FS Ablauf Verfolgung erweitern
4.  Klicken Sie mit der rechten Maustaste auf Debug, und wählen Sie **Protokoll aktivieren**.
![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Informationen zur Ereignisüberwachung für AD FS unter Windows Server 2016  
Standardmäßig ist für AD FS in Windows Server 2016 ein grundlegendes Maß an Überwachung aktiviert.  Bei der grundlegenden Überwachung sehen Administratoren maximal 5 oder weniger Ereignisse für eine einzelne Anforderung.  Dies kennzeichnet einen signifikanten Rückgang der Anzahl von Ereignissen, die Administratoren untersuchen müssen, um eine einzelne Anforderung anzuzeigen.   Die Überwachungs Ebene kann mithilfe des PowerShell-cmdlt ausgelöst oder verringert werden:  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

In der folgenden Tabelle werden die verfügbaren Überwachungs Stufen erläutert.  

|Überwachungsebene|PowerShell-Syntax|Beschreibung|  
|----- | ----- | ----- |
|Keine|Set-ADF sproperties-AuditLevel None|Die Überwachung ist deaktiviert, und es werden keine Ereignisse protokolliert.|  
|Basic (Standard)|Set-ADF sproperties-AuditLevel Basic|Für eine einzelne Anforderung werden höchstens 5 Ereignisse protokolliert.|  
|Ausführlich|Set-ADF sproperties-AuditLevel Verbose|Alle Ereignisse werden protokolliert.  Dadurch wird eine beträchtliche Menge an Informationen pro Anforderung protokolliert.|  
  
Zum Anzeigen der aktuellen Überwachungs Ebene können Sie das PowerShell-Cmdlet verwenden:  Get-ADF sproperties.  
  
![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
Die Überwachungs Ebene kann mithilfe des PowerShell-cmdlt ausgelöst oder verringert werden:  Set-ADF sproperties-AuditLevel.  
  
![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>Ereignis Typen  
AD FS Ereignisse können unterschiedliche Typen aufweisen, basierend auf den verschiedenen Typen von Anforderungen, die von AD FS verarbeitet werden. Jedem Ereignistyp sind bestimmte Daten zugeordnet.  Der Ereignistyp kann zwischen Anmelde Anforderungen (d. h. Tokenanforderungen) und Systemanforderungen (Server-Server-Aufrufe einschließlich Abrufen von Konfigurationsinformationen) unterscheiden.    

In der folgenden Tabelle werden die grundlegenden Ereignis Typen beschrieben.  
  
|Ereignistyp|Ereignis-ID|Beschreibung| 
|----- | ----- | ----- | 
|Erfolgreiche Überprüfung der Anmelde Informationen erfolgreich|1202|Eine Anforderung, bei der neue Anmelde Informationen erfolgreich vom Verbunddienst überprüft werden. Dies umfasst WS-Trust, WS-Federation, SAML-P (erster Teil zum Generieren von SSO) und OAuth-Autorisierungs Endpunkte.|  
|Fehler bei der Validierung der neuen Anmelde Informationen|1203|Eine Anforderung, bei der die Überprüfung der neuen Anmelde Informationen für den Verbunddienst fehlgeschlagen ist Hierzu gehören WS-Trust, WS-Fed, SAML-P (erster Teil zum Generieren von SSO) und OAuth-Autorisierungs Endpunkte.|  
|Anwendungs Token erfolgreich|1200|Eine Anforderung, bei der ein Sicherheits Token erfolgreich vom Verbunddienst ausgestellt wird. Für WS-Federation wird SAML-P protokolliert, wenn die Anforderung mit dem SSO-Element verarbeitet wird. (z. b. das SSO-Cookie).|  
|Anwendungs Token-Fehler|1201|Eine Anforderung, bei der die sicherheitstokenausstellung im Verbunddienst fehlgeschlagen ist Für WS-Federation wird SAML-P bei der Verarbeitung der Anforderung mit dem SSO-Element protokolliert. (z. b. das SSO-Cookie).|  
|Anforderung zum Ändern von Kenn Wörtern erfolgreich|1204|Eine Transaktion, bei der das Kennwort Change Request erfolgreich vom Verbunddienst verarbeitet wurde.|  
|Fehler beim Ändern der Kenn Wort Änderung|1205|Eine Transaktion, bei der das Kennwort Change Request nicht vom Verbunddienst verarbeitet werden konnte.| 
|Erfolg abmelden|1206|Beschreibt eine erfolgreiche Abmelde Anforderung.|  
|Abmelde Fehler|1207|Beschreibt eine fehlgeschlagene Abmelde Anforderung.|  

## <a name="security-auditing"></a>Sicherheitsüberwachung
Die Sicherheitsüberwachung des AD FS-Dienst Kontos kann manchmal hilfreich sein, um Probleme mit Kenn Wort Aktualisierungen, Anforderungs-/antwortprotokollierung, Anforderungs Kandidaten und Geräte Registrierungs Ergebnissen zu beheben.  Die Überwachung des AD FS-Dienst Kontos ist standardmäßig deaktiviert.

### <a name="to-enable-security-auditing"></a>So aktivieren Sie die Sicherheitsüberwachung
1. Klicken Sie auf Start, zeigen Sie auf **Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **lokale Sicherheitsrichtlinie**.
2. Navigieren Sie zum Ordner **Sicherheitseinstellungen\Lokale Richtlinien\User Rights Management** und doppelklicken dann auf **Generieren von Sicherheitsüberwachungen**.
3. Überprüfen Sie auf der Registerkarte **lokale Sicherheitseinstellung** , ob das AD FS-Dienst Konto aufgeführt ist. Wenn Sie nicht vorhanden ist, klicken Sie auf Benutzer oder Gruppe hinzufügen, fügen Sie Sie der Liste hinzu, und klicken Sie dann auf OK.
4. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus, um die Überwachung Auditpol. exe/Set/SubCategory: "Application generated"/Failure: enable/Success: enable zu aktivieren.
5. Schließen Sie **lokale Sicherheitsrichtlinie**, und öffnen Sie dann das Snap-in "AD FS-Verwaltung".
 
Klicken Sie zum Öffnen des Snap-Ins "AD FS-Verwaltung" auf Start, zeigen Sie auf Programme, zeigen Sie auf Verwaltung, und klicken Sie dann auf AD FS Verwaltung.
 
6. Klicken Sie im Aktionsbereich auf Verbunddienst Eigenschaften bearbeiten.
7. Klicken Sie im Dialogfeld Verbunddienst Eigenschaften auf die Registerkarte Ereignisse.
8. Aktivieren Sie die Kontrollkästchen **Erfolgs** Überwachungen und **Fehler** Überwachungen.
9. Klicken Sie auf „OK“.

![Überwachungs Erweiterungen](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>Die obigen Anweisungen werden nur verwendet, wenn AD FS auf einem eigenständigen Mitglieds Server ist.  Wenn AD FS auf einem Domänen Controller ausgeführt wird, anstelle der lokalen Sicherheitsrichtlinie, verwenden Sie die **Standard Domänen Controller Richtlinie** in **Gruppenrichtlinie Verwaltung/Gesamtstruktur/Domänen/** Domänen Controller.  Klicken Sie auf Bearbeiten, und navigieren Sie zu Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richt **Linien \ Benutzer Rights Management**

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation-und Windows Identity Foundation-Meldungen
Zusätzlich zur Ablauf Verfolgungs Protokollierung müssen Sie möglicherweise Windows Communication Foundation (WCF) und Windows Identity Foundation (WIF)-Nachrichten anzeigen, um ein Problem zu beheben. Dies kann durch Ändern der Datei " **Microsoft. identityserver. ServiceHost. exe. config** " auf dem AD FS-Server erreicht werden. 

Diese Datei befindet sich in **<% System root% > \windows\adfs** und ist im XML-Format. Die relevanten Teile der Datei sind unten dargestellt: 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


Nachdem Sie diese Änderungen vorgenommen haben, speichern Sie die Konfiguration, und starten Sie den AD FS-Dienst erneut. Nachdem Sie diese Ablauf Verfolgungen durch Festlegen der entsprechenden Switches aktiviert haben, werden Sie im AD FS Ablauf Verfolgungs Protokoll in der Windows-Ereignisanzeige angezeigt.

## <a name="correlating-events"></a>Korrelieren von Ereignissen
Eine der schwierigsten Probleme bei der Problembehandlung sind Zugriffs Probleme, die viele Fehler-oder Debugereignisse generieren.

Um dies zu unterstützen, AD FS korreliert alle Ereignisse, die in der Ereignisanzeige aufgezeichnet werden, sowohl in den Admin-als auch in den Debug-Protokollen, die einer bestimmten Anforderung entsprechen, mithilfe einer eindeutigen GUID (Global Unique Identifier), die als Aktivitäts-ID bezeichnet wird. Diese ID wird generiert, wenn die tokenausstellungsanforderung anfänglich der Webanwendung (für Anwendungen, die das passive Anforderer-Profil verwenden) oder Anforderungen, die direkt an den Anspruchs Anbieter gesendet werden (bei Anwendungen mit WS-Trust), angezeigt wird. 

![ActivityId](media/ad-fs-tshoot-logging/activityid1.png)

Diese Aktivitäts-ID bleibt für die gesamte Dauer der Anforderung gleich und wird als Teil jedes Ereignisses protokolliert, das im Ereignisanzeige für diese Anforderung aufgezeichnet wurde. Dies bedeutet Folgendes:
 - Wenn Sie die Ereignisanzeige mit dieser Aktivitäts-ID filtern oder durchsuchen, können Sie alle verwandten Ereignisse nachverfolgen, die der Tokenanforderung entsprechen.
 - dieselbe Aktivitäts-ID wird auf verschiedenen Computern protokolliert, sodass Sie die Problembehandlung für eine Benutzer Anforderung auf mehreren Computern, wie z. b. dem Verbund Server Proxy (FSP), ermöglichen.
 - die Aktivitäts-ID wird auch im Browser des Benutzers angezeigt, wenn die AD FS Anforderung in irgendeiner Weise fehlschlägt, sodass der Benutzer diese ID dem Helpdesk oder dem IT-Support mitteilen kann.

![ActivityId](media/ad-fs-tshoot-logging/activityid2.png)

Zur Unterstützung des Problem Behandlungsprozesses protokolliert AD FS auch immer dann das Aufrufer-ID-Ereignis, wenn der tokenausstellungs-Prozess auf einem AD FS Server fehlschlägt. Dieses Ereignis enthält den Anspruchstyp und den Wert eines der folgenden Anspruchs Typen, wobei angenommen wird, dass diese Informationen als Teil einer Tokenanforderung an die Verbunddienst übermittelt wurden:
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

Das Ereignis Aufruferkennung protokolliert auch die Aktivitäts-ID, damit Sie die Ereignisprotokolle mithilfe dieser Aktivitäts-ID filtern oder nach einer bestimmten Anforderung durchsuchen können.




## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
