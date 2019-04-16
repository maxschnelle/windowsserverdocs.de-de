---
title: Erstellen von Inhalten Datenpaketen für Web- und Dateiinhalte (Optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f814bbac5c74081259d8eef6deda79d914bfec7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Erstellen von Inhalten Datenpaketen für Web- und Dateiinhalte (Optional)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können mithilfe dieses Verfahrens können Sie Inhalte auf Web- und Dateiservern vorab der Hashfunktion unterziehen, und klicken Sie dann Erstellen von Datenpaketen auf dem Cacheserver gehosteten importieren. 

Dieses Verfahren ist optional, da Sie auf die gehosteten Cacheserver nicht prehash und vorab geladene erforderlich sind. Wenn Sie Inhalt nicht vorab laden, werden dem gehosteten Cache automatisch Daten hinzugefügt, wie Clients über die WAN-Verbindung heruntergeladen.

Dieses Verfahren bietet Anweisungen für die Inhalte auf Dateiservern und Webservern voraborganisation. Wenn Sie nicht mit einem dieser Typen von inhaltsservern verfügen, müssen Sie nicht die Anleitung für diesen Typ Inhaltsserver ausführen.

>[!IMPORTANT]
>Bevor Sie dieses Verfahren ausführen, müssen Sie installieren und Konfigurieren von BranchCache auf der Inhaltsserver. Darüber hinaus, wenn Sie den Serverschlüssel auf Inhaltsserver ändern möchten, sollte dies vor dem registrierungseintragswert hashing Inhalte – ändern den Serverschlüssel Previously\ generierten Hashes ungültig.

Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-create-content-server-data-packages"></a>Zum Erstellen von Inhaltsserver Datenpaketen

1. Suchen Sie auf jedem Inhaltsserver Ordner und Dateien, die Sie vorab der Hashfunktion unterziehen und einer Datenpaket hinzufügen möchten. Identifizieren Sie, oder erstellen Sie einen Ordner zum Speichern Ihrer Datenpaket später in diesem Verfahren werden soll.

2. Öffnen Sie auf dem Servercomputer des Windows PowerShell mit Administratorrechten.

3. Führen Sie eine oder beide der folgenden Optionen, je nachdem, welche Inhaltsserver, die Sie:

    > [!NOTE]
    > Der Wert für den – Pfad-Parameter ist der Ordner, in dem der Inhalt befindet. Sie müssen die Beispielwerte in den Befehlen unter durch einen gültigen Speicherort auf dem Inhaltsserver ersetzen, die Daten enthält, die Sie vorab der Hashfunktion unterziehen, und ein Paket hinzufügen möchten.
  
    - Wenn die Inhalte, die Sie vorab der Hashfunktion unterziehen möchten auf einem Dateiserver ist, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Ist der Inhalt, den Sie vorab der Hashfunktion unterziehen möchten auf einem Webserver, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. Erstellen Sie das Datenpaket durch Ausführen des folgenden Befehls auf jedem der Inhaltsserver. Ersetzen Sie die Beispiel-Wert-\(D:\\temp\) für – Destination-Parameters mit dem Speicherort, den Sie zu Beginn dieses Verfahrens erstellt oder identifiziert.

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. Vom Inhaltsserver Zugriff auf die Freigabe auf die gehosteten Cacheserver, in dem Sie Inhalt vorab laden möchten, und kopieren Sie die Datenpakete zu den Freigaben auf dem gehosteten Cacheserver.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [Importieren von Datenpaketen auf dem gehosteten Cacheserver & #40; Optional & #41; ](9-Bc-Import-Data.md).

