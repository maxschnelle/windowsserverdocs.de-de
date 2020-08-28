---
title: bitsadmin setaclflag
description: Referenz Artikel für den BITSAdmin-Befehl setaclflag, mit dem die weitergabesteuerungsflags der Zugriffs Steuerungs Liste (ACL) festgelegt werden.
ms.topic: reference
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89b605e94505610a2b355de9e4bcbc485a2bb7bf
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026298"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Legt die weitergabesteuerungsflags für die Zugriffs Steuerungs Liste (ACL) für den Auftrag fest. Die Flags geben an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Um z. b. den Besitzer und die Gruppe mit der Datei beizubehalten, legen Sie den **Flags** -Parameter auf fest `og` .

## <a name="syntax"></a>Syntax

```
bitsadmin /setaclflag <job> <flags>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| flags | Geben Sie einen oder mehrere der Werte an, einschließlich:<ul><li>**o** -Besitzer Informationen mit Datei kopieren.</li><li>**g** -Gruppeninformationen in Datei kopieren.</li><li>**d** : Kopieren Sie die DACL-Informationen ("-Zugriffs Steuerungs Liste") mit der Datei.</li><li>**s** -Informationen zur System Zugriffs Steuerungs Liste (SACL) mit Datei kopieren.</li></ul> |

## <a name="examples"></a>Beispiele

Um die Weitergabeflags für die Zugriffs Steuerungs Liste für den Auftrag mit dem Namen *mydownloadjob*festzulegen, werden die Besitzer-und Gruppeninformationen mit den heruntergeladenen Dateien verwaltet.

```
bitsadmin /setaclflags myDownloadJob og
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
