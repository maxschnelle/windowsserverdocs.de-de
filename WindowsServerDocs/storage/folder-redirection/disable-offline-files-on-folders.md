---
title: Offlinedateien auf einzelne umgeleiteten Ordnern deaktivieren
description: So deaktivieren Sie die Offlinedateien-caching in den einzelnen Ordnern, die mithilfe der Ordnerumleitung Netzwerkfreigaben umgeleitet werden.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc93906cb7ff958fc1db7b00abdc557623e764e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834201"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>Offlinedateien auf einzelne umgeleiteten Ordnern deaktivieren

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

In diesem Thema wird beschrieben, wie Dateien in den einzelnen Ordnern, die auf Netzwerkfreigaben umgeleitet werden, mithilfe der Ordnerumleitung Zwischenspeicherung deaktivieren, wird. Dies bietet die Möglichkeit, die angeben, welche Ordner ausschließen, lokal zwischenspeichern, muss reduzieren Zwischenspeicher für Offlinedateien Größe und Synchronisieren von Offlinedateien.

>[!NOTE]
>Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Grundlagen von Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6).

## <a name="prerequisites"></a>Vorraussetzungen

Um Offlinedateien Zwischenspeichern bestimmter umgeleiteten Ordner zu deaktivieren, muss Ihre Umgebung die folgenden Voraussetzungen erfüllen.

- Eine Domäne der Active Directory Domain Services (AD DS) mit Clientcomputern, die in die Domäne eingebunden. Es gibt keine Anforderungen von Gesamtstruktur oder Domäne auf Funktionsebene oder schemaanforderungen.
- Client-Computer unter Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.
- Ein Computer mit die Gruppenrichtlinien-Verwaltungskonsole installiert.

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>Offlinedateien auf einzelne umgeleiteten Ordnern deaktivieren

Um Offlinedateien Zwischenspeichern bestimmter umgeleiteten Ordner zu deaktivieren, mithilfe von Gruppenrichtlinien zum Aktivieren der **werden nicht automatisch bestimmte umgeleiteten Ordner offline verfügbar machen** richtlinieneinstellung für die entsprechende Gruppe Gruppenrichtlinienobjekt (GPO). Konfigurieren diese richtlinieneinstellung **deaktiviert** oder **nicht konfiguriert** alle umgeleiteten Ordner offline verfügbar macht.

>[!NOTE]
>Nur Domänenadministratoren, Organisationsadministratoren und Mitglieder der Gruppe der Gruppenrichtlinie Ersteller-Besitzer können Gruppenrichtlinienobjekte erstellen.

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>So deaktivieren Sie Offlinedateien auf bestimmte umgeleiteten Ordner

1. Open **Gruppenrichtlinienverwaltung**.
2. Um optional ein neues Gruppenrichtlinienobjekt zu erstellen, der angibt, welche Benutzer offline verfügbar gemacht werden ausgeschlossenen Ordner umgeleitet haben soll, mit der rechten Maustaste der entsprechenden Domäne oder Organisationseinheit (OU), und wählen Sie dann **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und verknüpfen Hier IT**.
3. In der Konsolenstruktur mit der Maustaste des GPOs für die Sie konfigurieren die Einstellungen für die Umleitung des Ordners ein, und wählen Sie dann **bearbeiten**. Der Gruppenrichtlinienverwaltungs-Editor wird angezeigt.
4. In der Konsolenstruktur unter **Benutzerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**, und Erweitern Sie **Ordnerumleitung**.
5. Mit der rechten Maustaste **werden nicht automatisch bestimmte umgeleiteten Ordner offline verfügbar machen** und wählen Sie dann **bearbeiten**. Die **werden nicht automatisch bestimmte umgeleiteten Ordner offline verfügbar machen** Fenster wird angezeigt.
6. Wählen Sie **Aktiviert** aus. In der **Optionen** wählen Sie die Ordner, die nicht offline verfügbar gemacht werden sollten dazu die entsprechenden Kontrollkästchen im Bereich. Wählen Sie **OK**.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie in die Prozedur beschrieben [Deaktivieren von Offlinedateien für einzelne umgeleiteten Ordner](#disabling-offline-files-on-individual-redirected-folders). Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

In diesem Beispiel erstellt ein neues Gruppenrichtlinienobjekt namens *Dateien Offlineeinstellungen* in die *MyOu* Organisationseinheit in der *"contoso.com"* Domäne (der LDAP-distinguished Name ist "Ou = MyOU, dc = Contoso, dc = com "). Klicken Sie dann deaktiviert sie Offlinedateien für der Ordner Videos umgeleitet.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

Finden Sie die folgende Tabelle enthält eine Liste der Namen von Registrierungsschlüsseln (Ordner-GUIDs) für jeden umgeleiteten Ordner verwenden.

|Umgeleitete Ordner|Name des Registrierungsschlüssels (Ordner "GUID")|
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

- [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)