---
title: resourcesacl für Auditpol
description: Referenz Artikel für den Befehl Auditpol resourcesacl, der globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs) konfiguriert.
ms.topic: reference
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 26353e339329553a977809310d3a93e95076dfdb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633168"
---
# <a name="auditpol-resourcesacl"></a>resourcesacl für Auditpol

> Gilt für: Windows 7 und Windows Server 2008 R2

Konfiguriert globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs).

Zum Durchführen von *resourcesacl* -Vorgängen müssen Sie über **Schreib** -oder **voll** Zugriff-Berechtigungen für das Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch *resourcesacl* -Vorgänge durchführen, wenn Sie über das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) verfügen.

## <a name="syntax"></a>Syntax

```
auditpol /resourceSACL
[/set /type:<resource> [/success] [/failure] /user:<user> [/access:<access flags>]]
[/remove /type:<resource> /user:<user> [/type:<resource>]]
[/clear [/type:<resource>]]
[/view [/user:<user>] [/type:<resource>]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /Set | Fügt einen neuen Eintrag zu oder aktualisiert einen vorhandenen Eintrag in der Ressourcen-SACL für den angegebenen Ressourcentyp. |
| /remove | Entfernt alle Einträge für den angegebenen Benutzer in der Liste der globalen Objekt Zugriffs Überwachung. |
| /Clear | Entfernt alle Einträge aus der Liste der globalen Objekt Zugriffs Überwachungen.|
| /view | Listet die globalen Objekt Zugriffs Überwachungs Einträge in einer Ressourcen-SACL auf. Die Benutzer-und Ressourcentypen sind optional. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="arguments"></a>Argumente

| Argument | BESCHREIBUNG |
| -------- | ----------- |
| /type | Die Ressource, für die die Objekt Zugriffs Überwachung konfiguriert wird. Die unterstützten, Unterscheidung nach Groß-/Kleinschreibung, Argument Werte sind *File* (für Verzeichnisse und Dateien) und *Key* (für Registrierungsschlüssel). |
| /Success | Gibt die erfolgreiche Überwachung an. |
| /Failure | Gibt die Fehlerüberwachung an. |
| /User | Gibt einen Benutzer in einer der folgenden Formen an:<ul><li> DOMAINNAME\ACCOUNT (z. b. Domänen Name \ Administratoren)</li><li>Standaloneserver\group-Konto (siehe [LookupAccountName-Funktion](/windows/win32/api/winbase/nf-winbase-lookupaccountnamea))</li><li>{S-1-x-x-x-x} (x wird als Dezimal ausgedrückt, und die gesamte sid muss in geschweifte Klammern eingeschlossen werden.) Beispiel: {S-1-5-21-5624481-130208933-164394174-1001}<p>**Hinweis:** Wenn das sid-Formular verwendet wird, wird keine Überprüfung durchgeführt, um zu überprüfen, ob dieses Konto vorhanden ist.</li></ul> |
| /access | Gibt eine Berechtigungs Maske an, die durch angegeben werden kann:<p>Allgemeine Zugriffsrechte, einschließlich:<ul><li>Allgemeine allgemeine Verfügbarkeit</li><li>Gr-generischer Lesevorgang</li><li>GW-generischer Schreibvorgang</li><li>GX-generisches ausführen</li></ul><p>Zugriffsrechte für Dateien, einschließlich:<ul><li>FA-Dateizugriff</li><li>allgemeiner Lesezugriff auf die FR-Datei</li><li>FW-Datei generischer Schreibvorgang</li><li>FX-Datei (generisch) ausführen</li></ul><p>Zugriffsrechte für Registrierungsschlüssel, einschließlich:<ul><li>Zugriffsschlüssel für alle Zugriffsrechte</li><li>KR-Schlüssel Lesevorgang</li><li>kW-Schlüssel Schreibvorgänge</li><li>Kx-Schlüssel ausführen</li></ul><p>Beispiel: `/access:FRFW` aktiviert Überwachungs Ereignisse für Lese-und Schreibvorgänge.<p>Ein Hexadezimalwert, der die Zugriffs Maske darstellt (z. b. 0x1200a9).<p>Dies ist nützlich, wenn Ressourcen spezifische Bitmasken verwendet werden, die nicht Teil des SDDL (Security Deskriptor Definition Language)-Standards sind. Wenn der Wert nicht weggelassen wird, wird Vollzugriff verwendet. |

## <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Auditpol-Befehle](auditpol.md)
