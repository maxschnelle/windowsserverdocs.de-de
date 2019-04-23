---
title: ResourceSACL mit "auditpol"
description: Windows-Befehle Thema **Uditpol ResourceSACL** -globale Ressource Systemzugriff-Steuerungslisten (SAcls) konfiguriert.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 375f37250404dd6740027cb18959697626c1ffc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837491"
---
# <a name="auditpol-resourcesacl"></a>ResourceSACL mit "auditpol"



Konfiguriert die globale Ressource Systemzugriff-Steuerungslisten (SACLs).

> [!NOTE]
> Gilt nur für Windows 7 und Windows Server 2008 R2.

Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

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
|/set|Fügt einen neuen Eintrag hinzu oder aktualisiert einen vorhandenen Eintrag in der SACL-Ressource für die Ressource angegebene Typ.|
|/remove|Entfernt alle Einträge für den angegebenen Benutzer in die globale objektzugriffsüberwachung Überwachung Liste an.|
|/clear|Entfernt alle Einträge aus die globale objektzugriffsüberwachung Überwachung Liste.|
|/ View|Listet die globale Objekt Zugriff Überwachungseinträge in eine Ressourcen-SACL. Der Benutzer und Azure-Ressourcentypen sind optional.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="arguments"></a>Argumente

|Argument|Beschreibung|
|--------|-----------|
|/type|Die Ressource, für welches, die Objekt dateizugriffsüberwachung konfiguriert wird. Die unterstützten Argumentwerte sind-Datei (für Verzeichnisse und Dateien) und den Schlüssel (für Registrierungsschlüssel).</br>Hinweis: Die Datei und den Schlüssel-Werte sind Groß-/Kleinschreibung beachtet.|
|/success|Gibt die erfolgreiche Überwachung.|
|/failure|Gibt die Fehlerüberwachung.|
|/ User|Gibt einen Benutzer in einem der folgenden Formate an:</br>-DomainName\Account (z. B. DOM\Administrators)</br>-StandaloneServer\Group Konto (finden Sie unter [LookupAccountName-Funktion](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx))</br>-{S-1-x-x-x-x} (X wird angegeben, in Dezimalstellen und die gesamte-SID muss in geschweifte Klammern eingeschlossen werden); zum Beispiel: {S-1-5-21-5624481-130208933-164394174-1001}</br>    Hinweis:     Wenn die SID-Form verwendet wird, erfolgt keine Überprüfung, um zu überprüfen, ob dieses Konto vorhanden ist.|
|/access|Gibt eine Berechtigungsmaske, die in einem von zwei Formaten angegeben werden kann:</br>– Eine Sequenz von einfachen rechten:</br>    -Generische Zugriffsrechte:</br>        -GA - GENERISCHE, DIE ALLE</br>        -GL – GENERISCHES LESEN</br>        -GW - GENERISCHES SCHREIBEN</br>        -GX - GENERISCHE AUSFÜHREN</br>    -Zugriffsrechte für Dateien:</br>        -FA - DATEIZUGRIFF ALLE</br>        -FR - DATEI, DIE GENERISCHE LESEN</br>        -WL - GENERISCHES SCHREIBEN</br>        FÜHREN SIE DIE DATEI GENERISCHE - FX-</br>    -Zugriffsrechte für Registrierungsschlüssel:</br>        -KA - TASTE ALLE ZUGRIFFE</br>        -KR - SCHLÜSSEL GELESEN WERDEN.</br>        -KW - WICHTIGE SCHREIBEN</br>        FÜHREN SIE - KX - SCHLÜSSEL</br>    Zum Beispiel: "/ Zugriff: FRFW" Aktivieren von Überwachungsereignissen für Lese- und Schreibvorgänge</br>– Ein Hexadezimalwert, der die Zugriffsmaske (z. B. 0x1200a9) darstellt</br>    Dies ist nützlich, wenn ressourcenspezifischen Bitmasken zu verwenden, die nicht Teil der Security Descriptor Definition Language (SDDL)-Standard sind. Wenn nicht angegeben, wird Vollzugriff verwendet.|

## <a name="remarks"></a>Hinweise

Für ResourceSACL-Vorgänge müssen Sie Schreib-oder Vollzugriff für das Objekt, das in der Sicherheitsbeschreibung festgelegt. Sie können auch ResourceSACL Vorgänge ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Diese Berechtigung ermöglicht jedoch zusätzliche Zugriffsrechte, die nicht zum Ausführen des Entfernungsvorgangs erforderlich ist.

## <a name="BKMK_Examples"></a>Beispiele für

Um eine globale Ressource festzulegen versucht, die SACL erfolgreiche Zugriffsversuche überwacht durch einen Benutzer auf einen Registrierungsschlüssel:
```
auditpol /resourceSACL /set /type:Key /user:MYDOMAIN\myuser /success
```
So richten Sie eine globale Ressourcen-SACL zu erfolgreichen und fehlgeschlagenen Versuche von einem Benutzer generisches lesen und Schreiben von Funktionen, die auf Dateien oder Ordner überwachen
```
auditpol /resourceSACL /set /type:File /user:MYDOMAIN\myuser /success /failure /access:FRFW
```
So entfernen Sie alle globalen Ressourcen-SACL-Einträge für Dateien oder Ordner:
```
auditpol /resourceSACL /type:File /clear
```
So entfernen alle globalen Ressourcen-SACL-Einträge für einen bestimmten Benutzer aus Dateien oder Ordner:
```
auditpol /resourceSACL /remove /type:File /user:{S-1-5-21-56248481-1302087933-1644394174-1001}
```
So Listen Sie die globale objektzugriffsüberwachung Überwachungseinträge für Dateien oder Ordner festlegen:
```
auditpol /resourceSACL /type:File /view
```
Um eine Liste globale Zugriff auf das Objekt Überwachungseinträge für einen bestimmten Benutzer, die auf Dateien oder Ordner festgelegt werden:
```
auditpol /resourceSACL /type:File /view /user:MYDOMAIN\myuser
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)