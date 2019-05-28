---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: Prüfliste – vertrauen Erstellen von Anspruchsregeln für Anspruchsanbieter
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 708919691f88cc49d1f2bd74d8f4255e1a854353
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192389"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung


Diese Prüfliste enthält die Aufgaben zur Planung, Entwurf und Bereitstellung von Anspruchsregeln, die ein Anspruchsanbieter zugeordnet sind in Active Directory-Verbunddienste vertrauen \(AD FS\).  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link zu einer Prozedur gelangen, geben zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren abgeschlossen haben, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Erstellen von Anspruchsregeln](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Ein anspruchsregelsatz für eine Anspruchsanbieter-Vertrauensstellung erstellen**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Überprüfen Sie die Konzepte zu Ansprüchen, Anspruchsregeln Sie, Ansprüchen Sie Regelsätze von und beanspruchen Sie, Vorlagen und wie sie Verbundvertrauensstellungen zugeordnet sind.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of Claims](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[die Rolle der Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Informieren Sie sich über alle Stufen in die anspruchsausstellungs-Pipeline wie ein Anspruch durchlaufen, und wie Regeln durch die anspruchsausstellungs-Engine verarbeitet werden.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[die Rolle der Anspruchspipeline](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[die Rolle der Anspruchs-Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Zur effektiven Planung und Implementierung der Ansprüche, die für diese Anspruchsanbieter-Vertrauensstellung ausgegeben werden, bestimmen Sie, ob eine oder mehrere Anspruchsregeln erforderlich sind, und die Anspruchsregeln, die Sie mit diesem Anspruchsanbieter-Vertrauensstellung verwenden sollten.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[bestimmt der Typ des Anspruchs Regelvorlage verwenden](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Überprüfen Sie die Konzepte zu, wenn So erstellen Sie einen Anspruch Regel gegenüber einer anderen, und wie Sie die anspruchsregelsprache verwenden können, um eine komplexere Logik als standard Regeln geben an, um ein gewünschtes Ergebnis in die ideale Ausgabe bieten eingabeanspruchssatz.|![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Verwendung einer Pass-Through oder Filtern Anspruchsregel](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Verwendung einer Transformation Anspruchsregel](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[wann a Send LDAP Attributes as Claims Rule verwenden](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a Send Group Membership Anspruch in der Regel verwenden](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[verwenden Sie eine benutzerdefinierte Anspruchsregel](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![Erstellen von Anspruchsregeln](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claim Rule Language](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Eine anspruchsbeschreibung muss erstellt werden, wenn Sie noch nicht vorhanden ist, die die Anforderungen Ihrer Organisation erfüllen. AD FS im Lieferumfang von eines Standardsatz von anspruchsbeschreibungen, die verfügbar gemacht werden im AD FS-Verwaltungs-Snap-\-in.|![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Hinzufügen einer Anspruchsbeschreibung](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![Erstellen von Anspruchsregeln](media/icon_checkboxo.gif)|Je nach den Anforderungen Ihres Unternehmens erstellen Sie eine oder mehrere Anspruchsregeln für die Zustimmung zur Transformation fest, die diese Anspruchsanbieter-Vertrauensstellung zugeordnet ist, sodass Ansprüche entsprechend ausgegeben werden sollen.|![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen eine Regel für Pass-Through oder Filtern eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Erstellen einer Regel zum Senden der Gruppenmitgliedschaft als Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen Sie eine Regel zum Senden eines Anspruchs zu Authentifizierung-Methode](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen Sie eine Regel zum Senden von AD FS 1.x kompatibel Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![Erstellen von Anspruchsregeln](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[erstellen Sie eine Regel zum Senden von Ansprüchen mithilfe einer benutzerdefinierten Regel](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
  

