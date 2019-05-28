---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: Konfigurieren von Partnerorganisationen
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3d7389ce806a5e3aebf4fe166b10e5262df0be8a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192237"
---
# <a name="configuring-partner-organizations"></a>Konfigurieren von Partnerorganisationen

Bereitstellen eine neuen Partnerorganisation in Active Directory-Verbunddienste \(AD FS\), führen Sie die Aufgaben in einem [Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](Checklist--Configuring-the-Resource-Partner-Organization.md) oder [Prüfliste: Konfigurieren der Kontopartnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md), abhängig von Ihrer AD FS-Entwurfs.  
  
> [!NOTE]  
> Wenn Sie einer dieser Prüflisten verwenden, es wird dringend empfohlen, dass Sie die Verweise auf Kontopartner oder planen die Anleitung im Ressourcenpartner lesen Sie zuerst die [AD FS-Entwurfshandbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) vor dem Fortfahren mit der Verfahren für das Einrichten der neuen Partnerorganisation. Mithilfe der folgenden Checkliste für die auf diese Weise können bieten ein besseres Verständnis der AD FS Design und Bereitstellung ganz für der Kontopartnerorganisation Partner oder Ressource.  
  
## <a name="about-account-partner-organizations"></a>Informationen zu kontopartnerorganisationen  
Kontopartner ist die Organisation in der verbundvertrauensstellung, die physisch Benutzerkonten in einem AD FS unterstützte Attributspeicher speichert. Kontopartner ist für das Sammeln von und die Anmeldeinformationen eines Benutzers zu authentifizieren, um Ansprüche für diesen Benutzer erstellen und Packen die Ansprüche in Sicherheitstokens verantwortlich. Mit diesen Token können dann über eine verbundvertrauensstellung So aktivieren Sie den Zugriff auf Web angezeigt werden\-Ressourcen, die in der Ressourcenpartnerorganisation befinden.  
  
Das heißt, Kontopartner stellt die Organisation dar, dessen Benutzer das Konto\-Verbundserver Seite Ausstellen von Sicherheitstoken. Der Verbundserver in der Kontopartnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheitstoken, die der Ressourcenpartner wird verwendet, in das treffen von autorisierungsentscheidungen.  
  
Im Hinblick auf Attributspeicher ist der Kontopartner AD FS vergleichbar mit einer einzelnen Active Directory-Gesamtstruktur, deren Konten Zugriff auf Ressourcen benötigen, die physisch in einer anderen Gesamtstruktur befinden. Konten in dieser Gesamtstruktur können Zugriff auf Ressourcen in der Ressourcengesamtstruktur nur, wenn eine externe Vertrauensstellung oder eine Beziehung zwischen den beiden Gesamtstrukturen vorhanden ist und die Ressourcen, die Benutzer Zugriff erhalten möchten, die richtige Autorisierung festgelegt wurden, vertraut Gesamtstruktur Berechtigungen.  
  
## <a name="about-resource-partner-organizations"></a>Informationen zu ressourcenpartnerorganisationen  
Der Ressourcenpartner ist die Organisation in einer AD FS-Bereitstellung, in dem sich Webserver befinden. Der Ressourcenpartner wird den Kontopartnern zum Authentifizieren von Benutzern. Um autorisierungsentscheidungen zu treffen, nutzt der Ressourcenpartner aus diesem Grund die Ansprüche, die in Sicherheitstoken gepackt werden, die von Benutzern in der Kontopartner stammen.  
  
Das heißt, ein Ressourcenpartner die Organisation, deren Webserver werden von der Ressource geschützt, darstellt\-Verbundserver für die Seite. Der Verbundserver in der Ressourcenpartner verwendet die Sicherheitstoken, die vom Kontopartner autorisierungsentscheidungen für Webserver beim Ressourcenpartner erstellt werden.  
  
Als AD FS-Ressource funktioniert, müssen Webserver in der Ressourcenpartnerorganisation Windows Identity Foundation entweder haben \(WIF\) installiert oder über die Active Directory Federation Services \(AD FS\) 1.x Ansprüche\-Aware Web Agent-Rollendienste installiert. Web-Server, die wie AD FS-Ressource entweder Web hosten kann\-Browser\-basieren oder Web-\-Service\--basierte Anwendungen.  
