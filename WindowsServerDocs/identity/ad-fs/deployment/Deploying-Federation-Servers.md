---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1f3b2e1ce901df1df1a232dfba51c292c8e1c29c
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192181"
---
# <a name="deploying-federation-servers"></a>Bereitstellen von Verbundservern

Zum Bereitstellen von Verbundservern in Active Directory Federation Services \(AD FS\), füllen Sie die einzelnen Aufgaben [Prüfliste: Das Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md).  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, es wird empfohlen, die Verweise auf Federation Server-Planung im Vorfeld zu lesen der [AD FS-Entwurfshandbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) bevor Sie die Verfahren zum Konfigurieren der Server beginnen. Befolgen die Checkliste auf diese Weise bietet ein besseres Verständnis des Prozesses Entwurf und Bereitstellung für Verbundserver.  
  
## <a name="about-federation-servers"></a>Informationen zu den Verbundserver  
Verbundserver sind die Computer unter Windows Server 2008 mit der AD FS-Software installiert, die konfiguriert wurden, um auf die Verbundserver-Rolle fungieren. Verbundserver authentifizieren oder Weiterleiten von Anforderungen von Benutzerkonten in anderen Organisationen und von Clientcomputern, die an einer beliebigen Stelle im Internet gefunden werden können.  
  
Die Installation der AD FS-Software auf einem Computer, und verwenden die AD FS Konfigurations-Assistenten für die Einstellung für die Verbundserver-Rolle wird dieser Computer eines Verbundservers. Darüber hinaus wird die AD FS-Verwaltungs-Snap\-in zur Verfügung, auf dem Computer in der **starten\\Verwaltung\\**  Menü, damit Sie die folgenden angeben können:  
  
-   Der AD FS-Hostname, wohin Partnerorganisationen und Anwendungen token-Anforderungen und-Antworten senden wird  
  
-   Der AD FS-Bezeichner, der Zusammenarbeit von Organisationen und Anwendungen verwendet zum Identifizieren von eindeutigen Namen oder Speicherort Ihrer Organisation  
  
-   Das Token\-Signaturzertifikat aus, die allen Verbundservern in einer Serverfarm, die zum Ausstellen und Signieren von Token verwendet werden  
  
-   Der Speicherort der benutzerdefinierten ASP.NET-Webseiten für Client anmelden, Abmelden und zur Ermittlung von Kontopartnern, die die Clientfunktionen voranbringen  
  
    > [!NOTE]  
    > Die meisten dieser core Benutzeroberfläche \(UI\) Einstellungen befinden sich in der Datei web.config auf jedem Verbundserver. Der Hostname des AD FS und AD FS-ID-Werte werden in der Datei "Web.config" nicht angegeben.  
  
Verbundservern wird eine anspruchsausstellungs-Engine, der basierend auf den Anmeldeinformationen Token ausstellt \(z. B. Benutzername und Kennwort\) , die es angezeigt werden. Ein Sicherheitstoken ist eine kryptografisch signierte Dateneinheit, die eine oder mehrere Ansprüche ausdrückt. Ein Anspruch ist eine Anweisung, die zu einem Server macht \(z. B. Name, Identität, Schlüssel, Gruppe, Berechtigung oder Funktion\) zu einem Client. Nachdem die Anmeldeinformationen, auf dem Verbundserver überprüft wurden \(über dem Benutzeranmeldeprozess\), Ansprüche für den Benutzer werden gesammelt, durch die Prüfung der Attribute, die im angegebenen Attribut-Speicher gespeichert sind.  
  
Im Federated Web einzelne\-anmelden\-auf \(SSO\) Entwürfe \(AD FS entwirft, in denen zwei oder mehr Unternehmen beteiligt sind\), Ansprüche durch Anspruchsregeln für eine bestimmte vertrauende Seite geändert werden können die Partei. Die Ansprüche werden in ein Token erstellt, die bei einem Verbundserver in der Ressourcenpartnerorganisation gesendet wird. Nachdem die Ansprüche als eingehende Ansprüche ein Verbundservers beim Ressourcenpartner empfangen hat, führt er die anspruchsausstellungs-Engine zum Ausführen eines Satzes von Anspruchsregeln zu filtern, pass-through oder transformiert diese Ansprüche. Die Ansprüche werden dann in ein neues Token erstellt, die an den Webserver beim Ressourcenpartner gesendet wird.  
  
In der Web-SSO-Entwurf \(eine AD FS-Entwurfs, der in dem nur einer Organisation beteiligt ist\), ein einzelnen Verbundservers kann verwendet werden, sodass Mitarbeiter einmal anmelden und weiterhin auf mehrere Anwendungen zugreifen können.  
  
