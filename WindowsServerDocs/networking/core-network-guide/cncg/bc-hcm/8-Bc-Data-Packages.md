---
title: Erstellen von Inhaltsserver-Datenpaketen für Web- und Dateiinhalte (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b8cd284a83736d17859968947f381af171fd6bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817171"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Erstellen von Inhaltsserver-Datenpaketen für Web- und Dateiinhalte (optional)

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können mit diesem Verfahren können Sie die Hashes von Inhalten für Web- und Dateiservern und erstellen Sie dann die Datenpakete, die auf den gehosteten Cacheserver importieren. 

Dieses Verfahren ist optional, da Sie auf die gehosteten Cacheserver nicht zu prehash und preload Inhalten erforderlich sind. Wenn Sie Inhalt nicht vorab laden, werden dem gehosteten Cache automatisch Daten hinzugefügt, wie Clients über die WAN-Verbindung heruntergeladen.

Dieses Verfahren enthält Anweisungen für voraborganisation Inhalt auf Dateiservern und Webservern. Wenn Sie nicht mit einer dieser Typen von inhaltsservern verfügen, müssen Sie keinen führen Sie die Anweisungen für diesen Typ Inhaltsserver.

>[!IMPORTANT]
>Bevor Sie dieses Verfahren auszuführen, müssen Sie installieren und Konfigurieren von BranchCache auf der Inhaltsserver. Darüber hinaus, wenn Sie den geheimen Server auf einem Content Server ändern möchten, sollte dies vor dem vor\-Hashwert der Inhalte – ändern den geheimen Server zuvor erklärt\-Hashes generiert.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-create-content-server-data-packages"></a>Zum Erstellen von Inhaltsserver Daten-Paketen

1. Suchen Sie auf jedem Server Inhalt die Ordner und Dateien, die Hashes und Hinzufügen eines Datenpakets verwendet werden sollen. Identifizieren Sie oder erstellen Sie einen Ordner, in dem Sie Ihr Datenpaket später in diesem Verfahren zu speichern möchten.

2. Öffnen Sie auf dem Server-Computer Windows PowerShell mit Administratorrechten aus.

3. Führen Sie eine oder beide der folgenden Einträge, je nach Art von inhaltsservern, die Sie aus:

    > [!NOTE]
    > Der Wert für den – Pfad Parameter wird dem Ordner, in denen Ihre Inhalte gespeichert ist. Die Beispielwerte in der nachfolgenden Befehle ersetzen Sie durch einen gültigen Ordnerpfad auf dem Inhaltsserver, die Daten enthält, die Hashes und einem Paket hinzufügen möchten.
  
    - Wenn der Inhalt, den Sie unterziehen möchten auf einem Dateiserver ist, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Wenn der Inhalt, den Sie unterziehen möchten auf einem Webserver ist, geben Sie den folgenden Befehl, und dann die drücken Sie EINGABETASTE.

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. Erstellen Sie das Paket mithilfe des folgenden Befehls auf jedem der Inhaltsserver an. Ersetzen Sie den Beispielwert \("d:"\\Temp\) für – Destination-Parameters mit dem Speicherort, die Sie identifiziert, oder die zu Beginn dieses Verfahrens erstellt haben.

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. Vom Inhaltsserver zugreifen auf die Freigabe für die gehosteten Cacheserver, in dem Sie Inhalt vorab laden möchten, und kopieren Sie die Datenpakete in die Freigaben auf dem gehosteten Cacheserver.

Mit diesem Handbuch finden Sie [Import-Data-Paketen auf dem gehosteten Cacheserver &#40;Optional&#41;](9-Bc-Import-Data.md).

