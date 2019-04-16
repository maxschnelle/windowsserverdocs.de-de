---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: "Überwachung von Verbesserungen bei der AD FS unter WindowsServer 2016"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3d622686a3cc34316f0cf5187839785195c2f104
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Überwachung von Verbesserungen bei der AD FS unter WindowsServer 2016

>Gilt für: Windows Server 2016

Derzeit in AD FS für Windows Server 2012 R2 gibt es zahlreiche für eine einzelne Anforderung und die relevanten Informationen zu einer Anmeldung generierten Überwachungsereignisse sind oder tokenausstellungs Aktivität ist entweder nicht vorhanden (in einigen Versionen von AD FS) oder über mehrere Überwachungsereignisse. Der AD FS werden Überwachungsereignisse aufgrund ihrer ausführliche Art standardmäßig deaktiviert.  
    Mit der Veröffentlichung von AD FS in Windows Server 2016 Überwachung optimierte und weniger ausführlich geworden.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Überwachung von Ebenen in AD FS für WindowsServer 2016  
Standardmäßig hat AD FS unter Windows Server 2016 grundlegende Überwachung aktiviert.  Mit der grundlegenden Überwachung werden Administratoren 5 oder weniger Ereignisse für eine einzelne Anforderung angezeigt.  Dies kennzeichnet erheblich verringert die Anzahl der Ereignisse, die Administratoren haben, um zu überprüfen, um eine einzelne Anforderung finden Sie unter.   Die Überwachungsebene kann ausgelöst werden, oder mithilfe der PowerShell-Cmdlet gesenkt: Set-AdfsProperties - AuditLevel.  In der folgenden Tabelle wird erläutert, die Überwachung Detailebenen.  
  
||||  
|-|-|-|  
|Überwachungsebene|PowerShell-syntax|Beschreibung|  
|Keine|Set-AdfsProperties - AuditLevel keine|Die Überwachung deaktiviert ist und keine Ereignisse protokolliert werden.|  
|Basis (Standard)|Set-AdfsProperties - AuditLevel Basic|Für eine einzelne Anforderung werden nicht mehr als 5 Ereignisse protokolliert werden|  
|Ausführliche|Set-AdfsProperties - Verbose AuditLevel|Alle Ereignisse werden protokolliert.  Dadurch wird eine beträchtliche Menge an Daten pro Anforderung protokolliert.|  
  
Um die aktuelle Überwachungsebene anzuzeigen, können Sie die PowerShell-Cmdlet: Get-AdfsProperties.  
  
![die Verbesserte Überwachung](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
Die Überwachungsebene kann ausgelöst werden, oder mithilfe der PowerShell-Cmdlet gesenkt: Set-AdfsProperties - AuditLevel.  
  
![die Verbesserte Überwachung](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>Arten von Überwachungsereignissen  
AD FS-Überwachungsereignisse können verschiedener Typen, die basierend auf den unterschiedlichen Arten von Anforderungen von AD FS verarbeitet werden. Jedes Überwachungsereignis hat bestimmte Daten zugeordnet.  Der Typ der Überwachungsereignisse kann zwischen Anmelde-Anforderungen (d. h. tokenanforderungen) im Vergleich zu den Anforderungen des Systems (Server-zu-Server-Aufrufe auch das Abrufen von Konfigurationsinformationen) unterschieden werden.    
  In der folgenden Tabelle werden die grundlegenden Typen von Überwachungsereignissen beschrieben.  
  
||||  
|-|-|-|  
|Ereignis des Typs überwachen|Ereignis-ID|Beschreibung|  
|Neue Credential Überprüfung erfolgreich|1202|Eine Anforderung, in denen aktuelle Anmeldeinformationen durch den Verbunddienst erfolgreich überprüft werden. Dazu gehören WS-Trust, WS-Federation, SAML-P (erste Abschnitt zum Generieren von SSO) und OAuth autorisieren Endpunkte.|  
|Neue Credential Überprüfungsfehler|1203|Eine Anforderung, in denen aktuelle Anmeldeinformationen für den Verbunddienst fehlgeschlagen. Dazu gehören WS-Trust, WS-eingezogen, SAML-P (erste Abschnitt zum Generieren von SSO) und OAuth autorisieren Endpunkte.|  
|Anwendung Token Erfolg|1200|Eine Anforderung, in denen ein Token vom Verbunddienst erfolgreich ausgestellt wird. Für die WS-Federation, SAML-P dies protokolliert, wenn die Anforderung mit den SSO-Artefakt verarbeitet wird. (z. B. das SSO-Cookie).|  
|Token Anwendungsfehler|1201|Eine Anforderung für den Verbunddienst tokenausstellungs Sicherheit ist fehlgeschlagen. Für die WS-Federation, SAML-P dies protokolliert, wenn die Anforderung mit den SSO-Artefakt verarbeitet wurde. (z. B. das SSO-Cookie).|  
|Kennwort ändern Anforderung Erfolg|1204|Eine Transaktion, die das Kennwort zu ändern, in denen Anforderung wurde vom Verbunddienst verarbeitet.|  
|Kennwort ändern Anforderungsfehler|1205|Eine Transaktion, die das Kennwort zu ändern, in denen Anforderung konnte vom Verbunddienst verarbeitet werden.| 
|Melden Sie sich erfolgreich|1206|Beschreibt eine erfolgreiche Abmelde Anforderung.|  
|Fehler beim Abmelden|1207|Beschreibt eine fehlerhafte Abmelde Anforderung.|  

  


