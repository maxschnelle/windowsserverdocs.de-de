---
title: "Migrieren Sie einen domänenbasierten Namespace zum Windows Server2008-Modus"
description: "Dieser Artikel beschreibt die Vorgehensweise beim Migrieren eines domänenbasierten Namespaces zum Windows Server2008-Modus"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1ef356e4f2abccb375732b7ec60a374c64dc0e7f
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>Migrieren Sie einen domänenbasierten Namespace zum Windows Server2008-Modus

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Der Windows Server2008-Modus für domänenbasierte Namespaces unterstützt Support für die zugriffsbasierte Aufzählung und eine bessere Skalierbarkeit.

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>So migrieren Sie einen domänenbasierten Namespace zum Windows Server2008-Modus

Um einen domänenbasierten Namespace vom Windows2000 Server-Modus zum Windows Server2008-Modus zu migrieren, müssen Sie den Namespace in eine Datei exportieren, den Namespace löschen und ihn neu im Windows Server2008-Modus erstellen und anschließend in die Namespaceeinstellungen importieren. Führen Sie dazu die nachfolgend aufgeführten Schritte aus:

1.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl ein, um den Namespace in eine Datei zu exportieren, wobei \\\*Domäne*\\*Namespace* der Name der entsprechenden Domäne und des Namespace ist und *Pfad\\Dateiname* der Pfad und Dateiname der zu exportierenden Datei ist:
     ```
     Dfsutil root export \\domain\namespace path\filename.xml 
     ```
2.  Notieren Sie den Pfad (\\\*Server* \\*Freigeben* ) für jeden Namespaceserver. Sie müssen Namespaceserver manuell auf den neu erstellten Namespace hinzufügen, da „Dfsutil” keine Namespaceserver importieren kann.
3.  Klicken Sie mit der rechten Maustaste unter DFS-Verwaltung auf die Namespaces, und klicken Sie dann auf **Löschen**, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, <br /> wobei \\\*Domäne*\\*Namespace* der Name der entsprechenden Domäne und des Namespace sind:
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  Erstellen Sie in der DFS-Verwaltung erneut den Namespace mit dem gleichen Namen, verwenden Sie allerdings den Windows Server2008-Modus, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\\\*Server*\\*Namespace* der Name des entsprechenden Servers und der Freigabe für den Namespacestamm sind:
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  Um den Namespace aus der Exportdatei zu importieren, geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\\\*Domäne*\\*Namespace* der Name der entsprechenden Domäne und des Namespace sind und *Pfad\\Dateiname* der Pfad und Dateiname der zu importierenden Datei sind:
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > Um die erforderliche Zeit während des Imports eines großen Namespaces zu minimieren, führen Sie den Stamm-Importbefehl **Dfsutil** lokal auf einem Namespaceserver aus.
6.  Fügen Sie alle verbleibenden Namespaceserver auf den neu erstellten Namespace hinzu, indem Sie mit der rechten Maustaste auf den Namespace in der DFS-Verwaltung klicken und dann auf **Namespace-Server hinzufügen**, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\\\*Server*\\*Freigeben* der Name des entsprechenden Servers und der Freigabe für den Namespacestamm sind:
     ```
     Dfsutil target add \\server\share 
     ```

    > [!NOTE]
    > Sie können Namespaceserver vor dem Importieren des Namespaces hinzufügen, dies führt allerdings dazu, dass die Namespaceserver die Metadaten für den Namespace inkrementell herunterladen anstatt den gesamten Namespace sofort nach dem Hinzufügen als Namespaceserver herunterzuladen.

## <a name="see-also"></a>Weitere Informationen:
-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Namespacetyp auswählen](choose-a-namespace-type.md)