---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: "Checkliste – Konfigurieren von AD FS zur Nutzung der Ansprüche von AD FS 1.x"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfd06a28f8ccaa04014024a235cd19512adb181
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS für die Ansprüche an einen AD FS 1.x-Verbunddienst gesendet werden

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x-Verbunddienst  
Diese Prüfliste enthält die Aufgaben zum Konfigurieren der Active Directory-Verbunddienste \(AD FS\) Verbunddienst in Windows Server 2012 Ansprüche senden, die von einem AD FS 1. verstanden werden können. *x* Verbunddienst.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge. Wenn ein Link gelangen Sie zu einem Verfahren in diesem Thema nach Abschluss der Schritte in diesem Verfahren, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Konfigurieren von AD FS zum Senden von Ansprüchen](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x-Verbunddienst**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie für die Interoperabilität zwischen AD FS unter Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie, dass weitere Informationen zu den Name-ID Typ geltend machen.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Bevor Sie die Interoperabilität mit einer früheren Version von AD FS erreichen können, müssen Sie zunächst eine Vertrauensstellung der vertrauenden Seite in der AD FS-Verbunddienst, der AD FS 1. erstellen. *x* Verbunddienst. **Hinweis:** Sie eine Vertrauensstellung mit einem AD FS 1. können nicht erstellt. *x* Verbunddienst mithilfe von Verbundmetadaten.<br /><br />Wenn Sie die Vertrauensstellung mithilfe des Verfahrens in der Verknüpfung mit der rechten Seite einrichten, müssen Sie die folgenden Vertrauensstellungen der vertrauenden Seite Party Vertrauensstellung Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, für die Interoperabilität mit einem AD FS 1. tun. *x* Verbunddienst:<br /><br />1. auf die **Auswählen einer Datenquelle** Seite **eingeben von Daten über die Vertrauensstellungen der vertrauenden Seite Partei Vertrauensstellung manuell**.<br />2. auf die **Profil auswählen** Seite **AD FS 1.0- und 1.1-Profil**.<br />3. auf die **URL konfigurieren** Seite unter **URL des passiven WS-Verbund:**, geben die **Endpunkt-URLs des Verbunddiensts** gemäß Definition in der AD FS 1. *x* Verbunddienst des Partners.<br />4. auf die **Konfigurieren von Bezeichnern** Seite unter **Bezeichner Vertrauensstellung der vertrauenden Seite**, geben die **Verbunddienst-URI** gemäß Definition in der AD FS 1. *x* Verbunddienst des Partners.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine der vertrauenden Seite Party vertrauen manuell](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf dem vertrauenden Seite Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie erstellen Anspruch Regeln, die eingehenden Ansprüche, die aus einem Attributspeicher extrahiert wurden aufnehmen und pass-through, filtern oder transformieren sie in einer-ID werden Anspruchstyp, die verstehen und genutzt werden, von der AD FS 1. *x* Verbunddienst. **Hinweis:** , bevor Sie diese Regel erstellen, stellen Sie sicher, dass der anspruchsregelsatz, in denen Sie diese Regel erstellen, eine Regel, die vor dem stammt, der einen Lightweight Directory Access Protocol \(LDAP\) Attribut Anspruch zunächst aus einem Attributspeicher extrahiert. Dies wird als Eingabe für die Regel verwendet werden, die Sie zum Senden von einem AD FS 1. erstellen. *x*\-compatible Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren von einem LDAP-Attribut finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen eine Regel zum Senden von einem AD FS 1.x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des AD FS 1. *x* Verbunddiensts und den Administrator des AD FS 1. *x* Verbunddienst Einrichten einer neuen Konto Partner-Vertrauensstellung. Außerdem bieten dem Administrator mit dem Verbunddienst-URI \ (in der Verbunddienst Properties\), der passiven WS-Federation-Endpunkt-URL \ (den Verbunddienst Endpunkt URL\), und eine exportierte Token\-Signaturzertifikat Datei \ (mit dem öffentlichen Schlüssel Only\). Diese Administratoren benötigen diese Elemente, um die Vertrauensstellung einrichten.|N\/A|  
  

