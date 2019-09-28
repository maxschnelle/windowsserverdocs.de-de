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

Um eine neue Partnerorganisation in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 bereitzustellen, führen Sie die Aufgaben entweder in [checkliste aus: Konfigurieren der Ressourcen Partner Organisation @ no__t-0 oder [prüfliste: Konfigurieren der Konto Partner Organisation @ no__t-0, je nach AD FS Design.  
  
> [!NOTE]  
> Wenn Sie eine dieser Checklisten verwenden, wird dringend empfohlen, zuerst die Verweise auf den Planungsleitfaden für Konto Partner oder Ressourcen Partner im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) zu lesen, bevor Sie mit den Vorgehensweisen zum Einrichten der neue Partnerorganisation. Wenn Sie die Prüfliste auf diese Weise befolgen, erhalten Sie ein besseres Verständnis der vollständigen AD FS Design-und Bereitstellungs Geschichte für den Konto Partner oder die Ressourcen Partnerorganisation.  
  
## <a name="about-account-partner-organizations"></a>Informationen zu Konto Partnerorganisationen  
Ein Konto Partner ist die Organisation in der Verbund Vertrauensstellung, die Benutzerkonten physisch in einem AD FS – unterstützten Attribut Speicher speichert. Der Konto Partner ist verantwortlich für das erfassen und Authentifizieren der Anmelde Informationen eines Benutzers, das Einrichten von Ansprüchen für diesen Benutzer und das Verpacken der Ansprüche in Sicherheits Token. Diese Token können dann über eine Verbund Vertrauensstellung hinweg angezeigt werden, um den Zugriff auf Web @ no__t-0based-Ressourcen zu ermöglichen, die sich in der Ressourcen Partnerorganisation befinden.  
  
Anders ausgedrückt: ein Konto Partner stellt die Organisation dar, deren Benutzer das Konto @ no__t-0side Federation Server Security Tokens ausgibt. Der Verbund Server in der Konto Partnerorganisation authentifiziert lokale Benutzer und erstellt Sicherheits Token, die der Ressourcen Partner verwendet, um Autorisierungs Entscheidungen zu treffen.  
  
Im Hinblick auf Attribut Speicher entspricht der Konto Partner in AD FS konzeptionell einer einzelnen Active Directory Gesamtstruktur, deren Konten Zugriff auf Ressourcen benötigen, die sich physisch in einer anderen Gesamtstruktur befinden. Konten in dieser Gesamtstruktur können nur auf Ressourcen in der Ressourcen Gesamtstruktur zugreifen, wenn zwischen den beiden Gesamtstrukturen eine externe Vertrauensstellung oder eine Gesamtstruktur-Vertrauensstellung besteht und die Ressourcen, auf die die Benutzer zugreifen möchten, mit der entsprechenden Autorisierung festgelegt wurden. Griff.  
  
## <a name="about-resource-partner-organizations"></a>Informationen zu Ressourcen Partnerorganisationen  
Der Ressourcen Partner ist die Organisation in einer AD FS Bereitstellung, in der sich Webserver befindet. Der Ressourcen Partner vertraut dem Konto Partner, um Benutzer zu authentifizieren. Um Autorisierungs Entscheidungen zu treffen, verwendet der Ressourcen Partner daher die Ansprüche, die in Sicherheits Token gepackt sind, die von Benutzern des Konto Partners stammen.  
  
Anders ausgedrückt: ein Ressourcen Partner stellt die Organisation dar, deren Webserver durch die Ressource @ no__t-0side Federation Server geschützt sind. Der Verbund Server beim Ressourcen Partner verwendet die Sicherheits Token, die vom Konto Partner erstellt werden, um Autorisierungs Entscheidungen für Webserver im Ressourcen Partner zu treffen.  
  
Um als AD FS Ressource zu fungieren, muss auf den Webservern in der Ressourcen Partnerorganisation entweder Windows Identity Foundation \(wif @ no__t-1 installiert sein, oder die Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-3 1. x Claims @ no__t-4aware Web Agent-Rollen Dienste sind installiert. Webserver, die als AD FS Ressource fungieren, können entweder Web @ no__t-0browser @ no__t-1based oder Web @ no__t-2service @ no__t-3based-Anwendungen hosten.  
