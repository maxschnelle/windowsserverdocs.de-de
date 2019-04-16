---
title: Offlinedateien für einzelne umgeleitete Ordner deaktivieren
description: So deaktivieren Sie Offlinedateien für einzelne Ordner, die in Netzwerkfreigaben umgeleitet wurden, mit der Ordnerumleitung Zwischenspeichern.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc93906cb7ff958fc1db7b00abdc557623e764e
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339308"
---
# Offlinedateien für einzelne umgeleitete Ordner deaktivieren

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

In diesem Thema wird beschrieben, wie Offlinedateien Zwischenspeichern für einzelne Ordner, die in Netzwerkfreigaben umgeleitet wurden, mit der Ordnerumleitung deaktivieren. Dies bietet die Möglichkeit zum angeben, welche Ordner ausgeschlossen werden lokal zwischenzuspeichern, Reduzierung des Caches für Offlinedateien Größe und Zeit erforderlich, um Offlinedateien zu synchronisieren.

>[!NOTE]
>Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, die Sie verwenden können, um einige der beschriebenen Verfahren zu automatisieren. Weitere Informationen finden Sie unter [Windows PowerShell-Grundlagen](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6).

## Voraussetzungen

Um Offlinedateien Zwischenspeichern von bestimmten umgeleitete Ordner zu deaktivieren, muss Ihre Umgebung folgende Voraussetzungen erfüllen.

- Einer Domäne Active Directory Domain Services (AD DS) mit Clientcomputern mit der Domäne verbunden. Es gibt keine Gesamtstruktur oder Domäne Funktionsebene Anforderungen oder Schema-Anforderungen.
- Clientcomputer, die unter Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.
- Ein Computer mit Gruppenrichtlinien-Verwaltungskonsole installiert.

## Deaktivieren von Offlinedateien auf einzelne umgeleitete Ordner

Um Offlinedateien Zwischenspeichern von bestimmten umgeleitete Ordner zu deaktivieren, verwenden Sie Gruppenrichtlinien zum Aktivieren **bestimmter umgeleitete Ordner nicht automatisch offline stellen** Einstellung der Richtlinie für das entsprechende Gruppenrichtlinienobjekt (GPO). Konfigurieren diese Einstellung **deaktiviert** oder **Nicht konfiguriert** stellt alle umgeleitete Ordner zur Verfügung offline.

>[!NOTE]
>Nur Domänen-Admins, Organisations-Admins und Mitglieder der Gruppenrichtlinie Ersteller Besitzer können Gruppenrichtlinienobjekte erstellen.

### So deaktivieren Sie Offlinedateien auf bestimmte umgeleitete Ordner

1. Öffnen Sie **die Gruppenrichtlinien-Verwaltungskonsole**.
2. Um ein neues GPO optional zu erstellen, die angibt, welche Benutzer Ordner offline verfügbar gemacht wird ausgeschlossen umgeleitet haben soll, mit der rechten Maustaste der entsprechenden Domäne oder Organisationseinheit (OE) und wählen Sie **Erstellen eines Gruppenrichtlinienobjekts in dieser Domäne, und verknüpfen Sie es hier **.
3. In der Konsolenstruktur mit der rechten Maustaste im GPOs, für die Sie konfigurieren Sie die Ordnerumleitung-Einstellungen, und wählen Sie dann **Bearbeiten**möchten. Die Gruppenrichtlinienverwaltungs-Editor angezeigt wird.
4. In der Konsolenstruktur unter **Benutzerkonfiguration**erweitern Sie **Richtlinien**, erweitern Sie **Administrative Vorlagen**, erweitern Sie **System**und **Ordnerumleitung**.
5. Mit der rechten Maustaste **bestimmte umgeleitete Ordner nicht automatisch offline machen** , und wählen Sie dann **Bearbeiten**. Das **bestimmte umgeleitete Ordner nicht automatisch offline stellen** Fenster erscheint.
6. Wählen Sie **Aktiviert** aus. Wählen Sie im **Bereich** die Ordner, die nicht offline verfügbar gemacht werden sollten durch die Auswahl der entsprechenden Kontrollkästchen. Wählen Sie **OK** aus.

### Entsprechende Windows PowerShell-Befehle

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie unter [Deaktivieren Offlinedateien für einzelne umgeleitete Ordner](#disabling-offline-files-on-individual-redirected-folders)beschrieben. Geben Sie jedes Cmdlet in einer einzelnen Zeile, obwohl sie über mehrere Zeilen umgebrochen erscheint aufgrund der Formatierung von Einschränkungen.

Dieses Beispiel erstellt ein neues Gruppenrichtlinienobjekt namens *Offline-Einstellungen* in der *MyOu* Organisationseinheit in der Domäne *"contoso.com"* (LDAP-distinguished Name ist "Ou = MyOU, dc = Contoso, dc = com"). Es wird dann Offlinedateien für den Ordner "Videos umgeleitet" deaktiviert.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

Finden Sie unter der folgenden Tabelle finden Sie eine Liste der Namen von Registrierungsschlüsseln (Ordner GUIDs) für jeden umgeleitete Ordner verwenden.

|Umgeleitete Ordner|Name des Registrierungsschlüssels (Ordner GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|Desktop|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|Menü "Start"|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|Dokumente|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|Bilder|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|Musik|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|Videos|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favorites|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|Kontakte|{56784854-C6CB-462b-8169-88E350ACB882}|
|Downloads|{374DE290-123F-4565-9164-39C4925E467B}|
|Links|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|Suchvorgänge|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|Gespeicherte Spiele|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## Weitere Informationen

- [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)