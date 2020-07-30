---
title: Hinzufügen von Computern zum neuen Windows Server Essentials-Server1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: cdfa9504-9881-4265-b308-c7ee8721bfaa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cbc2276eb3c627ebb94469e0acef2b57d086b5e7
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180746"
---
# <a name="join-computers-to-the-new-windows-server-essentials-server1"></a>Hinzufügen von Computern zum neuen Windows Server Essentials-Server1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_JoinComputers"></a>
 Der nächste Schritt des Migrations Vorgangs besteht im Hinzufügen von Client Computern zum neuen Windows Server Essentials-Netzwerk und zum Aktualisieren Gruppenrichtlinie Einstellungen.

> [!NOTE]
>  Wenn ein Clientcomputer bereits mit dem Quellserver verbunden ist, müssen Sie zunächst die Connector-Software auf dem Clientcomputer deinstallieren, bevor Sie den Computer mit dem Zielserver verbinden können.

 Der Prozess zum Verbinden eines Clientcomputers mit dem Server ist bei Computern, die einer Domäne angehören, der gleiche wie bei Computern, die keiner Domäne angehören.

- Navigieren Sie zu **http://**<em>Ziel-Servername</em>**/ connect** und installieren Sie die Windows Server-Connector-Software, wie bei einem neuen Computer.

> [!NOTE]
>  Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von der Windows Server-Connector-Software nicht unterstützt. Wenn Sie Computer mit Windows XP oder Windows Vista haben, die bereits mit der Domäne verbunden sind, können Sie diesen Schritt überspringen.

### <a name="ensure-that-group-policy-has-updated"></a>Stellen Sie sicher, dass die Gruppenrichtlinie aktualisiert hat

> [!NOTE]
>  Dies ist ein optionaler Schritt, er ist nur erforderlich, wenn der Quellserver mit benutzerdefinierten Gruppenrichtlinieneinstellungen, z. B. Ordnerumleitung konfiguriert wurde.

 Während der Quellserver und der Zielserver noch online sind, sollten Sie sicherzustellen, dass die Gruppenrichtlinieneinstellungen der Clientcomputer auf dem Zielserver repliziert wurden. Führen Sie auf jedem Clientcomputer die folgenden Schritte aus:

1.  Öffnen Sie ein Eingabeaufforderungsfenster.

2.  Geben Sie an der Eingabeaufforderung **GPRESULT /R** ein, und drücken Sie dann die EINGABETASTE.

3.  Überprüfen Sie die Ausgabe für den Abschnitt Gruppenrichtlinie der auf angewendet wurde, und stellen Sie sicher, dass Sie den Ziel Server auflistet, z. b. **destinationsrv. Domain. local**. Zum Beispiel:

    ```
    USER SETTINGS
    --------------
        CN=User,OU=Users,DC=DOMAIN,DC=Local
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM
        Group Policy was applied from:      DestinationSrv.Domain.local
        Group Policy slow link threshold:   500 kbps
        Domain Name:                        Domain
        Domain Type:                        Windows 2011

    ```

4.  Wenn Zielserver nicht aufgeführt ist, geben Sie in eine Eingabeaufforderung **gpupdate /force** ein und drücken Sie dann die EINGABETASTE, um die Gruppenrichtlinieneinstellungen zu aktualisieren. Führen Sie das vorherige Verfahren dann erneut aus.

5.  Wenn der Zielserver immer noch nicht angezeigt wird, liegt möglicherweise ein Fehler in den Gruppenrichtlinieneinstellungen vor oder ein Fehler bei der Anwendung auf diesem bestimmten Client-Computer. Wenn der Zielserver nicht angezeigt wird, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf **Start**, klicken Sie auf **ausführen**, geben Sie **rsop.msc** (Resultant Set of Policy,) ein und drücken Sie dann die EINGABETASTE.

    2.  Erweitern Sie die Struktur mit dem X-Wert, bis Sie zu einem Knoten gelangen.

    3.  Klciekn Sie mit der rechten Maustaste auf den Knoten und klicken Sie auf **Fehler anzeigen** für Informationen zu den Gründen, warum die Gruppenrichtlinieneinstellungen auf dem aufgeführten Computer fehlschlagen.
