---
title: bitsadmin setproxysettings
description: Referenz Thema für den Befehl "bizadmin setproxysettings", mit dem die Proxy Einstellungen für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f7c54b3081c85756735d921fb70f726ba60d833
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720494"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

Legt die Proxy Einstellungen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setproxysettings <job> <usage> [list] [bypass]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Nutzung | Legt die Proxy Verwendung fest, einschließlich:<ul><li>**PRECONFIG.** Verwenden Sie die Internet Explorer-Standardeinstellungen des Besitzers.</li><li>**NO_PROXY.** Verwenden Sie keinen Proxy Server.</li><li>**Dire.** Verwenden Sie eine explizite Proxy Liste und Umgehungs Liste. Die Proxy Liste und die Proxy Umgehungs Informationen müssen befolgt werden.</li><li>**Auto Ermittlung.** Erkennt automatisch Proxy Einstellungen.</li></ul> |
| list | Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist. Muss eine durch Trennzeichen getrennte Liste der zu verwendenden Proxy Server enthalten. |
| Umgehung | Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist. Muss eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen oder beides enthalten, für die Übertragungen nicht über einen Proxy weitergeleitet werden sollen. Dies kann dazu `<local>` führen, dass auf alle Server im gleichen LAN verwiesen wird. Werte von NULL können für eine leere Proxy Umgehungs Liste verwendet werden. |

## <a name="examples"></a>Beispiele

So legen Sie die Proxy Einstellungen mithilfe der verschiedenen Verwendungs Optionen für den Auftrag *mydownloadjob*fest:

```
bitsadmin /setproxysettings myDownloadJob PRECONFIG
```

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
```
```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80
```

```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
