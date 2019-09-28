---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 785dcad4ac8e03cc59730fb533e30a001569dd63
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359630"
---
# <a name="deploying-federation-servers"></a>Bereitstellen von Verbundservern

Führen Sie zum Bereitstellen von Verbund Servern in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 alle Aufgaben in [checkliste aus: Einrichten eines Verbund Servers @ no__t-0.  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, empfiehlt es sich, zuerst die Verweise auf die Verbund Server Planung im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) zu lesen, bevor Sie mit den Vorgehensweisen zum Konfigurieren der Server beginnen. Wenn Sie die Prüfliste auf diese Weise befolgen, erhalten Sie ein besseres Verständnis des Entwurfs-und Bereitstellungs Prozesses für Verbund Server.  
  
## <a name="about-federation-servers"></a>Informationen zu Verbund Servern  
Verbund Server sind Computer, auf denen Windows Server 2008 mit installierter AD FS Software ausgeführt wird, die für die Verbund Server Rolle konfiguriert wurde. Verbund Server authentifizieren oder leiten Anforderungen von Benutzerkonten in anderen Organisationen und von Client Computern weiter, die sich an einer beliebigen Stelle im Internet befinden können.  
  
Wenn Sie die AD FS Software auf einem Computer installieren und mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server für die Verbund Server Rolle konfigurieren, wird dieser Computer zu einem Verbund Server. Außerdem wird der AD FS Verwaltungs-Snap @ no__t-0in im Menü **Start @ no__t-2administrative Tools @ no__t-3** auf diesem Computer verfügbar, damit Sie Folgendes angeben können:  
  
-   Der AD FS Hostname, in dem Partnerorganisationen und Anwendungen Tokenanforderungen und-Antworten senden.  
  
-   Der AD FS Bezeichner, den Partnerorganisationen und Anwendungen verwenden werden, um den eindeutigen Namen oder Speicherort Ihrer Organisation zu identifizieren.  
  
-   Das Token @ no__t-0signing Certificate, das alle Verbund Server in einer Serverfarm zum Ausstellen und Signieren von Token verwenden.  
  
-   Der Speicherort der angepassten ASP.NET Webseiten für die Client Anmeldung, die Abmeldung und die Ermittlung von Konto Partnern, die die Client Leistung verbessern.  
  
    > [!NOTE]  
    > Die meisten dieser Kern Benutzeroberflächen \(ui @ no__t-1-Einstellungen sind in der Datei "Web. config" auf jedem Verbund Server enthalten. Die AD FS Hostnamen und AD FS Bezeichnerwerte werden in der Datei "Web. config" nicht angegeben.  
  
Verbund Server hosten ein Anspruchs Ausstellungs Modul, das Tokens basierend auf den Anmelde Informationen ausgibt @no__t z. b. Benutzername und Kennwort @ no__t-1, die diesem angezeigt werden. Ein Sicherheits Token ist eine kryptografisch signierte Dateneinheit, die einen oder mehrere Ansprüche ausdrückt. Ein Anspruch ist eine-Anweisung, die ein Server \(z. b. Name, Identität, Schlüssel, Gruppe, Berechtigung oder Funktion @ no__t-1 über einen Client erstellt. Nachdem die Anmelde Informationen auf dem Verbund Server \(durch den Benutzer Anmeldevorgang @ no__t-1 überprüft wurden, werden Ansprüche für den Benutzer durch Überprüfung der Benutzerattribute gesammelt, die im angegebenen Attribut Speicher gespeichert sind.  
  
In Federated Web Single @ no__t-0sign @ no__t-1On \(sso @ no__t-3 Entwürfe \(AD FS-Entwürfe, in denen mindestens zwei Organisationen an no__t-5 beteiligt sind, können Ansprüche durch Anspruchs Regeln für eine bestimmte vertrauende Seite geändert werden. Die Ansprüche werden in ein Token integriert, das an einen Verbund Server in der Ressourcen Partnerorganisation gesendet wird. Nachdem ein Verbund Server im Ressourcen Partner die Ansprüche als eingehende Ansprüche empfängt, führt er das Anspruchs Ausstellungs Modul aus, um einen Satz von Anspruchs Regeln zum Filtern, weiterleiten oder Transformieren dieser Ansprüche auszuführen. Die Ansprüche werden dann in ein neues Token integriert, das im Ressourcen Partner an den Webserver gesendet wird.  
  
Im Web-SSO-Entwurf \(ein AD FS Entwurf, in dem nur eine Organisation beteiligt ist @ no__t-1, kann ein einzelner Verbund Server verwendet werden, damit sich Mitarbeiter einmalig anmelden und weiterhin auf mehrere Anwendungen zugreifen können.  
  
