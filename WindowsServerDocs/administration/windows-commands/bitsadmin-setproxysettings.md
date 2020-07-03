---
title: bitsadmin setproxysettings
description: Referenz Artikel zum Befehl "setproxysettings" von bitadmin, mit dem die Proxy Einstellungen für den angegebenen Auftrag festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a59bbb560b8c89134e81c02f99aaecebdb65ca89
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927586"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

Legt die Proxy Einstellungen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setproxysettings <job> <usage> [list] [bypass]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Nutzung | Legt die Proxy Verwendung fest, einschließlich:<ul><li>**PRECONFIG.** Verwenden Sie die Internet Explorer-Standardeinstellungen des Besitzers.</li><li>**NO_PROXY.** Verwenden Sie keinen Proxy Server.</li><li>**Dire.** Verwenden Sie eine explizite Proxy Liste und Umgehungs Liste. Die Proxy Liste und die Proxy Umgehungs Informationen müssen befolgt werden.</li><li>**Auto Ermittlung.** Erkennt automatisch Proxy Einstellungen.</li></ul> |
| list | Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist. Muss eine durch Trennzeichen getrennte Liste der zu verwendenden Proxy Server enthalten. |
| Umgehung | Wird verwendet, wenn der *Usage* -Parameter auf Override festgelegt ist. Muss eine durch Leerzeichen getrennte Liste von Hostnamen oder IP-Adressen oder beides enthalten, für die Übertragungen nicht über einen Proxy weitergeleitet werden sollen. Dies kann dazu führen, dass auf `<local>` alle Server im gleichen LAN verwiesen wird. Werte von NULL können für eine leere Proxy Umgehungs Liste verwendet werden. |

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
