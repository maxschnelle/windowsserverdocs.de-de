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

Zum Bereitstellen von Verbund Servern in Active Directory-Verbunddienste (AD FS) \(AD FS\)führen Sie alle Aufgaben in Prüfliste [: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)aus.  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, empfiehlt es sich, zuerst die Verweise auf die Verbund Server Planung im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) zu lesen, bevor Sie mit den Vorgehensweisen zum Konfigurieren der Server beginnen. Wenn Sie die Prüfliste auf diese Weise befolgen, erhalten Sie ein besseres Verständnis des Entwurfs-und Bereitstellungs Prozesses für Verbund Server.  
  
## <a name="about-federation-servers"></a>Informationen zu Verbund Servern  
Verbund Server sind Computer, auf denen Windows Server 2008 mit installierter AD FS Software ausgeführt wird, die für die Verbund Server Rolle konfiguriert wurde. Verbund Server authentifizieren oder leiten Anforderungen von Benutzerkonten in anderen Organisationen und von Client Computern weiter, die sich an einer beliebigen Stelle im Internet befinden können.  
  
Wenn Sie die AD FS Software auf einem Computer installieren und mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server für die Verbund Server Rolle konfigurieren, wird dieser Computer zu einem Verbund Server. Außerdem wird das\-Snap-in "AD FS-Verwaltung" auf diesem Computer im **\\Menü\\Verwaltung starten** verfügbar, damit Sie Folgendes angeben können:  
  
-   Der AD FS Hostname, in dem Partnerorganisationen und Anwendungen Tokenanforderungen und-Antworten senden.  
  
-   Der AD FS Bezeichner, den Partnerorganisationen und Anwendungen verwenden werden, um den eindeutigen Namen oder Speicherort Ihrer Organisation zu identifizieren.  
  
-   Das Token\-Signatur Zertifikats, das alle Verbund Server in einer Serverfarm zum Ausstellen und Signieren von Token verwenden.  
  
-   Der Speicherort der angepassten ASP.NET Webseiten für die Client Anmeldung, die Abmeldung und die Ermittlung von Konto Partnern, die die Client Leistung verbessern.  
  
    > [!NOTE]  
    > Die meisten dieser Kern Benutzeroberflächen-\) Einstellungen der Benutzer \(Oberfläche sind in der Datei "Web. config" auf jedem Verbund Server enthalten. Die AD FS Hostnamen und AD FS Bezeichnerwerte werden in der Datei "Web. config" nicht angegeben.  
  
Verbund Server hosten ein Anspruchs Ausstellungs Modul, das Token basierend auf den Anmelde Informationen ausgibt \(z. b. Benutzername und Kennwort\), die ihm angezeigt werden. Ein Sicherheits Token ist eine kryptografisch signierte Dateneinheit, die einen oder mehrere Ansprüche ausdrückt. Ein Anspruch ist eine-Anweisung, die von einem Server \(z. b. Name, Identität, Schlüssel, Gruppe, Berechtigung oder Funktions\) zu einem Client erstellt wird. Nachdem die Anmelde Informationen auf dem Verbund Server \(über den Benutzer Anmeldeprozess\)überprüft wurden, werden die Ansprüche für den Benutzer durch Untersuchen der Benutzerattribute gesammelt, die im angegebenen Attribut Speicher gespeichert sind.  
  
In Verbund-Web-\-Sign\-on \(SSO\) Entwürfe \(AD FS Entwürfe, in denen zwei oder mehr Organisationen\)sind, können Ansprüche mithilfe von Anspruchs Regeln für eine bestimmte vertrauende Seite geändert werden. Die Ansprüche werden in ein Token integriert, das an einen Verbund Server in der Ressourcen Partnerorganisation gesendet wird. Nachdem ein Verbund Server im Ressourcen Partner die Ansprüche als eingehende Ansprüche empfängt, führt er das Anspruchs Ausstellungs Modul aus, um einen Satz von Anspruchs Regeln zum Filtern, weiterleiten oder Transformieren dieser Ansprüche auszuführen. Die Ansprüche werden dann in ein neues Token integriert, das im Ressourcen Partner an den Webserver gesendet wird.  
  
Im Web-SSO-Entwurf \(ein AD FS Entwurf, in dem nur eine Organisation\)ist, ein einzelner Verbund Server verwendet werden kann, sodass sich Mitarbeiter einmalig anmelden und weiterhin auf mehrere Anwendungen zugreifen können.  
  
