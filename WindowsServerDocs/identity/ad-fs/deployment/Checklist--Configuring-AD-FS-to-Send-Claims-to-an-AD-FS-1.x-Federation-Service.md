---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: 'Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1. x'
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f91944333da9ce4c1d78bbbf7b3652f1118e1f08
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408508"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS, um Ansprüche an eine AD FS 1. x-Verbunddienst zu senden

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS, um Ansprüche an eine AD FS 1. x-Verbunddienst zu senden  
Diese Prüfliste enthält die Aufgaben, die zum Konfigurieren Ihrer Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 Verbunddienst in Windows Server 2012 erforderlich sind, um Ansprüche zu senden, die von einer AD FS 1 verstanden werden können. *x* -Verbunddienst.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn Sie über einen Verweis Link zu einer Prozedur gelangen, kehren Sie zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren ausgeführt haben, damit Sie mit den verbleibenden Aufgaben in dieser Prüfliste fortfahren können.  
  
![configure AD FS to Send Claims @ no__t-1checkprüfliste: Konfigurieren von AD FS für das Senden von Ansprüchen an eine AD FS 1. x Verbunddienst @ no__t-0  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie die Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über den Anspruchstyp "Name ID".|![configure AD FS, um die Anspruchs](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planung für die Interoperabilität mit AD FS 1. x](https://technet.microsoft.com/library/ff678040.aspx) zu senden.|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Bevor Sie die Interoperabilität mit einer früheren Version von AD FS erreichen können, müssen Sie zunächst eine Vertrauensstellung der vertrauenden Seite im AD FS Verbunddienst zum AD FS 1 erstellen. *x* -Verbunddienst. **Hinweis**: Es ist nicht möglich, eine Vertrauensstellung mit einem AD FS 1 zu erstellen. *x* Verbunddienst mithilfe von Verbund Metadaten.<br /><br />Wenn Sie die Vertrauensstellung mithilfe des Verfahrens im Link auf der rechten Seite einrichten, müssen Sie im Assistenten zum Hinzufügen von Vertrauens Stellungen der vertrauenden Seite die folgenden Schritte ausführen, um diese Vertrauensstellung für die Interoperabilität mit einem AD FS 1 einzurichten. *x* -Verbunddienst:<br /><br />1.  Wählen Sie auf der Seite **Datenquelle auswählen** die Option **Daten über die Vertrauensstellung der vertrauenden Seite manuell eingeben**aus.<br />2.  Wählen Sie auf der Seite **Profil auswählen** die Option **AD FS 1,0-und 1,1-Profil**aus.<br />3.  Geben Sie auf der Seite **URL konfigurieren** unter der **passiven URL von WS @ no__t-2federation**die **Verbunddienst Endpunkt-URL** ein, wie in der AD FS 1 definiert. *x* Verbunddienst des Partners.<br />4.  Geben Sie auf der Seite **Bezeichner** **Konfigurieren** unter Vertrauensstellungs-ID den **Verbunddienst URI** ein, wie in der AD FS 1 definiert. *x* Verbunddienst des Partners.|![configure AD FS to Send Claims (](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Manuelles Erstellen einer Vertrauensstellung der vertrauenden Seite](../../ad-fs/operations/Create-a-Relying-Party-Trust.md) )|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf der Vertrauensstellung der vertrauenden Seite, die Sie zuvor erstellt haben, müssen Sie Anspruchs Regeln erstellen, die eingehende Ansprüche akzeptieren, die aus einem Attribut Speicher extrahiert wurden, und Sie durchlaufen, Filtern oder transformieren. FS 1. *x* -Verbunddienst. **Hinweis**: Stellen Sie vor dem Erstellen dieser Regel sicher, dass der Anspruchs Regel Satz, für den Sie diese Regel erstellen, eine Regel enthält, die zuerst einen Lightweight Directory Access Protocol-\(ldap @ no__t-1-Attribut Anspruch aus einem Attribut Speicher extrahiert. Dieser Anspruch wird als Eingabe für die Regel verwendet, die Sie erstellen, um eine AD FS 1 zu senden. *x*\- kompatibler Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren eines LDAP-Attributs finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![configure AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Erstellen einer Regel zum Senden eines AD FS 1. x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des AD FS 1. *x* Verbunddienst und haben den Administrator des AD FS 1. *x* Verbunddienst Einrichten einer neuen Vertrauensstellung des Konto Partners. Stellen Sie diesem Administrator außerdem den Verbunddienst-URI \(in den Verbunddienst-Eigenschaften @ no__t-1, die URL des passiven WS @ no__t-2 Federation-Endpunkts \(the Verbunddienst Endpoint URL @ no__t-4 und ein exportiertes Token @ no__ t-5signing Certificate File \(with Public Key only @ no__t-7. Dieser Administrator benötigt diese Elemente, um die Vertrauensstellung einzurichten.|N\/A|  
  

