---
title: bitsadmin removecredentials
description: Referenz Artikel für den Befehl "bizadmin removecredenseins", mit dem Anmelde Informationen aus einem Auftrag entfernt werden.
ms.topic: reference
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c380aeba07d3dbbe3278003fdffb48dbb4fce913
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631155"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

Entfernt Anmelde Informationen aus einem Auftrag.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /removecredentials <job> <target> <scheme>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| target | Verwenden Sie entweder den **Server** oder den **Proxy**. |
| scheme | Verwenden Sie einen der folgenden Werte:<ul><li>**Basic.** Das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</li><li>**Lich.** Ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</li><li>**NTLM.** Ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</li><li>**Aushandeln (auch als einfaches und geschütztes Aushandlungs Protokoll bezeichnet).** Ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandiert, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</li><li>**BU.** Ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.</li></ul> |

## <a name="examples"></a>Beispiele

So entfernen Sie Anmelde Informationen aus dem Auftrag *mydownloadjob*:

```
bitsadmin /removecredentials myDownloadJob SERVER BASIC
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
