---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Überwachung von Erweiterungen für AD FS unter Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3d622686a3cc34316f0cf5187839785195c2f104
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880231"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Überwachung von Erweiterungen für AD FS unter Windows Server 2016

>Gilt für: Windows Server 2016

Derzeit in AD FS für Windows Server 2012 R2 gibt es zahlreiche Überwachungsereignisse, die für eine einzelne Anforderung und die relevanten Informationen zu einer Anmeldung generiert werden oder die Ausstellung von token-Aktivität ist entweder nicht vorhanden (in einigen Versionen von AD FS) oder über mehrere Überwachungsereignisse verbreiten sich. Der AD FS werden Überwachungsereignisse aufgrund der Natur ausführliche standardmäßig deaktiviert.  
    Mit der Version von AD FS in Windows Server 2016-Überwachung optimierte und weniger ausführlich geworden.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Überwachung von Ebenen in AD FS für WindowsServer 2016  
Standardmäßig verfügt die AD FS unter Windows Server 2016 allgemeine Überwachung aktiviert.  Bei der grundlegenden Überwachung werden Administratoren 5 oder weniger Ereignisse für eine einzelne Anforderung finden Sie unter.  Kennzeichnet eine deutliche Verringerung der Anzahl der Ereignisse, die Administratoren haben, betrachten, um eine einzelne Anforderung finden Sie unter.   Die Überwachungsebene kann ausgelöst werden, oder gesenkt werden, mithilfe der PowerShell-Cmdlet:  Set-AdfsProperties -AuditLevel.  In der folgenden Tabelle erläutert die verfügbaren Überwachungsebenen dienen.  
  
||||  
|-|-|-|  
|Überwachungsebene|PowerShell-syntax|Beschreibung|  
|Keine|Set-AdfsProperties - AuditLevel keine|Die Überwachung ist deaktiviert, und keine Ereignisse protokolliert werden.|  
|Basic (Standard)|Set-AdfsProperties - AuditLevel Basic|Nicht mehr als 5 Ereignisse werden für eine einzelne Anforderung protokolliert|  
|Ausführlich|Set-AdfsProperties - AuditLevel-Verbose|Alle Ereignisse werden protokolliert.  Dadurch wird eine beträchtliche Menge an Daten pro Anforderung protokolliert.|  
  
Zum Anzeigen der aktuellen Ebene für die Überwachung können Sie die PowerShell-Cmdlet verwenden:  Get-AdfsProperties.  
  
![die Verbesserte Überwachung](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
Die Überwachungsebene kann ausgelöst werden, oder gesenkt werden, mithilfe der PowerShell-Cmdlet:  Set-AdfsProperties -AuditLevel.  
  
![die Verbesserte Überwachung](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>Arten von Überwachungsereignissen  
AD FS-Überwachungsereignisse können verschiedener Typen, die basierend auf die verschiedenen Typen von Anforderungen, die von AD FS verarbeitet werden. Jedes Überwachungsereignis verfügt über bestimmte Daten zugeordnet.  Der Typ von Überwachungsereignissen kann zwischen anmeldeanforderungen (d. h. tokenanforderungen) im Vergleich zu den Anforderungen des Systems (einschließlich Konfigurationsinformationen abrufen Servern-Aufrufe) unterschieden werden.    
  Die folgende Tabelle beschreibt die grundlegenden Typen von Überwachungsereignissen.  
  
||||  
|-|-|-|  
|Audit-Ereignis des Typs|Ereignis-ID|Beschreibung|  
|Neue Anmeldeinformationen Validierung erfolgreich|1202|Eine Anforderung, in dem neue Anmeldeinformationen erfolgreich vom Verbunddienst überprüft werden. Dies schließt die WS-Trust, WS-Federation, SAML-P (ersten Abschnitt zum Generieren von SSO) und Autorisieren von OAuth-Endpunkte.|  
|Überprüfungsfehler für die neuen Anmeldeinformationen|1203|Eine Anforderung, in dem neue Anmeldeinformationen für den Verbunddienst Fehler bei der Überprüfung. Dies schließt die WS-Trust, WS-Fed-, SAML-P (ersten Abschnitt zum Generieren von SSO) und Autorisieren von OAuth-Endpunkte.|  
|Anwendung Token erfolgreich|1200|Eine Anforderung, in denen ein Sicherheitstoken vom Verbunddienst erfolgreich ausgegeben wird. Für WS-Verbund, SAML-P-dies protokolliert, wenn es sich bei der Verarbeitung der Anforderung mit der SSO-Element. (z. B. das SSO-Cookie).|  
|Fehler bei der Anwendung Token|1201|Eine Anforderung, an der tokenausstellung Sicherheit für den Verbunddienst fehlgeschlagen ist. Für WS-Verbund, SAML-P-dies protokolliert, wenn die Anforderung, mit der SSO-Element verarbeitet wurde. (z. B. das SSO-Cookie).|  
|Anforderung wurde erfolgreich von Kennwort geändert|1204|Eine Transaktion, in denen Anforderung der kennwortänderung, wurde erfolgreich vom Verbunddienst verarbeitet.|  
|Kennwort ändern-Anforderungsfehler|1205|Eine Transaktion, in denen Anforderung der kennwortänderung, nicht durch den Verbunddienst verarbeitet werden konnten.| 
|Melden Sie sich erfolgreich|1206|Beschreibt eine erfolgreiche Anforderung zur Abmelde.|  
|Fehler beim Abmelden|1207|Beschreibt eine Anforderung zur Abmelde und Fehler an.|  

  


