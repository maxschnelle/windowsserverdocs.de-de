---
title: Zusätzliche Authentifizierungsmethoden in AD FS 2019
description: In diesem Dokument werden die neuen Authentifizierungsmethoden in AD FS 2019 beschrieben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8a53a4cfca4f34459102b8edc8e6af82f36be70d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358370"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>Konfigurieren von Drittanbieter-Authentifizierungs Anbietern als primäre Authentifizierung in AD FS 2019


Organisationen stoßen auf Angriffe, bei denen versucht wird, Benutzerkonten durch das Senden von Kenn Wort basierten Authentifizierungsanforderungen auf Brute-Force-, kompromittierten oder anderweitig auszusperren.  Um Organisationen vor Gefährdung zu schützen, hat AD FS Funktionen wie die "intelligente" Sperre für das Extranet und die auf IP-Adressen basierende Blockierung eingeführt.  

Diese entschärfungen sind jedoch reaktiv.  Um auf proaktive Weise den Schweregrad dieser Angriffe zu reduzieren, ist AD FS in der Lage, vor dem Erfassen des Kennworts vor dem Erfassen des Kennworts zur Eingabe von nicht Kenn Wort Faktoren aufzufordern.  

Beispielsweise wurde in AD FS 2016 Azure MFA als primäre Authentifizierung eingeführt, damit OTP-Codes aus der Authenticator-App als erster Faktor verwendet werden können.
Mit AD FS 2019 können Sie externe Authentifizierungs Anbieter als primäre Authentifizierungsfaktoren konfigurieren.

Es gibt zwei wichtige Szenarien, die dies ermöglichen:

## <a name="scenario-1-protect-the-password"></a>Szenario 1: Schützen des Kennworts
Schützen Sie die Kenn Wort basierte Anmeldung vor Brute-Force-Angriffen und-sperren, indem Sie zuerst einen zusätzlichen, externen Faktor anfordern.  Nur wenn die externe Authentifizierung erfolgreich abgeschlossen wurde, wird dem Benutzer eine Kenn Wort Eingabeaufforderung angezeigt.  Dadurch wird verhindert, dass Angreifer versuchen, Konten zu kompromittieren oder zu deaktivieren.

Dieses Szenario besteht aus zwei Komponenten:
- Eingabeaufforderung für Azure MFA oder einen externen Authentifizierungs Faktor als primäre Authentifizierung
- Benutzername und Kennwort als zusätzliche Authentifizierung in AD FS

## <a name="scenario-2-password-free"></a>Szenario 2: Kennwort kostenlos!
Kenn Wörter vollständig ausschließen, aber eine starke Multi-Factor Authentication mit vollständig nicht Kenn Wort basierten Methoden in AD FS
- Azure MFA mit Authenticator-App
- Windows 10 Hello for Business
- Zertifikatauthentifizierung
- Externe Authentifizierungs Anbieter

## <a name="concepts"></a>Konzepte
Die **primäre Authentifizierung** bedeutet, dass es sich um die Methode handelt, nach der der Benutzer vor weiteren Faktoren zur Eingabe aufgefordert wird.  Zuvor waren die einzigen primären Methoden, die in AD FS verfügbar waren, in Methoden für Active Directory oder Azure MFA oder andere LDAP-Authentifizierungs Speicher integriert.  Externe Methoden können als "zusätzliche" Authentifizierung konfiguriert werden, die nach erfolgreichem Abschluss der primären Authentifizierung erfolgt.

In AD FS 2019 bedeutet die externe Authentifizierung als primäre Funktion, dass alle externen Authentifizierungs Anbieter, die in der AD FS Farm registriert sind (mithilfe von Register-adfsauthenticationprovider), für die primäre Authentifizierung und "Weitere" verfügbar sind. Genehmigung. Sie können auf die gleiche Weise wie die integrierten Anbieter wie Formular Authentifizierung und Zertifikat Authentifizierung für die Intranet-und/oder Extranetverwendung aktiviert werden.

