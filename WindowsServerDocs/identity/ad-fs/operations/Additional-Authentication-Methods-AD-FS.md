---
title: Zusätzliche Authentifizierungsmethoden in AD FS-2019
description: Dieses Dokument beschreibt die neuen Authentifizierungsmethoden in AD FS-2019.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b0d5754a4622df9ca26a80bd4e32c355dda0f684
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190063"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>Konfigurieren Sie als primäre Authentifizierung in AD FS-2019 3rd Party-Authentifizierungsanbieter


Organisationen treten Angriffe, die versuchen, Brute-Force-Angriff, gefährden oder andernfalls ausgesperrt Benutzerkonten durch Senden von Anforderungen für Kennwort-basierte Authentifizierung.  Um Unternehmen vor Angriffen zu schützen, wurde eingeführt, AD FS-Funktionen wie "smart" extranetsperre "und" IP-Adressen basierende blockiert.  

Bei diesen Lösungen sind jedoch reaktiv.  Um proaktive die Möglichkeit, reduzieren Sie den Schweregrad der diese Angriffe ab und kann AD FS für Faktoren vor, ohne Kennwort vor dem Erfassen des Kennworts aufgefordert.  

AD FS 2016 eingeführt z. B. Azure MFA als primäre Authentifizierung, sodass OTP-Codes von der Authenticator-App als der erste Faktor verwendet werden können.
Erstellen mit AD FS-2019, können Sie als primäre Authentifizierungsfaktoren externe Authentifizierungsanbieter konfigurieren.

Es gibt zwei wichtige Szenarien, die auf diese Weise können:

## <a name="scenario-1-protect-the-password"></a>Szenario 1: Schützen Sie das Kennwort
Kennwortbasierte Anmeldung vor Brute-Force-Angriffen und Sperrungen fordert zuerst einen zusätzlichen, externe Faktor zu schützen.  Nur, wenn die externe Authentifizierung erfolgreich abgeschlossen wird wird der Benutzer dann aufgefordert, ein Kennwort angezeigt.  Dadurch wird eine einfache Möglichkeit, die Angreifer versucht haben, gefährden oder Konten deaktivieren.

Dieses Szenario besteht aus zwei Komponenten:
- Für Azure MFA oder ein Faktor für die externe Authentifizierung aufgefordert wird, als die primäre Authentifizierung
- Benutzername und Kennwort als zusätzliche Authentifizierung in AD FS

## <a name="scenario-2-password-free"></a>Szenario 2: kennwortfreies!
Kennwörter vollständig entfernen, aber abgeschlossen ist ein sicheres, mehrstufiger Authentifizierung unter Verwendung vollständig ohne Kennwort-basierte Methoden in AD FS
- Azure MFA mit der Authenticator-app
- Windows 10-Hello for Business
- Zertifikatauthentifizierung
- Externe Authentifizierungsanbieter

## <a name="concepts"></a>Konzepte
Was **primäre Authentifizierung** wirklich bedeutet, dass darin, dass es die Methode, die der Benutzer wird aufgefordert, für den ersten, vor dem zusätzliche Faktoren.  Zuvor wurden die nur primären Methoden, die in AD FS verfügbaren Methoden für Active Directory oder Azure MFA oder anderen LDAP-Authentifizierung speichert erstellt.  Externe Methoden können als "zusätzlicher"-Authentifizierung konfiguriert werden, die stattfindet, nachdem die primäre Authentifizierung erfolgreich abgeschlossen wurde.

In AD FS-2019 bedeutet die externe Authentifizierung als die primäre Funktion, um alle externen Authentifizierungsanbietern auf der AD FS-Farm (mithilfe von Register-AdfsAuthenticationProvider) registriert ist für die primäre Authentifizierung als auch "additional" verfügbar machen die Authentifizierung. Sie können die gleiche Weise wie die integrierten Anbieter wie z. B. Formularauthentifizierung und Clientzertifikatauthentifizierung für Intranet bzw. extranet aktiviert werden.

