---
title: ntbackup
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba3aaaa192283e0e1dc1777a27fc13973949784b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723484"
---
# <a name="ntbackup"></a>ntbackup



Der Befehl " **Ntbackup** " ist in Windows Vista oder Windows Server 2008 nicht verfügbar. Stattdessen sollten Sie den Befehl " **Wbadmin** " und die Unterbefehle verwenden, um Ihren Computer und Dateien über eine Eingabeaufforderung zu sichern und wiederherzustellen.

Es ist nicht möglich, mit **ntbackup** erstellte Sicherungen mit **wbadmin** wiederherzustellen. Allerdings ist eine Version von **Ntbackup** als Download für Windows Server 2008-und Windows Vista-Benutzer verfügbar, die mit **Ntbackup**erstellte Sicherungen wiederherstellen möchten. Diese herunterladbare Version von **Ntbackup** ermöglicht die Wiederherstellung nur von Legacy Sicherungen und kann nicht auf Computern verwendet werden, auf denen Windows Server 2008 oder Windows Vista ausgeführt wird, um neue Sicherungen zu erstellen. Informationen zum Herunterladen dieser Version von **Ntbackup**finden [https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917)Sie unter.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)