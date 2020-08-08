---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: Bereitstellen von Verbundservern
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: e648f77593f90e976389601d8db5504f6693ce0d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962844"
---
# <a name="deploying-federation-servers"></a>Bereitstellen von Verbundservern

Zum Bereitstellen von Verbund Servern in Active Directory-Verbunddienste (AD FS) AD FS führen Sie \( \) alle Aufgaben in Prüfliste [: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)aus.

> [!NOTE]
> Wenn Sie diese Prüfliste verwenden, empfiehlt es sich, zuerst die Verweise auf die Verbund Server Planung im [AD FS Entwurfs Handbuch in Windows Server 2012](../design/ad-fs-design-guide-in-windows-server-2012.md) zu lesen, bevor Sie mit den Vorgehensweisen zum Konfigurieren der Server beginnen. Wenn Sie die Prüfliste auf diese Weise befolgen, erhalten Sie ein besseres Verständnis des Entwurfs-und Bereitstellungs Prozesses für Verbund Server.

## <a name="about-federation-servers"></a>Informationen zu Verbund Servern
Verbund Server sind Computer, auf denen Windows Server 2008 mit installierter AD FS Software ausgeführt wird, die für die Verbund Server Rolle konfiguriert wurde. Verbund Server authentifizieren oder leiten Anforderungen von Benutzerkonten in anderen Organisationen und von Client Computern weiter, die sich an einer beliebigen Stelle im Internet befinden können.

Wenn Sie die AD FS Software auf einem Computer installieren und mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server für die Verbund Server Rolle konfigurieren, wird dieser Computer zu einem Verbund Server. Außerdem wird das Snap-in "AD FS-Verwaltung" \- auf diesem Computer über das Menü " ** \\ \\ Verwaltung starten** " zur Verfügung gestellt, sodass Sie Folgendes angeben können:

-   Der AD FS Hostname, in dem Partnerorganisationen und Anwendungen Tokenanforderungen und-Antworten senden.

-   Der AD FS Bezeichner, den Partnerorganisationen und Anwendungen verwenden werden, um den eindeutigen Namen oder Speicherort Ihrer Organisation zu identifizieren.

-   Das \- Tokensignaturzertifikat, das alle Verbund Server in einer Serverfarm zum Ausstellen und Signieren von Token verwenden.

-   Der Speicherort der angepassten ASP.NET Webseiten für die Client Anmeldung, die Abmeldung und die Ermittlung von Konto Partnern, die die Client Leistung verbessern.

    > [!NOTE]
    > Die meisten Benutzeroberflächen Einstellungen der Benutzer \( Oberfläche \) sind in der web.config-Datei auf jedem Verbund Server enthalten. Die AD FS Hostnamen und AD FS Bezeichnerwerte sind nicht in der web.config-Datei angegeben.

Verbund Server hosten ein Anspruchs Ausstellungs Modul, das Token basierend auf den Anmelde Informationen ausgibt \( , z. b. Benutzername und Kennwort, \) die ihm angezeigt werden. Ein Sicherheits Token ist eine kryptografisch signierte Dateneinheit, die einen oder mehrere Ansprüche ausdrückt. Ein Anspruch ist eine-Anweisung, die ein Server \( z. b. für einen Client erstellt, z. b. Name, Identität, Schlüssel, Gruppe, Berechtigung oder Funktion \) . Nachdem die Anmelde Informationen \( durch den Benutzer Anmeldevorgang auf dem Verbund Server überprüft \) wurden, werden die Ansprüche für den Benutzer durch die Untersuchung der im angegebenen Attribut Speicher gespeicherten Benutzerattribute gesammelt.

Unter Federated Web Single \- Sign \- on \( SSO \) Entwürfe \( AD FS Entwürfe, in denen zwei oder mehr Organisationen beteiligt sind \) , können Ansprüche mithilfe von Anspruchs Regeln für eine bestimmte vertrauende Seite geändert werden. Die Ansprüche werden in ein Token integriert, das an einen Verbund Server in der Ressourcen Partnerorganisation gesendet wird. Nachdem ein Verbund Server im Ressourcen Partner die Ansprüche als eingehende Ansprüche empfängt, führt er das Anspruchs Ausstellungs Modul aus, um einen Satz von Anspruchs Regeln zum Filtern, weiterleiten oder Transformieren dieser Ansprüche auszuführen. Die Ansprüche werden dann in ein neues Token integriert, das im Ressourcen Partner an den Webserver gesendet wird.

Im Web-SSO-Entwurf entwerfen Sie \( einen AD FS Entwurf, in dem nur eine Organisation beteiligt ist \) , ein einzelner Verbund Server kann verwendet werden, damit sich Mitarbeiter einmalig anmelden und weiterhin auf mehrere Anwendungen zugreifen können.

