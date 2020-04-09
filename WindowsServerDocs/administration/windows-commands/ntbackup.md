---
title: ntbackup
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b68b4cca579a5fc27f921ce2f4fcc6976d8e5600
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838013"
---
# <a name="ntbackup"></a>ntbackup



Der Befehl " **Ntbackup** " ist in Windows Vista oder Windows Server 2008 nicht verfügbar. Stattdessen sollten Sie den Befehl " **Wbadmin** " und die Unterbefehle verwenden, um Ihren Computer und Dateien über eine Eingabeaufforderung zu sichern und wiederherzustellen.

Es ist nicht möglich, mit **ntbackup** erstellte Sicherungen mit **wbadmin** wiederherzustellen. Allerdings ist eine Version von **Ntbackup** als Download für Windows Server 2008-und Windows Vista-Benutzer verfügbar, die mit **Ntbackup**erstellte Sicherungen wiederherstellen möchten. Diese herunterladbare Version von **Ntbackup** ermöglicht die Wiederherstellung nur von Legacy Sicherungen und kann nicht auf Computern verwendet werden, auf denen Windows Server 2008 oder Windows Vista ausgeführt wird, um neue Sicherungen zu erstellen. Informationen zum Herunterladen dieser Version von **Ntbackup**finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917).

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)