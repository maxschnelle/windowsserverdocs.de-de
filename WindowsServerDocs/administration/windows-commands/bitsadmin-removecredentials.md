---
title: bitsadmin removecredentials
description: Windows-Befehls Thema für biout admin **removecredenseins**, mit dem Anmelde Informationen aus einem Auftrag entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dbb25f0b0a19358b83a610c4684a3eb647c8232
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123098"
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

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| target | Verwenden Sie entweder den **Server** oder den **Proxy**. |
| scheme | Verwenden Sie eine der folgenden Aktionen:<ul><li>**Basic.** Das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</li><li>**Lich.** Ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</li><li>**NTLM.** Ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</li><li>**Aushandeln (auch als einfaches und geschütztes Aushandlungs Protokoll bezeichnet).** Ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandiert, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</li><li>**BU.** Ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.</li></ul> |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden die Anmelde Informationen aus dem Auftrag mit dem Namen *mydownloadjob*entfernt.

```
C:\>bitsadmin /removecredentials myDownloadJob SERVER BASIC
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)