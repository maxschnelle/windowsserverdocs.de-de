---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: Konfigurieren von Partnerorganisationen
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5494f3bd8d012bf1ecc240439ff880d1bb52c280
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configuring-partner-organizations"></a>Konfigurieren von Partnerorganisationen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Um eine neue Partnerorganisation in Active Directory Federation Services \(AD FS\) bereitzustellen, führen Sie die Aufgaben in einem [Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](Checklist--Configuring-the-Resource-Partner-Organization.md) oder [Prüfliste: Konfigurieren der Kontopartnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md)abhängig von der AD FS-Entwurfs.  
  
> [!NOTE]  
> Wenn Sie eine der folgenden Prüflisten verwenden, wird dringend empfohlen, lesen Sie zunächst die Verweise auf Kontopartner oder Planen der Anleitung im Ressourcenpartner die [AD FS-Entwurfshandbuch in Windows Server2012](https://technet.microsoft.com/library/dd807036.aspx) vor dem fortfahren zu den Vorgehensweisen zum Einrichten der neuen Partnerorganisation. Befolgen die Checkliste auf diese Weise können ein besseres Verständnis der AD FS Entwurfs- und umfassende für der Kontopartnerorganisation Partner oder Ressource bereitstellen.  
  
## <a name="about-account-partner-organizations"></a>Informationen zu kontopartnerorganisationen  
Ein Kontopartner ist die Organisation in der verbundvertrauensstellung, die physisch Benutzerkonten in einem AD FS unterstützte Attributspeicher speichert. Der Kontopartner ist sammeln und Authentifizieren der Anmeldeinformationen eines Benutzers, das Zusammenstellen von Ansprüchen für diesen Benutzer und das Integrieren der Ansprüche in Sicherheitstoken. Diese Token können dann angezeigt werden, über eine verbundvertrauensstellung ermöglichen den Zugriff auf webbasierte Ressourcen, die in der Ressourcenpartnerorganisation befinden.  
  
Anders ausgedrückt, stellt Kontopartner die Organisation, für die Benutzer der Zuordnung überprüfen\ clientseitigen Verbundserver Sicherheitstoken ausstellt. Der Verbundserver in der Kontopartnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheitstoken, die der Ressourcenpartner verwendet bei der Bereitstellung von Autorisierungsentscheidungen.  
  
In Bezug auf Attributspeicher entspricht der Kontopartner in AD FS vom Konzept her einer Active Directory-Gesamtstruktur, deren Konten auf Ressourcen zugreifen, die sich physisch in einer anderen Gesamtstruktur befinden. Konten in dieser Gesamtstruktur können Ressourcen in der Gesamtstruktur zugreifen, nur, wenn eine externe Vertrauensstellung oder Gesamtstruktur-Vertrauensstellung Beziehung zwischen den beiden Gesamtstrukturen vorhanden ist und dass die Ressourcen, die Benutzer versuchen, für den Zugriff, mit den Berechtigungen für die ordnungsgemäße Autorisierung festgelegt wurden.  
  
## <a name="about-resource-partner-organizations"></a>Informationen zu ressourcenpartnerorganisationen  
Der Ressourcenpartner ist die Organisation in einer AD FS-Bereitstellung in dem sich Webserver befinden. Der Ressourcenpartner vertraut den Kontopartner, um Benutzer zu authentifizieren. Daher nutzt der Ressourcenpartner zur Autorisierung von Entscheidungen, die Ansprüche, die in Sicherheitstoken gepackt sind, die von Benutzern in der Kontopartner stammen.  
  
Anders ausgedrückt, stellt Ressourcenpartner die Organisation, die vom Verbundserver Resource\-Seite, deren Webserver geschützt sind. Der Verbundserver an den Ressourcenpartner verwendet die Sicherheitstoken, die der Kontopartner zum treffen von Autorisierungsentscheidungen für Webserver in der Ressourcenpartnerorganisation erzeugt werden.  
  
Wie AD FS-Ressource, Webserver in der Ressourcenpartnerorganisation Windows Identity Foundation \(WIF\) entweder benötigen, installiert, oder die Active Directory Federation Services \(AD FS\) 1.x Claims\-Aware Web Agent-Rollendienste installiert haben. Webserver, die als AD FS-Ressource fungieren können entweder Browser\-webbasierten oder Service\-webbasierten Anwendungen gehostet werden.  
