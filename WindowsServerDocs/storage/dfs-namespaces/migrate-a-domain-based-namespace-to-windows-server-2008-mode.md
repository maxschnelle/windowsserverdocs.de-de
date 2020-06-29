---
title: Migrieren Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus
description: In diesem Artikel wird beschrieben, wie Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus migrieren.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3aa7743773a8a6e9ed22c0f626c2c6a0dbafce56
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475467"
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>Migrieren eines domänenbasierten Namespace zum Windows Server 2008-Modus

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Der Windows Server 2008-Modus für Domänen basierte Namespaces bietet Unterstützung für die Zugriffs basierte Aufzählung und eine größere Skalierbarkeit.

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>So migrieren Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus

Wenn Sie einen domänenbasierten Namespace vom Windows 2000-Server Modus zum Windows Server 2008-Modus migrieren möchten, müssen Sie den Namespace in eine Datei exportieren, den Namespace löschen, ihn im Windows Server 2008-Modus neu erstellen und dann die Namespace Einstellungen importieren. Verwenden Sie dazu das folgende Verfahren:

1.  Öffnen Sie ein Eingabe Aufforderungs Fenster, und geben Sie den folgenden Befehl ein, um den Namespace in eine Datei zu exportieren, wobei \\ \\ *Domänen* \\ *Namespace* der Name der entsprechenden Domäne und Namespace und *Pfad \\ Dateiname* der Pfad und der Dateiname der zu exportierenden Datei sind:
     ```
     Dfsutil root export \\domain\namespace path\filename.xml
     ```
2.  Notieren Sie sich den Pfad ( \\ \\ *Server* \\ *Freigabe* ) für jeden Namespace Server. Sie müssen dem neu erstellten Namespace manuell Namespace Server hinzufügen, da Dfsutil keine Namespace Server importieren kann.
3.  Klicken Sie in der DFS-Verwaltung mit der rechten Maustaste auf den Namespace, und klicken Sie dann auf **Löschen**, oder geben Sie den folgenden Befehl an einer Eingabeaufforderung ein <br /> dabei \\ \\ ist der *Domänen* \\ *Namespace* der Name der entsprechenden Domäne und des entsprechenden Namespace:
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  Erstellen Sie in der DFS-Verwaltung den Namespace mit demselben Namen neu, verwenden Sie jedoch den Windows Server 2008-Modus, oder geben Sie den folgenden Befehl an einer Eingabeaufforderung ein, wobei <br /> \\\\*Server* \\ *Namespace* ist der Name des entsprechenden Servers und der entsprechenden Freigabe für den Namespace Stamm:
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  Um den Namespace aus der Exportdatei zu importieren, geben Sie den folgenden Befehl an einer Eingabeaufforderung ein, wobei <br /> \\\\*Domäne* \\ *Namespace* ist der Name der entsprechenden Domäne und des Namespace und *Pfad \\ Dateiname* ist der Pfad und Dateiname der zu importierenden Datei:
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > Führen Sie den **dfsutil** root Import-Befehl lokal auf einem Namespace Server aus, um die Zeit zu minimieren, die zum Importieren eines großen Namespace erforderlich ist.
6.  Fügen Sie dem neu erstellten Namespace alle verbleibenden Namespace Server hinzu, indem Sie mit der rechten Maustaste auf den Namespace in der DFS-Verwaltung klicken und dann auf **Namespace Server hinzufügen**klicken, oder indem Sie den folgenden Befehl an einer Eingabeaufforderung eingeben, wobei <br /> \\\\*Server* \\ *Freigabe* ist der Name des entsprechenden Servers und der entsprechenden Freigabe für den Namespace Stamm:
     ```
     Dfsutil target add \\server\share
     ```

    > [!NOTE]
    > Sie können Namespace Server hinzufügen, bevor Sie den Namespace importieren. Dies bewirkt jedoch, dass die Namespace Server die Metadaten für den Namespace inkrementell herunterladen, anstatt den gesamten Namespace nach dem Hinzufügen als Namespace Server sofort herunterzuladen.

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Auswählen eines Namespacetyps](choose-a-namespace-type.md)