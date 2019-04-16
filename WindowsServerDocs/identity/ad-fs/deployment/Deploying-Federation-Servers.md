---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: Bereitstellen von Verbundservern
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 225e6b52ed46eef6f2ccacb5b0d9c6e6d880f475
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-servers"></a>Bereitstellen von Verbundservern

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Führen Sie zum Bereitstellen von Verbundservern in Active Directory Federation Services \(AD FS\) einzelnen Aufgaben in [Checklist: Setting Up a Federation Server](Checklist--Setting-Up-a-Federation-Server.md).  
  
> [!NOTE]  
> Wenn Sie diese Checkliste verwenden, es wird empfohlen, Sie zunächst die Verweise Lesen auf Federation Server planen, in der [AD FS-Entwurfshandbuch in Windows Server2012](https://technet.microsoft.com/library/dd807036.aspx) vor dem Beginn der Verfahren zum Konfigurieren der Server. Befolgen die Checkliste auf diese Weise bietet ein besseres Verständnis des Prozesses Entwurfs- und für Verbundserver.  
  
## <a name="about-federation-servers"></a>Informationen zu Verbundserver  
Verbundserver sind Computer, die unter Windows Server2008 mit der AD FS-Software installiert und konfiguriert wurden, um in die Verbundserver-Rolle verwendet werden. Verbundserver authentifizieren oder Weiterleiten von Anfragen von Benutzerkonten in anderen Organisationen und von Computern, auf denen eine beliebige Stelle im Internet gefunden werden können.  
  
Installieren der AD FS-Software auf einem Computer sowie das Verwenden von AD FS Federation Server-Konfigurations-Assistenten für die Verbundserver-Rolle konfigurieren, wird dieser Computer ein Verbundservers. Macht zudem AD FS-Verwaltungs-Snap-In zur Verfügung, auf dem Computer in der **Start\\Administrative Tools\\** Menü, damit können Sie Folgendes angeben:  
  
-   Der AD FS-Hostname, Partnerorganisationen und Anwendungen Token anfordert und Antworten senden können  
  
-   Die AD FS-Kennung, die Organisationen und Anwendungen Partner wird verwendet, um den eindeutigen Namen oder Speicherort Ihrer Organisation zu identifizieren  
  
-   Das Token\-Signaturzertifikat, das alle Verbundserver in einer Serverfarm zum Problem und sich von Token verwendet wird  
  
-   Der Speicherort der benutzerdefinierten ASP.NET Webseiten für Clientanmeldung, Abmeldung und Ermittlung von Kontopartnern, die der Client-Erlebnis wird  
  
    > [!NOTE]  
    > Die meisten dieser Core Benutzeroberflächeneinstellungen \(UI\) in der Datei "Web.config" auf jedem Verbundserver enthalten sind. AD FS-Hostname und AD FS-ID-Werte werden in der Datei "Web.config" nicht angegeben.  
  
Eine anspruchsausstellungsmodul, die basierend auf den Anmeldeinformationen Token ausstellt auf Verbundservern \ (z.B. Benutzernamen und Password\), die darauf angezeigt werden. Ein Token ist eine kryptografisch signierten Daten-Einheit, die eine oder mehrere Ansprüche drückt. Ein Anspruch ist eine Anweisung, die ein Server macht \ (z.B. Name, Identität, Schlüssel, Gruppe, Berechtigungen oder Capability\) zu einem Client. Nachdem die Anmeldeinformationen, auf dem Verbundserver überprüft wurden \ (über die Benutzer Anmeldung Process\), werden gesammelt, Ansprüche für den Benutzer über die Benutzer-Attribute, die in der angegebenen Attributspeicher gespeichert sind.  
  
Designs im Federated-Web-Single\-Sign\-On \(SSO\) \ (AD FS-Designs in der sind mindestens zwei Organisationen Involved\), Ansprüche von Anspruchsregeln für eine bestimmte vertrauende geändert werden können. Ansprüche sind in einem Token integriert, die an einen Verbundserver in der Ressourcenpartnerorganisation gesendet wird. Nach dem Verbundserver in der Ressourcenpartnerorganisation Ansprüche als eingehende Ansprüche erhält, wird das anspruchsausstellungsmodul führen Sie eine Reihe von Anspruchsregeln zu filtern, pass-through oder transformieren Sie diese Ansprüche ausgeführt. Die Ansprüche werden dann in ein neues Token erstellt, die an den Webserver in der Ressourcenpartnerorganisation gesendet wird.  
  
Im Web-SSO-Entwurf \ (ein AD FS-Entwurfs in der Organisation nur eine Involved\ ist), ein einzelnen Verbundservers kann verwendet werden, sodass Mitarbeiter melden Sie sich einmal und weiterhin auf mehrere Anwendungen zugreifen können.  
  
