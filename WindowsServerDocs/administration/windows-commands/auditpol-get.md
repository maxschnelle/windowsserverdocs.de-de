---
title: Get für "auditpol"
description: Windows-Befehle Thema **"auditpol" erhalten** -Ruft die Systemrichtlinie, die pro-Benutzer-Richtlinie, die Überwachung von Optionen und Audit sicherheitsbeschreibungs-Objekt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe13de4e-836c-4207-b47c-64b6272d6c41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03ba59b19af42ab2d3fdd1dd52d976d381779640
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435143"
---
# <a name="auditpol-get"></a>Get für "auditpol"

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft ab, die Systemrichtlinie, die pro-Benutzer-Richtlinie, die Überwachung von Optionen und Audit sicherheitsbeschreibungs-Objekt.

## <a name="syntax"></a>Syntax
```
auditpol /get 
[/user[:<username>|<{sid}>]]
[/category:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/subcategory:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/option:<option name>]
[/sd]
[/r]
```
## <a name="parameters"></a>Parameter

|  Parameter   |                                                                                                                                         Beschreibung                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    / User     | Zeigt an, der Sicherheitsprinzipal für den die Überwachungsrichtlinie pro Benutzer abgefragt wird. Der/Category oder SubCategory-Parameter muss angegeben werden. Der Benutzer kann als eine Sicherheits-ID (SID) oder ein Name angegeben werden. Wenn kein Benutzerkonto angegeben ist, wird der Dateisystem-Überwachungsrichtlinie abgefragt. |
|  /category   |                                                          Eine oder mehrere Überwachungskategorien von global eindeutigen Bezeichner (GUID) oder den Namen angegeben. Ein Sternchen (\*) kann verwendet werden, um anzugeben, dass alle Überwachungskategorien abgefragt werden sollen.                                                          |
| /subcategory |                                                                                                                  Eine oder mehrere überwachungsunterkategorien anhand des GUID oder den Namen.                                                                                                                  |
|     /sd      |                                                                                                        Ruft die Sicherheitsbeschreibung, die zum Delegieren des Zugriffs auf die Überwachungsrichtlinie ab.                                                                                                        |
|   /option    |                                                                              Ruft die vorhandene Richtlinie für die CrashOnAuditFail FullprivilegeAuditing, AuditBaseObjects oder AuditBasedirectories Optionen ab.                                                                               |
|      /r      |                                                                                                              Zeigt die Ausgabe im Format des Berichts durch Trennzeichen getrennten Werten (CSV).                                                                                                              |
|      /?      |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Hinweise
Alle Kategorien und Unterkategorien können durch die GUID oder den Namen in Anführungszeichen eingeschlossen angegeben werden. Benutzer können durch die SID oder angegeben werden.
für alle Get-Vorgänge für die pro-Benutzer und Systemrichtlinien müssen Sie für dieses Objekt festgelegt werden, in der Sicherheitsbeschreibung Leseberechtigung. Sie können auch Get-Vorgänge ausführen, indem besitzt die **Verwalten von überwachungs- und Sicherheitsprotokollen** Benutzerrecht (SeSecurityPrivilege). Diese Berechtigung ermöglicht jedoch zusätzliche Zugriffsrechte, die nicht zum Ausführen des Get-Vorgangs erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele für
### <a name="examples-for-the-per-user-audit-policy"></a>Beispiele für die Überwachungsrichtlinie pro Benutzer
Zum Abrufen der Einzelbenutzer-Überwachungsrichtlinie für das Gastkonto und zeigen die Ausgabe für das System detaillierte Überwachung, und geben Sie Objektzugriff Kategorien:
```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:"System","detailed Tracking","Object Access"
```
> [!NOTE]
> Dieser Befehl ist in zwei Szenarien hilfreich. Wenn ein bestimmtes Benutzerkonto für verdächtige Aktivitäten zu überwachen, können Sie den Befehl/Get /, um die Ergebnisse in bestimmten Kategorien abrufen, indem Sie eine Richtlinie für die Aufnahme verwenden, um zusätzliche Überwachung zu aktivieren. Oder, wenn zahlreiche jedoch überflüssig Ereignisse überwachungseinstellungen in einem Konto anmelden, können Sie den/GET /-Befehl verwenden, um relevante Ereignisse herausgefiltert werden für dieses Konto mit einer Ausschlussrichtlinie zu filtern. Eine Liste aller Kategorien verwenden Sie den Auditpol/List/Category-Befehl.
> Zum Abrufen der Einzelbenutzer-Überwachungsrichtlinie für eine Kategorie und einer bestimmten Unterkategorie, die die inklusiven und exklusiven Einstellungen für diese Unterkategorie unter der Kategorie "System" für das Gastkonto meldet, geben Sie Folgendes ein:
> ```
> auditpol /get /user:guest /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> Zeigen die Ausgabe im Berichtsformat und den Namen des Computers einschließen möchten, geben Sie Richtlinienziel, Subcategory, Unterkategorie GUID, Inclusion-Einstellungen und ausschlusseinstellungen, aus:
> ```
> auditpol /get /user:guest /category:detailed Tracking" /r
> ```
> ### <a name="examples-for-the-system-audit-policy"></a>Beispiele für die Dateisystem-Überwachungsrichtlinie
> Geben Sie die Richtlinie für das System abrufen Kategorien und Unterkategorien, die Berichte die Kategorie und Unterkategorie-Richtlinieneinstellungen für die Dateisystem-Überwachungsrichtlinie aus:
> ```
> auditpol /get /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> Ruft die Richtlinie für die ausführliche Überwachung-Kategorie und Unterkategorien im Berichtsformat und gehören der Name des Computers, Richtlinienziel, Subcategory, Unterkategorie-GUID, Inclusion-Einstellungen und ausschlusseinstellungen, Typ:
> ```
> auditpol /get /category:"detailed Tracking" /r
> ```
> Zum Abrufen der Richtlinie für zwei Kategorien mit den Kategorien angegeben als GUIDs, die alle sicherheitsüberwachungs-Richtlinieneinstellungen der alle Unterkategorien meldet in zwei Kategorien, Typ:
> ```
> auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> ### <a name="examples-for-auditing-options"></a>Beispiele für die Optionen für die Überwachung
> Geben Sie zum Abrufen des Zustands, entweder aktiviert oder deaktiviert werden, der AuditBaseObjects-Option:
> ```
> auditpol /get /option:AuditBaseObjects
> ```
> [!NOTE]
> Die verfügbaren Optionen sind AuditBaseObjects AuditBaseOperations und FullprivilegeAuditing.
> Geben Sie zum Abrufen des Zustands aktiviert deaktiviert oder 2 der CrashOnAuditFail-Option:
> ```
> auditpol /get /option:CrashOnAuditFail /r
> ```
> #### <a name="additional-references"></a>Zusätzliche Referenzen
> [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
