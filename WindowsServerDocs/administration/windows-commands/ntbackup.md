---
title: ntbackup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebbe71fd5547311beb36747d32d695823e0f0059
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372677"
---
# <a name="ntbackup"></a>ntbackup



Der Befehl " **Ntbackup** " ist in Windows Vista oder Windows Server 2008 nicht verfügbar. Stattdessen sollten Sie den Befehl " **Wbadmin** " und die Unterbefehle verwenden, um Ihren Computer und Dateien über eine Eingabeaufforderung zu sichern und wiederherzustellen.

Es ist nicht möglich, mit **ntbackup** erstellte Sicherungen mit **wbadmin** wiederherzustellen. Allerdings ist eine Version von **Ntbackup** als Download für Windows Server 2008-und Windows Vista-Benutzer verfügbar, die mit **Ntbackup**erstellte Sicherungen wiederherstellen möchten. Diese herunterladbare Version von **Ntbackup** ermöglicht die Wiederherstellung nur von Legacy Sicherungen und kann nicht auf Computern verwendet werden, auf denen Windows Server 2008 oder Windows Vista ausgeführt wird, um neue Sicherungen zu erstellen. Informationen zum Herunterladen dieser Version von **Ntbackup**finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917).

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)