---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Überwachung von Erweiterungen für AD FS unter Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4eb93513d12b2bba2620ff16be24f62ace5dee85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407258"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Überwachung von Erweiterungen für AD FS unter Windows Server 2016


Derzeit gibt es in AD FS für Windows Server 2012 R2 zahlreiche Überwachungs Ereignisse, die für eine einzelne Anforderung generiert werden, und die relevanten Informationen zu einer Anmelde-oder tokenausstellungsaktivität sind entweder nicht vorhanden (in einigen Versionen AD FS) oder auf mehrere Überwachungs Ereignisse verteilt. Standardmäßig sind die AD FS Überwachungs Ereignisse aufgrund ihrer ausführlichen Art deaktiviert.  
    Mit der Veröffentlichung von AD FS in Windows Server 2016 wird die Überwachung optimiert und ist weniger ausführlich.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Überwachungs Stufen in AD FS für Windows Server 2016  
Standardmäßig ist für AD FS in Windows Server 2016 die grundlegende Überwachung aktiviert.  Bei der grundlegenden Überwachung sehen Administratoren maximal 5 oder weniger Ereignisse für eine einzelne Anforderung.  Dies kennzeichnet einen signifikanten Rückgang der Anzahl von Ereignissen, die Administratoren untersuchen müssen, um eine einzelne Anforderung anzuzeigen.   Die Überwachungs Ebene kann mithilfe des PowerShell-cmdlt ausgelöst oder verringert werden:  Set-ADF sproperties-AuditLevel.  In der folgenden Tabelle werden die verfügbaren Überwachungs Stufen erläutert.  
  
||||  
|-|-|-|  
|Überwachungsebene|PowerShell-Syntax|Beschreibung|  
|Keine|Set-ADF sproperties-AuditLevel None|Die Überwachung ist deaktiviert, und es werden keine Ereignisse protokolliert.|  
|Basic (Standard)|Set-ADF sproperties-AuditLevel Basic|Für eine einzelne Anforderung werden höchstens 5 Ereignisse protokolliert.|  
|Ausführlich|Set-ADF sproperties-AuditLevel Verbose|Alle Ereignisse werden protokolliert.  Dadurch wird eine beträchtliche Menge an Informationen pro Anforderung protokolliert.|  
  
Zum Anzeigen der aktuellen Überwachungs Ebene können Sie das PowerShell-Cmdlet verwenden:  Get-ADF sproperties.  
  
![Überwachungs Erweiterungen](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
Die Überwachungs Ebene kann mithilfe des PowerShell-cmdlt ausgelöst oder verringert werden:  Set-ADF sproperties-AuditLevel.  
  
![Überwachungs Erweiterungen](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>Typen von Überwachungs Ereignissen  
AD FS Überwachungs Ereignisse können unterschiedliche Typen aufweisen, basierend auf den verschiedenen Typen von Anforderungen, die von AD FS verarbeitet werden. Jeder Art von Überwachungs Ereignis sind bestimmte Daten zugeordnet.  Der Typ der Überwachungs Ereignisse kann zwischen Anmelde Anforderungen (d. h. Tokenanforderungen) und Systemanforderungen (Server-Server-Aufrufe einschließlich Abrufen von Konfigurationsinformationen) unterschieden werden.    
  In der folgenden Tabelle werden die grundlegenden Typen von Überwachungs Ereignissen beschrieben.  
  
||||  
|-|-|-|  
|Audit-Ereignistyp|Ereignis-ID|Beschreibung|  
|Erfolgreiche Überprüfung der Anmelde Informationen erfolgreich|1202|Eine Anforderung, bei der neue Anmelde Informationen erfolgreich vom Verbunddienst überprüft werden. Dies umfasst WS-Trust, WS-Federation, SAML-P (erster Teil zum Generieren von SSO) und OAuth-Autorisierungs Endpunkte.|  
|Fehler bei der Validierung der neuen Anmelde Informationen|1203|Eine Anforderung, bei der die Überprüfung der neuen Anmelde Informationen für den Verbunddienst fehlgeschlagen ist Hierzu gehören WS-Trust, WS-Fed, SAML-P (erster Teil zum Generieren von SSO) und OAuth-Autorisierungs Endpunkte.|  
|Anwendungs Token erfolgreich|1200|Eine Anforderung, bei der ein Sicherheits Token erfolgreich vom Verbunddienst ausgestellt wird. Für WS-Federation wird SAML-P protokolliert, wenn die Anforderung mit dem SSO-Element verarbeitet wird. (z. b. das SSO-Cookie).|  
|Anwendungs Token-Fehler|1201|Eine Anforderung, bei der die sicherheitstokenausstellung im Verbunddienst fehlgeschlagen ist Für WS-Federation wird SAML-P bei der Verarbeitung der Anforderung mit dem SSO-Element protokolliert. (z. b. das SSO-Cookie).|  
|Anforderung zum Ändern von Kenn Wörtern erfolgreich|1204|Eine Transaktion, bei der das Kennwort Change Request erfolgreich vom Verbunddienst verarbeitet wurde.|  
|Fehler beim Ändern der Kenn Wort Änderung|1205|Eine Transaktion, bei der das Kennwort Change Request nicht vom Verbunddienst verarbeitet werden konnte.| 
|Erfolg abmelden|1206|Beschreibt eine erfolgreiche Abmelde Anforderung.|  
|Abmelde Fehler|1207|Beschreibt eine fehlgeschlagene Abmelde Anforderung.|  

  


