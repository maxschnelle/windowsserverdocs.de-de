---
title: Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern
description: Deaktivieren der Zwischenspeicherung von Offlinedateien für einzelne Ordner, die mithilfe von Ordnerumleitung an Netzwerkfreigaben umgeleitet werden.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0219c669a52d961cc98d6b0ee16bcbcfbbb78417
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961572"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>Deaktivieren von Offlinedateien in einzelnen umgeleiteten Ordnern

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows (halbjährlicher Kanal)

In diesem Thema wird beschrieben, wie die Zwischenspeicherung von Offlinedateien für einzelne Ordner deaktiviert wird, die mithilfe von Ordnerumleitung an Netzwerkfreigaben umgeleitet werden. Dies bietet die Möglichkeit, anzugeben, welche Ordner lokal zwischengespeichert werden sollen, wodurch die Cachegröße der Offlinedateien und die für die Synchronisierung von Offlinedateien benötigte Zeit verringert werden.

>[!NOTE]
>Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Grundlagen von Windows PowerShell](/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6).

## <a name="prerequisites"></a>Voraussetzungen

Um die Zwischenspeicherung von Offlinedateien bestimmter umgeleiteter Ordner zu deaktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Active Directory Domain Services-Domäne (AD DS) mit Clientcomputern, die der Domäne beigetreten sind. Es gibt keine Anforderungen an die Gesamtstruktur- oder Domänenfunktionsebene oder Schemaanforderungen.
- Clientcomputer, die Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows (halbjährlicher Kanal) ausführen.
- Ein Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>Deaktivieren von Offlinedateien für einzelne umgeleitete Ordner

Um die Zwischenspeicherung von Offlinedateien für bestimmte umgeleitete Ordner zu deaktivieren, verwenden Sie die Gruppenrichtlinie, um die Richtlinieneinstellung **Bestimmte umgeleitete Ordner nicht automatisch offline verfügbar machen** für das entsprechende Gruppenrichtlinienobjekt. Wenn diese Richtlinieneinstellung auf **Deaktiviert** oder **Nicht konfiguriert**  festgelegt wird, werden alle umgeleiteten Ordner offline verfügbar.

>[!NOTE]
>Nur Domänenadministratoren, Organisationsadministratoren und Mitglieder der Gruppe „Ersteller/Besitzer“ der Gruppenrichtlinie können Gruppenrichtlinienobjekte erstellen.

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>So deaktivieren Sie Offlinedateien für bestimmte umgeleitete Ordner

1. Öffnen Sie **Gruppenrichtlinienverwaltung**.
2. Um optional ein neues Gruppenrichtlinienobjekt zu erstellen, das angibt, welche Benutzer von der Offlineverfügbarkeit ausgeschlossene umgeleitete Ordner haben sollen, klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit (OU), und wählen Sie dann **Gruppenrichtlinienobjekt in dieser Domäne erstellen und es hier verknüpfen** aus.
3. Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, für das Sie die Ordnerumleitungseinstellungen konfigurieren möchten, und wählen Sie dann **Bearbeiten** aus. Der Gruppenrichtlinienverwaltungs-Editor wird geöffnet.
4. Erweitern Sie in der Konsolenstruktur unter **Benutzerkonfiguration** die Optionen **Richtlinien**, **Verwaltungsvorlagen**, **System** und **Ordnerumleitung**.
5. Klicken Sie mit der rechten Maustaste auf **Bestimmte umgeleitete Ordner nicht automatisch offline verfügbar machen**, und wählen Sie dann **Bearbeiten** aus. Das Fenster **Bestimmte umgeleitete Ordner nicht automatisch offline verfügbar machen** wird geöffnet.
6. Wählen Sie **Aktiviert**aus. Wählen Sie im Bereich **Optionen** die Ordner aus, die nicht offline verfügbar gemacht werden sollen, indem Sie die entsprechenden Kontrollkästchen aktivieren. Wählen Sie **OK** aus.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion aus wie das unter [Deaktivieren von Offlinedateien für einzelne umgeleitete Ordner](#disabling-offline-files-on-individual-redirected-folders) beschriebene Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

In diesem Beispiel wird ein neues Gruppenrichtlinienobjekt mit dem Namen *Offline File Settings* in der Organisationseinheit *MyOu* in der Domäne *contoso.com* erstellt (der LDAP-DN lautet „ou=MyOU,dc=contoso,dc=com“). Anschließend werden Offlinedateien für den umgeleiteten Ordner „Videos“ deaktiviert.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

In der folgenden Tabelle finden Sie eine Liste der Namen der Registrierungsschlüssel (Ordner-GUIDs), die für jeden umgeleiteten Ordner verwendet werden.

|Umgeleiteter Ordner|Name des Registrierungsschlüssels (Ordner-GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|Desktop|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|Startmenü|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|Dokumente|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|Bilder|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|Musik|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|Videos|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favoriten|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|Kontakte|{56784854-C6CB-462b-8169-88E350ACB882}|
|Downloads|{374DE290-123F-4565-9164-39C4925E467B}|
|Links|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|Suchvorgänge|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|Gespeicherte Spiele|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>Weitere Informationen

- [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht](folder-redirection-rup-overview.md)
- [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md)
