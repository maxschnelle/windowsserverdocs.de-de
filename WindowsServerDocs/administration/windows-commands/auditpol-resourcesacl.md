---
title: resourcesacl für Auditpol
description: Windows-Befehls Thema für **Auditpol resourcesacl**, das globale Ressourcensystem-Zugriffs Steuerungs Listen (SACLs) konfiguriert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b004be6f21cd076fe20e73c45268731c35d654e5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851153"
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

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /set | Fügt einen neuen Eintrag zu oder aktualisiert einen vorhandenen Eintrag in der Ressourcen-SACL für den angegebenen Ressourcentyp. |
| /remove | Entfernt alle Einträge für den angegebenen Benutzer in der Liste der globalen Objekt Zugriffs Überwachung. |
| /Clear | Entfernt alle Einträge aus der Liste der globalen Objekt Zugriffs Überwachungen.|
| /view | Listet die globalen Objekt Zugriffs Überwachungs Einträge in einer Ressourcen-SACL auf. Die Benutzer-und Ressourcentypen sind optional. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="arguments"></a>Argumente

| Argument | Beschreibung |
| -------- | ----------- | 
| /type | Die Ressource, für die die Objekt Zugriffs Überwachung konfiguriert wird. Die unterstützten, Unterscheidung nach Groß-/Kleinschreibung, Argument Werte sind File (für Verzeichnisse und Dateien) und Key (für Registrierungsschlüssel). |
| /Success | Gibt die erfolgreiche Überwachung an. |
| /Failure | Gibt die Fehlerüberwachung an. |
| /User | Gibt einen Benutzer in einer der folgenden Formen an:<ul><li> DOMAINNAME\ACCOUNT (z. b. Domänen Name \ Administratoren)</li><li>Standaloneserver\group-Konto (siehe [LookupAccountName-Funktion](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx))</li><li>{S-1-x-x-x-x} (x wird als Dezimal ausgedrückt, und die gesamte sid muss in geschweifte Klammern eingeschlossen werden.) Beispiel: {S-1-5-21-5624481-130208933-164394174-1001}<p>**Hinweis:** Wenn das sid-Formular verwendet wird, wird keine Überprüfung durchgeführt, um zu überprüfen, ob dieses Konto vorhanden ist.</li></ul> |
| /access | Gibt eine Berechtigungs Maske an, die durch angegeben werden kann:<p>Allgemeine Zugriffsrechte, einschließlich:<ul><li>Allgemeine allgemeine Verfügbarkeit</li><li>Gr-generischer Lesevorgang</li><li>GW-generischer Schreibvorgang</li><li>GX-generisches ausführen</li></ul><p>Zugriffsrechte für Dateien, einschließlich:<ul><li>FA-Dateizugriff</li><li>allgemeiner Lesezugriff auf die FR-Datei</li><li>FW-Datei generischer Schreibvorgang</li><li>FX-Datei (generisch) ausführen</li></ul><p>Zugriffsrechte für Registrierungsschlüssel, einschließlich:<ul><li>Zugriffsschlüssel für alle Zugriffsrechte</li><li>KR-Schlüssel Lesevorgang</li><li>kW-Schlüssel Schreibvorgänge</li><li>Kx-Schlüssel ausführen</li></ul><p>Beispiel: `/access:FRFW` aktiviert Überwachungs Ereignisse für Lese-und Schreibvorgänge.<p>Ein Hexadezimalwert, der die Zugriffs Maske darstellt (z. b. 0x1200a9).<p>    Dies ist nützlich, wenn Ressourcen spezifische Bitmasken verwendet werden, die nicht Teil des SDDL (Security Deskriptor Definition Language)-Standards sind. Wenn der Wert nicht weggelassen wird, wird Vollzugriff verwendet. |

## <a name="remarks"></a>Hinweise

Bei resourcesacl-Vorgängen müssen Sie über die Berechtigung Schreiben oder Vollzugriff für dieses Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch resourcesacl-Vorgänge durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen des Entfernungs Vorgangs nicht erforderlich ist.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

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