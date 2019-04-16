---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: "Checkliste – Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6b0ece3274b0e0a2a0d5e18e3c0ebf10ded67ebe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Diese Prüfliste enthält Aufgaben für die Planung, Entwurf und Bereitstellung von Anspruchsregeln, die eine Anspruchsanbieter-Vertrauensstellung in Active Directory Federation Services \(AD FS\) zugeordnet sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge. Wenn ein Link gelangen Sie zu einem Verfahren in diesem Thema nach Abschluss der Schritte in diesem Verfahren, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Erstellen von Anspruchsregeln](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Erstellen einer Anspruchsregel legen Sie für eine Anspruchsanbieter-Vertrauensstellung**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Überprüfen Sie die Konzepte zu Ansprüchen, Anspruchsregeln, Regel Anspruchssätze und geltend machen, Vorlagen und wie sie leistungsfähigen Verbundvertrauensstellungen zugeordnet sind.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of Claims](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[der Rolle der Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Informieren Sie sich über alle Phasen in die anspruchsausstellungs-Pipeline wie ein Anspruch durchläuft, und wie Regeln durch das anspruchsausgabemodul verarbeitet werden.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claims Pipeline](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Um effektiv planen und implementieren die Ausgabe Ansprüche, die über diese Anspruchsanbieter-Vertrauensstellung ausgegeben wird, bestimmen Sie, ob eine oder mehrere Anspruchsregeln erforderlich sind und die Anspruchsregeln, die diese Anspruchsanbieter-Vertrauensstellung verwendet werden soll.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[bestimmen Sie den Typ der Anspruch Regelvorlage verwenden](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Bei einem Anspruch Erstellen der Regel über ein anderes und Verwendung die anspruchsregelsprache komplexeren Logik als Standardregeln bereitstellen, um das gewünschte Ergebnis in der Ausgabe der ideale geliefert eingabeanspruchssatz Konzepte zu überprüfen.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[einen Pass-Through oder Filterregel Anspruch verwenden](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[transformieren Anspruch Regel verwenden](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a Send LDAP Attributes as Claims Rule verwenden](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a Send Group Membership Anspruch in der Regel verwenden](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[verwenden eine benutzerdefinierte Anspruchsregel-Regel](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claim Rule Language](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Eine anspruchsbeschreibung erstellt werden muss, wenn nicht bereits vorhanden ist, die die Bedürfnisse Ihrer Organisation erfüllt wird. Im Lieferumfang von AD FS ist eines Standardsatz von anspruchsbeschreibungen, die in AD FS-Verwaltungs-Snap-in verfügbar gemacht werden.|![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Hinzufügen einer Anspruchsbeschreibung](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Je nach den Anforderungen Ihrer Organisation erstellen Sie eine oder mehrere Anspruchsregeln für die Annahme Transformation Regeln festgelegt, die diese Anspruchsanbieter-Vertrauensstellung zugeordnet ist, sodass entsprechend Ansprüche ausgestellt werden.|![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen eine Regel zum Senden eines Authentifizierung Methode Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen eine Regel zum Senden von einem AD FS 1.x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen eine Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
  

