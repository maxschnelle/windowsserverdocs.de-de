---
title: Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern
description: So deaktivieren Sie das Zwischenspeichern von Offlinedateien für einzelne Ordner, die mithilfe der Ordner Umleitung an Netzwerkfreigaben umgeleitet werden.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c2614c0180b32a0215454f2d725d6a962986ef1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394402"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows (halbjährlicher Kanal)

In diesem Thema wird beschrieben, wie Sie das Zwischenspeichern von Offlinedateien in einzelnen Ordnern deaktivieren, die mithilfe der Ordner Umleitung an Netzwerkfreigaben umgeleitet werden. Dies bietet die Möglichkeit, anzugeben, welche Ordner lokal zwischengespeichert werden sollen, wodurch die Offlinedateien Cache Größe und die benötigte Zeit für die Synchronisierung Offlinedateien verringert werden.

>[!NOTE]
>Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Grundlagen zu Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6).

## <a name="prerequisites"></a>Erforderliche Komponenten

Um Offlinedateien Zwischenspeichern bestimmter umgeleiteter Ordner zu deaktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Active Directory Domain Services Domäne (AD DS) mit Client Computern, die der Domäne beigetreten sind. Es gibt keine Anforderungen an die Gesamtstruktur-oder Domänen Funktionsebene oder Schema Anforderungen.
- Client Computer, auf denen Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows (halbjährlicher Kanal) ausgeführt wird.
- Ein Computer, auf dem Gruppenrichtlinie-Verwaltung installiert ist.

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern

Um das Zwischenspeichern bestimmter umgeleiteter Ordner Offlinedateien zu deaktivieren, verwenden Sie Gruppenrichtlinie, um die Richtlinien Einstellung **automatisch bestimmte umgeleitete Ordner offline verfügbar** für das entsprechende Gruppenrichtlinie Objekt (GPO) zu aktivieren. Wenn Sie diese Richtlinien Einstellung auf **deaktiviert** oder **nicht konfiguriert** konfigurieren, werden alle umgeleiteten Ordner offline verfügbar.

>[!NOTE]
>Nur Domänen Administratoren, Organisations Administratoren und Mitglieder der Gruppe "Gruppenrichtlinie Ersteller-Besitzer" können GPOs erstellen.

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>So deaktivieren Sie Offlinedateien für bestimmte umgeleitete Ordner

1. Öffnen Sie **Gruppenrichtlinie-Verwaltung**.
2. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, und wählen Sie dann Gruppenrichtlinien Objekt **in dieser Domäne erstellen aus, um optional ein neues Gruppenrichtlinien Objekt zu erstellen, das angibt, welche Benutzer von der Offline-Offline Schaltung ausgeschlossen werden sollen.** .
3. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf das GPO, für das Sie die Einstellungen für die Ordner Umleitung konfigurieren möchten, und wählen Sie dann **Bearbeiten**aus. Der Gruppenrichtlinienverwaltungs-Editor wird angezeigt.
4. Erweitern Sie in der Konsolen **Struktur unter Benutzerkonfiguration**den Eintrag **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und erweitern Sie **Ordner Umleitung**.
5. Klicken Sie mit der rechten Maustaste auf **nicht automatisch bestimmte umgeleitete Ordner offline verfügbar machen** , und klicken Sie dann auf **Bearbeiten**. Das Fenster **automatisch bestimmte umgeleitete Ordner nicht automatisch verfügbar machen** wird angezeigt.
6. Wählen Sie **Aktiviert** aus. Wählen Sie im Bereich **Optionen** die Ordner aus, die nicht offline verfügbar gemacht werden sollen, indem Sie die entsprechenden Kontrollkästchen aktivieren. Wählen Sie **OK**.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

Das folgende Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion aus wie das unter [Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern](#disabling-offline-files-on-individual-redirected-folders)beschriebenen Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

In diesem Beispiel wird ein neues Gruppenrichtlinien Objekt mit dem Namen *Offlinedateien Einstellungen* in der *mit* -Organisationseinheit in der Domäne *contoso.com* erstellt (der Name des LDAP-Distinguished Name lautet "OU = MyOU, DC = Configuration, DC = com"). Anschließend werden die Offlinedateien für den Ordner "Videos umgeleitet" deaktiviert.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

In der folgenden Tabelle finden Sie eine Liste der Namen der Registrierungsschlüssel (Ordner-GUIDs), die für jeden umgeleiteten Ordner verwendet werden sollen.

|Umgeleiteter Ordner|Registrierungsschlüssel Name (Ordner-GUID)|
|---|---|
|APPDATA (Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|Desktop|B4BFCC3A-DB2C-424C-B029-7FE99A87C641|
|Startmenü|{625B53C3-AB48-4EC1-BA1A-A1EF4146FC19}|
|Dokumente|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|Bilder|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|Musik|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|Videos|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favoriten|{1777F 761-68AD-4D8A-87BD-30B759FA33DD}|
|Kontakte|{56784854-C6CB-462b-8169-88e350 acb882}|
|Downloads|{374DE290-123B-4565-9164-39C4925E467B}|
|Links|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|Suchvorgänge|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|Gespeicherte Spiele|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>Weitere Informationen

- [Übersicht über Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Bereitstellen der Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md)