---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: -Checkliste – Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bd4c436c806074f63bf51f497429532d7be32f75
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192414"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem Verbunddienst von AD FS 1.x

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Federation Service  
Diese Prüfliste enthält die Aufgaben, die erforderlich sind, für die Konfiguration Ihrer Active Directory Federation Services \(AD FS\) Verbunddienst in Windows Server 2012, um Ansprüche zu senden, die von einem AD FS 1. verstanden werden. *X* Verbunddienst.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link zu einer Prozedur gelangen, geben zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren abgeschlossen haben, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Konfigurieren von AD FS zum Senden von Ansprüchen](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Federation Service**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie der Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über die ID der Anspruchstyp.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Bevor Sie Interoperabilität mit einer früheren Version von AD FS erreichen können, müssen Sie zuerst eine Vertrauensstellung der vertrauenden Seite in AD FS-Verbunddienst auf dem AD FS-1. erstellen. *x* Verbunddienst. **Hinweis**: Sie können keine Vertrauensstellung mit einem AD FS 1. erstellen. *x* Federation Service mithilfe von Verbundmetadaten.<br /><br />Beim Einrichten der Vertrauensstellung mit dem Verfahren in den Link, um das Recht, müssen Sie die folgenden der vertrauenden Seite Party Trust Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, die Interoperabilität mit einem AD FS 1. tun. *x* Verbunddienst:<br /><br />1.  Auf der **Auswählen einer Datenquelle** Seite **eingeben von Daten über die abhängige Partei Vertrauensstellung manuell**.<br />2.  Auf der **Profil auswählen** Seite **AD FS 1.0 und 1.1-Profil**.<br />3.  Auf der **-URL konfigurieren** Seite **WS\-URL des passiven Verbunds**, Typ der **Verbunddienst-Endpunkt-URL** gemäß der in der AD FS 1. *X* Verbunddienst des Partners.<br />4.  Auf der **Konfigurieren von Bezeichnern** Seite **Trust-Bezeichner der vertrauenden Seite**, Typ der **Verbunddienst-URI** gemäß der in der AD FS 1. *X* Verbunddienst des Partners.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[eine verlassen Partei vertrauen manuell erstellen](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf die vertrauenden Seite Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie die Forderung, dass die Regeln, die dauern der eingehenden Ansprüche, die in einem Attributspeicher extrahiert wurden und pass-through-, filtern oder deren Umwandlung in eine Name-ID werden Typ beansprucht, die verstanden werden können und die vom AD genutzt werden kann erstellen FS 1. *x* Verbunddienst. **Hinweis**: Bevor Sie mit dieser Regel erstellen, stellen sicher, dass der Satz von Ansprüchen Regel Sie mit dieser Regel erstellen eine Regel, die es vorangeht, die zuerst ein Lightweight Directory Access Protocol extrahiert \(LDAP\) Attribut Anspruch in einem Attributspeicher. Dieser Anspruch wird als Eingabe für die Regel verwendet werden, die Sie erstellen, um einen AD FS 1. zu senden. *x*\--kompatibler Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren von einem LDAP-Attribut finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine Regel zum Senden von AD FS 1.x-kompatibler Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des AD FS 1. *x* Verbunddienst und lassen Sie den Administrator des AD FS 1. *X* Verbunddienst Einrichten einer neuen Konto Partner Vertrauensstellung. Geben Sie außerdem mit dem Verbund-Dienst-URI der Administrator \(in den Eigenschaften des Verbunddiensts\), WS\-passiven Verbund-Endpunkt-URL \(die Endpunkt-URL des Verbunddiensts\), und ein Token exportierten\-Zertifikatdatei signieren \(mit öffentlichen Schlüssel nur\). Dieser Administrator benötigen Folgendes, um die Vertrauensstellung einzurichten.|N\/A|  
  

