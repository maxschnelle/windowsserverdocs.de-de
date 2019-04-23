---
title: Ausführen des WSUS-Replikatmodus
description: 'Windows Server Update Service (WSUS)-Thema - Replikatmodus konfigurieren '
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d218cd6b-3b6b-4429-913b-31d412ce3356
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b4139354a3f0f7b1f1a97107d2f6b28db2b02c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878741"
---
# <a name="running-wsus-replica-mode"></a>Ausführen des WSUS-Replikatmodus

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ein WSUS-Server im Replikatmodus erbt, der die updategenehmigungen und Computergruppen, die auf einem Verwaltungsserver erstellt wurden. In einem Szenario, Replikatmodus verwendet haben, müssen Sie normalerweise einen einzelner Verwaltungsserver und eine oder mehrere untergeordnete WSUS-Replikatserver in der gesamten Organisation, basierend auf der Standort- bzw. organisationstopografie verteilt. Sie genehmigen Updates und erstellen Computergruppen auf dem Verwaltungsserver, die der replikatmodusserver anschließend spiegelt. Replikatmodusserver können nur während der WSUS-Setup eingerichtet werden, und falls Sie dieses Szenario implementiert, ist es wahrscheinlich daran, dass in Ihrer Organisation, die Genehmigungen aktualisieren ist es wichtig, und Computergruppen werden zentral verwaltet.

Wenn Ihr WSUS-Server im Replikatmodus ausgeführt wird, werden Sie möglicherweise nur begrenzte Verwaltungsfunktionen auf dem Server ausführen, die in erster Linie enthalten soll:

-   Das Hinzufügen und Entfernen von Computern aus Computergruppen. Gruppenmitgliedschaft für Computer wird nicht an Replikatserver verteilt, die nur auf der Computer Gruppen selbst. Auf einen Replikatserver Modus, werden Sie daher die Computergruppen, die Sie auf dem Verwaltungsserver erstellt erben. Allerdings werden die Gruppe leer sein. Sie müssen den Client dann Computer zuweisen, die auf den Replikatserver für die Computergruppen zu verbinden.

-   Festlegen eines Synchronisierungszeitplans

-   Proxyserver Einstellungen

-   Angeben der Updatequelle. Dies kann einem anderen Server als dem Verwaltungsserver sein.

-   Aufrufen verfügbarer Updates

-   Überwachen von Update "," Synchronisierung "," des Computers, und "WSUS-Einstellungen auf dem server

-   Replikatmodusserver Berichte verfügbare mit allen standard WSUS



