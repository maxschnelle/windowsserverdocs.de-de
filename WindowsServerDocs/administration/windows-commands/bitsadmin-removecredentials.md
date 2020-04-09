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
ms.openlocfilehash: 55ff7e2a813c7cc6b60e04d55ef63804a2aed796
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849843"
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
| scheme | Verwenden Sie eine der folgenden Aktionen:<ul><li>**Basic.** Das Authentifizierungsschema, in dem der Benutzername und das Kennwort in Klartext an den Server oder Proxy gesendet werden.</li><li>**lich.** Ein Challenge-Response-Authentifizierungsschema, das eine vom Server angegebene Daten Zeichenfolge für die Abfrage verwendet.</li><li>**NTLM.** Ein Challenge-Response-Authentifizierungsschema, bei dem die Anmelde Informationen des Benutzers zur Authentifizierung in einer Windows-Netzwerkumgebung verwendet werden.</li><li>**Aushandeln (auch als einfaches und geschütztes Aushandlungs Protokoll bezeichnet).** Ein Challenge-Response-Authentifizierungsschema, das mit dem Server oder Proxy aushandiert, um zu bestimmen, welches Schema für die Authentifizierung verwendet werden soll. Beispiele sind das Kerberos-Protokoll und NTLM.</li><li>**BU.** Ein von Microsoft bereitgestellter zentralisierter Authentifizierungsdienst, der eine einzelne Anmeldung für Mitglieder Standorte bietet.</li></ul> |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Anmelde Informationen aus dem Auftrag mit dem Namen *mydownloadjob*entfernt.

```
C:\>bitsadmin /removecredentials myDownloadJob server basic
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)