![Authentifizierung](media/Additional-Authentication-Methods-AD-FS/auth1.png)

Nachdem Sie ein externer Anbieter für das extranet, Intranet, aktiviert haben oder für beide wird es für Benutzer verfügbar.  Wenn mehr als eine Methode aktiviert ist, werden Benutzer finden Sie auf eine Seite Ihrer Wahl und in der Lage, wählen Sie eine primäre Methode, wie sie für die zusätzliche Authentifizierung.

## <a name="pre-requisites"></a>Voraussetzungen
Bevor externe Authentifizierungsanbieter als primäre konfiguriert haben, stellen Sie sicher, dass Sie die folgenden Voraussetzungen eingerichtet haben
- AD FS-Farm Verhalten-Ebene (FBL) wurde auf "4" (dieser Wert übersetzt in AD FS-2019) ausgelöst
    - Dies ist der Standardwert für die FBL für neue AD FS-2019 Farmen
    - Für AD FS-Farmen, die basierend auf Windows Server 2012 R2 oder 2016 kann die FBL mit dem PowerShell-Cmdlet Invoke-AdfsFarmBehaviorLevelRaise ausgelöst werden.  Weitere Informationen zum Aktualisieren von einer AD FS-Farm finden Sie unter der Farm, die Artikel für SQL-Farmen oder WID-Farmen aktualisieren 
    - Sie können den FBL-Wert, der mit dem Cmdlet Get-AdfsFarmInformation überprüfen.
- Die AD FS-2019-Farm konfiguriert ist, um den neuen gegenüberliegenden Seiten "paginierten" 2019-Benutzer verwenden
    - Dies ist das Standardverhalten für die neue AD FS-2019 Farmen
    - Für AD FS-Farmen, die von Windows Server 2012 R2 oder 2016 aktualisiert werden die paginierte Datenflüsse automatisch aktiviert, wenn externe Authentifizierung als Primär (das Feature wird in diesem Dokument beschriebenen) aktiviert ist, wie unten beschrieben.

## <a name="enable-external-authentication-methods-as-primary"></a>Externe Authentifizierungsmethoden als primäre aktivieren
Nachdem Sie die Voraussetzungen überprüft haben, gibt es zwei Möglichkeiten zum Konfigurieren zusätzlicher Authentifizierungsanbieter für AD FS als primär:

### <a name="using-powershell"></a>Mithilfe der PowerShell


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


Der AD FS-Dienst muss neu gestartet werden, nach dem Aktivieren oder deaktivieren die zusätzlichen Authentifizierung als Primär.

### <a name="using-the-ad-fs-management-console"></a>Verwenden die AD FS-Verwaltungskonsole
In der AD FS-Verwaltungskonsole unter **Service** -> **Authentifizierungsmethoden**unter **primären Authentifizierungsmethoden**, klicken Sie auf Bearbeiten

Klicken Sie auf das Kontrollkästchen für **können Sie zusätzliche Authentifizierungsanbieter als primäre**.

Der AD FS-Dienst muss neu gestartet werden, nach dem Aktivieren oder deaktivieren die zusätzlichen Authentifizierung als Primär.

## <a name="enable-username-and-password-as-additional-authentication"></a>Benutzername und Kennwort als zusätzliche Authentifizierung aktivieren
Aktivieren Sie zum Abschließen des Szenarios "Schützen Sie das Kennwort" Benutzername und Kennwort als zusätzliche Authentifizierung mithilfe von PowerShell oder die AD FS-Verwaltungskonsole
### <a name="using-powershell"></a>Mithilfe der PowerShell



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>Verwenden die AD FS-Verwaltungskonsole
In der AD FS-Verwaltungskonsole unter **Service** -> **Authentifizierungsmethoden**unter **Additional Authentication Methods**, klicken Sie auf  **Bearbeiten**

Klicken Sie auf das Kontrollkästchen für **Formularauthentifizierung** Benutzername und Kennwort als zusätzliche Authentifizierung zu aktivieren.
