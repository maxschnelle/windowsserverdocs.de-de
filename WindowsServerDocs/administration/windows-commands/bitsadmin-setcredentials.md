---
title: bitsadmin setcredentials
description: Windows-Befehls Thema für **bigsadmin setanmelde**Informationen, mit dem einem Auftrag Anmelde Informationen hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96b3973e9b5c01e2577873fa292e4c0725498f91
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123035"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

Fügt einem Auftrag Anmelde Informationen hinzu.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /setcredentials <job> <target> <scheme> <username> <password>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| target | Verwenden Sie entweder den **Server** oder den **Proxy**. |
| scheme | Verwenden Sie eine der folgenden Aktionen:<ul><li>**Basic.** Das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</li><li>**Lich.** Ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</li><li>**NTLM.** Ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</li><li>**Aushandeln (auch als einfaches und geschütztes Aushandlungs Protokoll bezeichnet).** Ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandiert, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</li><li>**BU.** Ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.</li></ul> |
| Benutzername | Der Name des Benutzers. |
| password | Das Kennwort, das dem angegebenen *Benutzernamen*zugeordnet ist. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden dem Auftrag mit dem Namen *mydownloadjob*Anmelde Informationen hinzugefügt.

```
C:\>bitsadmin /setcredentials myDownloadJob SERVER BASIC Edward password20
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)