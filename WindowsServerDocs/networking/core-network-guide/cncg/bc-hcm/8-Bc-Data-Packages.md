---
title: Erstellen von Inhaltsserver-Datenpaketen für Web- und Dateiinhalte (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 104e3cfd0525c43857bb37d781f6b2475978238e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406383"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Erstellen von Inhaltsserver-Datenpaketen für Web- und Dateiinhalte (optional)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwenden Sie dieses Verfahren, um Inhalt auf Web-und Dateiservern vorzuführen und anschließend Datenpakete zu erstellen, die auf ihren gehosteten Cache Server importiert werden sollen. 

Dieses Verfahren ist optional, weil Sie den Inhalt auf ihren gehosteten Cache Servern nicht vorab in den Hash laden und vorab laden müssen. Wenn Sie keinen Inhalt vorab laden, werden die Daten automatisch dem gehosteten Cache hinzugefügt, wenn Sie von Clients über die WAN-Verbindung heruntergeladen werden.

Diese Prozedur enthält Anweisungen für das vorab Hashen von Inhalten auf Dateiservern und Webservern. Wenn Sie nicht über einen dieser Inhalts Server Typen verfügen, müssen Sie die Anweisungen für den betreffenden inhaltsservertyp nicht ausführen.

>[!IMPORTANT]
>Bevor Sie dieses Verfahren ausführen, müssen Sie BranchCache auf Ihren Inhalts Servern installieren und konfigurieren. Wenn Sie das Server Geheimnis auf einem Inhalts Server ändern möchten, können Sie dies auch vor dem\-Hashs-Inhalt tun – durch das Ändern des Server Geheimnisses werden zuvor\-generierte Hashes ungültig.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-create-content-server-data-packages"></a>So erstellen Sie Inhalts Server-Datenpakete

1. Suchen Sie auf jedem Inhalts Server die Ordner und Dateien, die Sie vorab Hashen und zu einem Datenpaket hinzufügen möchten. Identifizieren oder erstellen Sie einen Ordner, in dem Sie das Datenpaket später in diesem Verfahren speichern möchten.

2. Öffnen Sie Windows PowerShell mit Administrator Rechten auf dem Server Computer.

3. Führen Sie eine oder beide der folgenden Aktionen aus, abhängig von den Typen der Inhalts Server, die Sie haben:

    > [!NOTE]
    > Der Wert für den – path-Parameter ist der Ordner, in dem sich der Inhalt befindet. Sie müssen die Beispiel Werte in den nachfolgenden Befehlen durch einen gültigen Ordner Speicherort auf Ihrem Inhalts Server ersetzen, der Daten enthält, die Sie einem Paket vorab hinzufügen möchten.
  
    - Wenn sich der Inhalt, den Sie als prähash ausführen möchten, auf einem Dateiserver befindet, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Wenn sich der Inhalt, der als prähash verwendet werden soll, auf einem Webserver befindet, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. Erstellen Sie das Datenpaket, indem Sie den folgenden Befehl auf jedem ihrer Inhalts Server ausführen. Ersetzen Sie den Beispiel Wert \(D:\\Temp\) für den – Destination-Parameter durch den Speicherort, den Sie am Anfang dieses Verfahrens identifiziert oder erstellt haben.

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. Greifen Sie vom Inhalts Server aus auf die Freigabe auf ihren gehosteten Cache Servern zu, auf denen Sie Inhalt vorab laden möchten, und kopieren Sie die Datenpakete in die Freigaben auf den gehosteten Cache Servern.

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Importieren von Datenpaketen auf dem &#40;gehosteten Cache Server optional&#41;](9-Bc-Import-Data.md).

