---
title: bitsadmin setproxysettings
description: Referenz Artikel zum Befehl "setproxysettings" von bitadmin, mit dem die Proxy Einstellungen für den angegebenen Auftrag festgelegt werden.
ms.topic: reference
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 199cb3f4b4259a52a8960cac23b9e408e71ded23
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630683"
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
