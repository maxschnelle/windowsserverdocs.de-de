---
title: Migrieren eines domänenbasierten Namespace zum Windows Server 2008-Modus
description: Dieser Artikel beschreibt die Vorgehensweise beim Migrieren eines domänenbasierten Namespaces zum Windows Server 2008-Modus
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 75e366d6b72e9f08ece77558cff253239474777c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386207"
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>Migrieren Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Der Windows Server 2008-Modus für domänenbasierte Namespaces unterstützt Support für die zugriffsbasierte Aufzählung und eine bessere Skalierbarkeit.

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>So migrieren Sie einen domänenbasierten Namespace zum Windows Server 2008-Modus

Um einen domänenbasierten Namespace vom Windows 2000 Server-Modus zum Windows Server 2008-Modus zu migrieren, müssen Sie den Namespace in eine Datei exportieren, den Namespace löschen und ihn neu im Windows Server 2008-Modus erstellen und anschließend in die Namespaceeinstellungen importieren. Führen Sie dazu die nachfolgend aufgeführten Schritte aus:

1.  Öffnen Sie ein Eingabe Aufforderungs Fenster, und geben Sie den folgenden Befehl ein, um den Namespace in eine Datei zu exportieren, wobei \\ @ no__t-1*Domain*\\*Namespace* der Name der entsprechenden Domäne ist und Namespace und *Pfad @ no__t-6filename* der Pfad ist. und der Dateiname der Datei für den Export:
     ```
     Dfsutil root export \\domain\namespace path\filename.xml 
     ```
2.  Notieren Sie sich den Pfad (\\ @ no__t-1*Server* \\-*Freigabe* ) für jeden Namespace Server. Sie müssen Namespaceserver manuell auf den neu erstellten Namespace hinzufügen, da „Dfsutil” keine Namespaceserver importieren kann.
3.  Klicken Sie mit der rechten Maustaste unter DFS-Verwaltung auf die Namespaces, und klicken Sie dann auf **Löschen**, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, <br /> Dabei ist \\ @ no__t-1*Domain*\\-*Namespace* der Name der entsprechenden Domäne und des entsprechenden Namespace:
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  Erstellen Sie in der DFS-Verwaltung erneut den Namespace mit dem gleichen Namen, verwenden Sie allerdings den Windows Server 2008-Modus, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\ @ no__t-1*Server*\\-*Namespace* ist der Name des entsprechenden Servers und der entsprechenden Freigabe für den Namespace Stamm:
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  Um den Namespace aus der Exportdatei zu importieren, geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\ @ no__t-1*Domäne*\\-*Namespace* ist der Name der entsprechenden Domäne und des Namespace und der *Pfad @ no__t-6filename* ist der Pfad und der Dateiname der zu importierenden Datei:
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > Um die erforderliche Zeit während des Imports eines großen Namespaces zu minimieren, führen Sie den Stamm-Importbefehl **Dfsutil** lokal auf einem Namespaceserver aus.
6.  Fügen Sie alle verbleibenden Namespaceserver auf den neu erstellten Namespace hinzu, indem Sie mit der rechten Maustaste auf den Namespace in der DFS-Verwaltung klicken und dann auf **Namespace-Server hinzufügen**, oder geben Sie den folgenden Befehl in eine Eingabeaufforderung ein, wobei <br /> \\ @ no__t-1*Server*\\-*Freigabe* ist der Name des entsprechenden Servers und der entsprechenden Freigabe für den Namespace Stamm:
     ```
     Dfsutil target add \\server\share 
     ```

    > [!NOTE]
    > Sie können Namespaceserver vor dem Importieren des Namespaces hinzufügen, dies führt allerdings dazu, dass die Namespaceserver die Metadaten für den Namespace inkrementell herunterladen anstatt den gesamten Namespace sofort nach dem Hinzufügen als Namespaceserver herunterzuladen.

## <a name="see-also"></a>Siehe auch
-   [Bereitstellen von DFS-Namespaces](deploying-dfs-namespaces.md)
-   [Auswählen eines Namespacetyps](choose-a-namespace-type.md)