![Authentifizierung](media/Additional-Authentication-Methods-AD-FS/auth1.png)

Sobald ein externer Anbieter für das Extranet, das Intranet oder beides aktiviert ist, kann er von Benutzern verwendet werden.  Wenn mehr als eine Methode aktiviert ist, wird Benutzern eine Auswahl Seite angezeigt, und Sie können eine primäre Methode auswählen, genauso wie bei der zusätzlichen Authentifizierung.

## <a name="pre-requisites"></a>Voraussetzungen
Bevor Sie externe Authentifizierungs Anbieter als primär konfigurieren, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
- Die AD FS-Farm Verhaltensebene (FBL) wurde auf ' 4 ' (dieser Wert wird in AD FS 2019 übersetzt).
    - Dies ist der standardmäßige Standardwert für den Standardwert für die AD FS 2019-Farmen.
    - Bei AD FS Farmen, die auf Windows Server 2012 R2 oder 2016 basieren, kann der FBL mithilfe des PowerShell-Commandlets "aufrufen-adfsfarmverhalorlevelraise" ausgelöst werden.  Weitere Informationen zum Aktualisieren einer AD FS-Farm finden Sie im Artikel Farm Upgrade für SQL-Farmen oder WID-Farmen. 
    - Sie können den FBL-Wert mithilfe des Cmdlets Get-adfsfarminformation überprüfen.
- Die AD FS 2019-Farm ist so konfiguriert, dass Sie die neuen Seiten mit der Seite "paginierte" von 2019 verwendet.
    - Dies ist das Standardverhalten für neue AD FS 2019-Farmen.
    - Bei AD FS Farmen, die von Windows Server 2012 R2 oder 2016 aktualisiert wurden, werden die paginierten Flows automatisch aktiviert, wenn die externe Authentifizierung als Primär (das in diesem Dokument beschriebene Feature) wie unten beschrieben aktiviert ist.

## <a name="enable-external-authentication-methods-as-primary"></a>Externe Authentifizierungsmethoden als primär aktivieren
Nachdem Sie die Voraussetzungen überprüft haben, gibt es zwei Möglichkeiten, um AD FS zusätzlichen Authentifizierungs Anbietern als primär zu konfigurieren:

### <a name="using-powershell"></a>Mithilfe der PowerShell


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


Der AD FS-Dienst muss nach dem Aktivieren oder Deaktivieren der zusätzlichen Authentifizierung als primär neu gestartet werden.

### <a name="using-the-ad-fs-management-console"></a>Verwenden der AD FS-Verwaltungskonsole
Klicken Sie in der AD FS-Verwaltungskonsole unter **Dienst** -> **Authentifizierungsmethoden**unter **primäre Authentifizierungsmethoden**auf Bearbeiten.

Aktivieren Sie das Kontrollkästchen **zusätzliche Authentifizierungs Anbieter als Primäranbieter zulassen**.

Der AD FS-Dienst muss nach dem Aktivieren oder Deaktivieren der zusätzlichen Authentifizierung als primär neu gestartet werden.

## <a name="enable-username-and-password-as-additional-authentication"></a>Benutzernamen und Kennwort als zusätzliche Authentifizierung aktivieren
Aktivieren Sie den Benutzernamen und das Kennwort mithilfe von PowerShell oder der AD FS Management Console als zusätzliche Authentifizierung, um das Szenario "Schützen des Kennworts" abzuschließen.
### <a name="using-powershell"></a>Mithilfe der PowerShell



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>Verwenden der AD FS-Verwaltungskonsole
Klicken Sie in der AD FS-Verwaltungskonsole unter " **Dienst** -> **Authentifizierungsmethoden**" unter **zusätzliche Authentifizierungsmethoden**auf **Bearbeiten** .

Aktivieren Sie das Kontrollkästchen für die **Formular Authentifizierung** , um Benutzername und Kennwort als zusätzliche Authentifizierung zu aktivieren.
