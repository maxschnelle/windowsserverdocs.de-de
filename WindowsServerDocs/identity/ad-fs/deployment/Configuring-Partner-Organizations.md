---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: Konfigurieren von Partner Organisationen
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 575d7e3fc97496c3f7c147220fe342add66517c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408398"
---
# <a name="configuring-partner-organizations"></a>Konfigurieren von Partner Organisationen

Zum Bereitstellen einer neuen Partnerorganisation in Active Directory-Verbunddienste (AD FS) \(AD FS\)führen Sie die Aufgaben entweder in der Prüfliste [: Konfigurieren der Ressourcen Partnerorganisation](Checklist--Configuring-the-Resource-Partner-Organization.md) oder Prüfliste [: Konfigurieren der Konto Partnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md)aus, abhängig von Ihrem AD FS Design.  
  
> [!NOTE]  
> Wenn Sie eine dieser Checklisten verwenden, wird dringend empfohlen, zuerst die Verweise auf den Planungsleitfaden für Konto Partner oder Ressourcen Partner im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) zu lesen, bevor Sie mit den Vorgehensweisen zum Einrichten der neuen Partnerorganisation fortfahren. Wenn Sie die Prüfliste auf diese Weise befolgen, erhalten Sie ein besseres Verständnis der vollständigen AD FS Design-und Bereitstellungs Geschichte für den Konto Partner oder die Ressourcen Partnerorganisation.  
  
## <a name="about-account-partner-organizations"></a>Informationen zu Konto Partnerorganisationen  
Ein Konto Partner ist die Organisation in der Verbund Vertrauensstellung, die Benutzerkonten physisch in einem AD FS – unterstützten Attribut Speicher speichert. Der Konto Partner ist verantwortlich für das erfassen und Authentifizieren der Anmelde Informationen eines Benutzers, das Einrichten von Ansprüchen für diesen Benutzer und das Verpacken der Ansprüche in Sicherheits Token. Diese Token können dann über eine Verbund Vertrauensstellung hinweg angezeigt werden, um den Zugriff auf Web\-basierten Ressourcen zu ermöglichen, die sich in der Ressourcen Partnerorganisation befinden.  
  
Anders ausgedrückt: ein Konto Partner stellt die Organisation dar, für deren Benutzer das Konto\-seitigen Verbund Servers Sicherheits Token ausgibt. Der Verbund Server in der Konto Partnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheits Token, die der Ressourcen Partner verwendet, um Autorisierungs Entscheidungen zu treffen.  
  
Im Hinblick auf Attribut Speicher entspricht der Konto Partner in AD FS konzeptionell einer einzelnen Active Directory Gesamtstruktur, deren Konten Zugriff auf Ressourcen benötigen, die sich physisch in einer anderen Gesamtstruktur befinden. Konten in dieser Gesamtstruktur können nur auf Ressourcen in der Ressourcen Gesamtstruktur zugreifen, wenn zwischen den beiden Gesamtstrukturen eine externe Vertrauensstellung oder eine Gesamtstruktur-Vertrauensstellung besteht und die Ressourcen, auf die die Benutzer zugreifen möchten, mit der entsprechenden Autorisierung festgelegt wurden. Griff.  
  
## <a name="about-resource-partner-organizations"></a>Informationen zu Ressourcen Partnerorganisationen  
Der Ressourcen Partner ist die Organisation in einer AD FS Bereitstellung, in der sich Webserver befindet. Der Ressourcen Partner vertraut dem Konto Partner, um Benutzer zu authentifizieren. Um Autorisierungs Entscheidungen zu treffen, verwendet der Ressourcen Partner daher die Ansprüche, die in Sicherheits Token gepackt sind, die von Benutzern des Konto Partners stammen.  
  
Anders ausgedrückt: ein Ressourcen Partner stellt die Organisation dar, deren Webserver durch die Ressource\-seitigen Verbund Servers geschützt werden. Der Verbund Server beim Ressourcen Partner verwendet die Sicherheits Token, die vom Konto Partner erstellt werden, um Autorisierungs Entscheidungen für Webserver im Ressourcen Partner zu treffen.  
  
Um als AD FS Ressource zu fungieren, muss auf den Webservern in der Ressourcen Partnerorganisation entweder Windows Identity Foundation \(WIF\) installiert sein, oder die Active Directory-Verbunddienste (AD FS) \(AD FS\) 1. x-Ansprüche\-die installierten Web-Agent-Rollen Dienste installiert sein. Webserver, die als AD FS Ressource fungieren, können entweder Web\-Browser\-oder auf Web\-Dienst\-basierten Anwendungen hosten.  
