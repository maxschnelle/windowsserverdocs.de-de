---
title: Auditpol Get
description: 'Windows-Befehls Thema für **Auditpol Get** : Ruft die System Richtlinie, die Richtlinie für benutzerspezifische Richtlinien, Überwachungs Optionen und das Überwachungs Sicherheits Deskriptor-Objekt ab.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 296fc5afb540411d76b563faca42fc045b8df3b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382488"
---
# <a name="auditpol-get"></a>Auditpol Get

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft die System Richtlinie, die Richtlinie pro Benutzer, die Überwachungs Optionen und das Überwachungs Sicherheits Deskriptor-Objekt ab.

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
|    /User     | Zeigt den Sicherheits Prinzipal an, für den die Überwachungsrichtlinie pro Benutzer abgefragt wird. Der/Category-Parameter oder der/SubCategory-Parameter muss angegeben werden. Der Benutzer kann als Sicherheits-ID (SID) oder Name angegeben werden. Wenn kein Benutzerkonto angegeben ist, wird die System Überwachungsrichtlinie abgefragt. |
|  /Category   |                                                          Eine oder mehrere Überwachungs Kategorien, die durch Globally Unique Identifier (GUID) oder den Namen angegeben werden. Ein Sternchen (\*) kann verwendet werden, um anzugeben, dass alle Überwachungs Kategorien abgefragt werden sollen.                                                          |
| /SubCategory |                                                                                                                  Eine oder mehrere Überwachungs Unterkategorien, die durch GUID oder Name angegeben werden.                                                                                                                  |
|     /sd      |                                                                                                        Ruft die Sicherheits Beschreibung ab, die zum Delegieren des Zugriffs auf die Überwachungsrichtlinie verwendet wird.                                                                                                        |
|   /Option    |                                                                              Ruft die vorhandene Richtlinie für die Optionen CrashOnAuditFail, FullPrivilegeAuditing, auditbaseobjects oder auditbasedirectories ab.                                                                               |
|      /r      |                                                                                                              Zeigt die Ausgabe im Berichtsformat an, durch Kommas getrennte Werte (CSV).                                                                                                              |
|      /?      |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="remarks"></a>Hinweise
Alle Kategorien und Unterkategorien können durch die GUID oder den Namen angegeben werden, die in Anführungszeichen eingeschlossen sind. Benutzer können nach SID oder Name angegeben werden.
für alle Get-Vorgänge für die Richtlinie und die System Richtlinie pro Benutzer müssen Sie über die Berechtigung Lesen für das Objekt verfügen, das in der Sicherheits Beschreibung festgelegt ist. Sie können auch Get-Vorgänge durchführen, indem Sie das Benutzerrecht zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** (SeSecurityPrivilege) besitzen. Dieses Recht ermöglicht jedoch zusätzlichen Zugriff, der zum Ausführen des Get-Vorgangs nicht erforderlich ist.
## <a name="BKMK_examples"></a>Beispiele
### <a name="examples-for-the-per-user-audit-policy"></a>Beispiele für die Überwachungsrichtlinie pro Benutzer
Geben Sie Folgendes ein, um die Überwachungsrichtlinie pro Benutzer für das Gastkonto abzurufen und die Ausgabe für die Kategorien "System", "ausführliche Nachverfolgung" und "Objektzugriff" anzuzeigen:
```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:"System","detailed Tracking","Object Access"
```
> [!NOTE]
> Dieser Befehl ist in zwei Szenarios nützlich. Wenn Sie ein bestimmtes Benutzerkonto auf verdächtige Aktivitäten überwachen, können Sie den/get-Befehl verwenden, um die Ergebnisse in bestimmten Kategorien abzurufen, indem Sie eine Inklusions Richtlinie verwenden, um zusätzliche Überwachung zu aktivieren. Wenn die Überwachungs Einstellungen für ein Konto zahlreiche, aber überflüssige Ereignisse protokollieren, können Sie den/get-Befehl verwenden, um überflüssige Ereignisse für dieses Konto mit einer Ausschluss Richtlinie herauszufiltern. Eine Liste aller Kategorien erhalten Sie mit dem Befehl auditpol/list/Category.
> Zum Abrufen der Überwachungsrichtlinie pro Benutzer für eine Kategorie und eine bestimmte Unterkategorie, in der die inklusiven und exklusiven Einstellungen für diese Unterkategorie in der Kategorie System für das Gastkonto gemeldet werden, geben Sie Folgendes ein:
> ```
> auditpol /get /user:guest /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> Geben Sie Folgendes ein, um die Ausgabe im Berichtsformat anzuzeigen und den Computernamen, das Richtlinien Ziel, die Unterkategorie, die unterkategorieguid, die Inklusions Einstellungen und die Ausschluss Einstellungen einzuschließen:
> ```
> auditpol /get /user:guest /category:detailed Tracking" /r
> ```
> ### <a name="examples-for-the-system-audit-policy"></a>Beispiele für die System Überwachungsrichtlinie
> Zum Abrufen der Richtlinie für die System Kategorie und die Unterkategorien, die die Richtlinien Einstellungen Kategorie und Unterkategorie für die System Überwachungsrichtlinie melden, geben Sie Folgendes ein:
> ```
> auditpol /get /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> Geben Sie Folgendes ein, um die Richtlinie für die ausführliche nach Verfolgungs Kategorie und die Unterkategorien im Berichtsformat abzurufen, und geben Sie den Computernamen, das Richtlinien Ziel, die Unterkategorie, die GUID der Unterkategorie, Inklusions Einstellungen und Ausschluss Einstellungen ein:
> ```
> auditpol /get /category:"detailed Tracking" /r
> ```
> Zum Abrufen der Richtlinie für zwei Kategorien mit den als GUIDs angegebenen Kategorien, die alle Überwachungs Richtlinien Einstellungen für alle Unterkategorien in zwei Kategorien meldet, geben Sie Folgendes ein:
> ```
> auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> ### <a name="examples-for-auditing-options"></a>Beispiele für Überwachungs Optionen
> Geben Sie Folgendes ein, um den Status der Option auditbaseobjects abzurufen, der entweder aktiviert oder deaktiviert ist:
> ```
> auditpol /get /option:AuditBaseObjects
> ```
> [!NOTE]
> Die verfügbaren Optionen sind auditbaseobjects, auditbaseoperations und FullPrivilegeAuditing.
> Geben Sie Folgendes ein, um den Status "aktiviert", "deaktiviert" oder "2" der CrashOnAuditFail-Option abzurufen:
> ```
> auditpol /get /option:CrashOnAuditFail /r
> ```
> #### <a name="additional-references"></a>Weitere Verweise
> [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
