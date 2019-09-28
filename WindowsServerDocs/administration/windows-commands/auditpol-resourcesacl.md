---
title: resourcesacl für Auditpol
description: 'Windows-Befehls Thema für **uditpol resourcesacl** : konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs).'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2acffd75298f0f36a9c15e0622816feaae57cb64
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382427"
---
# <a name="auditpol-resourcesacl"></a>resourcesacl für Auditpol



Konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs).

> [!NOTE]
> Gilt nur für Windows 7 und Windows Server 2008 R2.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
auditpol /resourceSACL
[/set /type:<resource> [/success] [/failure] /user:<user> [/access:<access flags>]]
[/remove /type:<resource> /user:<user> [/type:<resource>]]
[/clear [/type:<resource>]]
[/view [/user:<user>] [/type:<resource>]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/Set|Fügt einen neuen Eintrag zu oder aktualisiert einen vorhandenen Eintrag in der Ressourcen-SACL für den angegebenen Ressourcentyp.|
|/remove|Entfernt alle Einträge für den angegebenen Benutzer in der Liste der globalen Objekt Zugriffs Überwachung.|
|/Clear|Entfernt alle Einträge aus der Liste der globalen Objekt Zugriffs Überwachungen.|
|/view|Listet die globalen Objekt Zugriffs Überwachungs Einträge in einer Ressourcen-SACL auf. Die Benutzer-und Ressourcentypen sind optional.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="arguments"></a>Argumente

|Argument|Beschreibung|
|--------|-----------|
|/Type|Die Ressource, für die die Objekt Zugriffs Überwachung konfiguriert wird. Die unterstützten Argument Werte sind File (für Verzeichnisse und Dateien) und Key (für Registrierungsschlüssel).</br>Hinweis: Beim Datei-und Schlüsselwert wird die Groß-/Kleinschreibung beachtet.|
|/Success|Gibt die erfolgreiche Überwachung an.|
|/Failure|Gibt die Fehlerüberwachung an.|
|/User|Gibt einen Benutzer in einer der folgenden Formen an:</br>-DOMAINNAME\ACCOUNT (z. b. Domäne \ Administratoren)</br>-Standaloneserver\gruppenkonto (siehe [LookupAccountName-Funktion](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx))</br>-{S-1-x-x-x-x} (x wird als Dezimal ausgedrückt, und die gesamte sid muss in geschweifte Klammern eingeschlossen sein); Beispiel: {S-1-5-21-5624481-130208933-164394174-1001}</br>    Hinweis:     Wenn das sid-Formular verwendet wird, wird keine Überprüfung durchgeführt, um zu überprüfen, ob dieses Konto vorhanden ist.|
|/access|Gibt eine Berechtigungs Maske an, die in einer von zwei Formen angegeben werden kann:</br>-Eine Sequenz von einfachen rechten:</br>    -Generische Zugriffsrechte:</br>        -GA-GENERISCH ALLE</br>        -GR-GENERISCHER LESEVORGANG</br>        -GW-GENERISCHER SCHREIBVORGANG</br>        -GX-GENERISCHES AUSFÜHREN</br>    -Zugriffsrechte für Dateien:</br>        -FA-DATEIZUGRIFF</br>        -FR-GENERISCHER DATEI LESEVORGANG</br>        -FW-DATEI GENERISCHER SCHREIBVORGANG</br>        -FX-DATEI GENERISCH AUSFÜHREN</br>    -Zugriffsrechte für Registrierungsschlüssel:</br>        -KA-SCHLÜSSEL ZUGRIFF</br>        -KR-SCHLÜSSEL LESEVORGANG</br>        -KWH-SCHLÜSSEL SCHREIBVORGANG</br>        -KX-SCHLÜSSEL AUSFÜHREN</br>    Beispiel: "/Access: frfw" aktiviert Überwachungs Ereignisse für Lese-und Schreibvorgänge.</br>-Ein Hexadezimalwert, der die Zugriffs Maske darstellt (z. b. 0x1200a9).</br>    Dies ist nützlich, wenn Ressourcen spezifische Bitmasken verwendet werden, die nicht Teil des SDDL (Security Deskriptor Definition Language)-Standards sind. Wenn der Wert nicht weggelassen wird, wird Vollzugriff verwendet.|

## <a name="remarks"></a>Hinweise

Bei resourcesacl-Vorgängen müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch resourcesacl-Vorgänge durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen des Entfernungs Vorgangs nicht erforderlich ist.

## <a name="BKMK_Examples"></a>Beispiele

So legen Sie eine globale Ressourcen-SACL fest, um erfolgreiche Zugriffsversuche eines Benutzers für einen Registrierungsschlüssel zu überwachen:
```
auditpol /resourceSACL /set /type:Key /user:MYDOMAIN\myuser /success
```
So legen Sie eine globale Ressourcen-SACL zum Überwachen erfolgreicher und fehlgeschlagener Versuche durch einen Benutzer zum Ausführen allgemeiner Lese-und Schreibfunktionen für Dateien oder Ordner fest:
```
auditpol /resourceSACL /set /type:File /user:MYDOMAIN\myuser /success /failure /access:FRFW
```
So entfernen Sie alle globalen Ressourcen-SACL-Einträge für Dateien oder Ordner:
```
auditpol /resourceSACL /type:File /clear
```
So entfernen Sie alle globalen Ressourcen-SACL-Einträge für einen bestimmten Benutzer aus Dateien oder Ordnern:
```
auditpol /resourceSACL /remove /type:File /user:{S-1-5-21-56248481-1302087933-1644394174-1001}
```
Auflisten der in Dateien oder Ordnern festgelegten globalen Einträge für die Objekt Zugriffs Überwachung:
```
auditpol /resourceSACL /type:File /view
```
So Listen Sie die Einträge für die globale Objekt Zugriffs Überwachung für einen bestimmten Benutzer auf, der für Dateien oder Ordner festgelegt ist:
```
auditpol /resourceSACL /type:File /view /user:MYDOMAIN\myuser
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)