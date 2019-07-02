---
title: Hochladen eines spezialisierten Windows Server 2008/2008 R2-Images auf Azure
description: Windows Server 2008 und 2008 R2 werden demnächst eingestellt. Erfahren Sie, wie Sie sie auf Azure auslagern können, indem Sie Windows Server in der Cloud hosten.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/11/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 425197d3462762c60a7371fc6ca529ad1b70e7ef
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66443370"
---
# <a name="upload-a-windows-server-20082008-r2-specialized-image-to-azure"></a>Hochladen eines spezialisierten Windows Server 2008/2008 R2-Images auf Azure 

![Bildthema mit Banner zur Einführung von WS08](media/WS08-image-banner-large.png)

Sie können mit Azure nun eine Windows Server 2008/2008 R2-VM in der Cloud ausführen. 

## <a name="prep-the-windows-server-20082008-r2-specialized-image"></a>Vorbereiten des spezialisierten Windows Server 2008/2008 R2-Images
Bevor Sie ein Image hochladen können, nehmen Sie die folgenden Änderungen vor:

- Laden Sie Windows Server 2008 Service Pack 2 (SP2) herunter, und installieren Sie es, sofern es in Ihrem Image nicht bereits installiert ist.

- Konfigurieren Sie die Einstellungen für Remotedesktop (RDP).
  1. Wechseln Sie zu **Systemsteuerung** > **Systemeinstellungen**.   
  2. Wählen Sie im linken Menü **Remote-Einstellungen** aus.

     ![Screenshot der Systemeinstellungen, mit Hervorhebung von „Remote-Einstellungen“.](media/1a_remote_settings.png)

  3. Wählen Sie in den Systemeigenschaften die Registerkarte **Remote** aus.   

     ![Screenshot der Registerkarte „Remote“ in den Systemeigenschaften.](media/2c_sysprops.png)

  4. Wählen Sie „Verbindungen von Computern zulassen, auf denen eine beliebige Version von Remotedesktop ausgeführt wird (weniger Sicherheit)“ aus.   
  5. Klicken Sie auf **Übernehmen** und dann auf **OK**.
- Konfigurieren Sie die Windows-Firewall-Einstellungen.   
   1. Geben Sie an der Eingabeaufforderung im Administratormodus „**wf.msc**“ für Windows-Firewall und erweiterte Sicherheitseinstellungen ein.   
   2. Sortieren Sie die Ergebnisse nach **Ports**, und wählen Sie **Port 3389** aus.   
     ![Screenshot der eingehenden Regeln in den Windows-Firewall-Einstellungen.](media/3b_inboundrules.png)   
   3. Aktivieren Sie Remotedesktop (TCP-IN) für die Profile: **Domäne**, **Privat** und **Öffentlich** (siehe oben).

- Speichern Sie alle Einstellungen, und fahren Sie das Image herunter.   
- Wenn Sie Hyper-V verwenden, stellen Sie sicher, dass die untergeordnete AVHD für dauerhafte Änderungen mit der übergeordneten virtuellen Festplatte zusammengeführt wird.

Ein bekannter aktueller Fehler bewirkt, dass das Administratorkennwort auf dem hochgeladenen Image innerhalb von 24 Stunden abläuft. Führen Sie die folgenden Schritte aus, um dieses Problem zu umgehen: 

1. Wechseln Sie zu **Start** > **Ausführen**.
2. Geben Sie **lusrmgr.msc** ein.
3. Wählen Sie unter „Lokale Benutzer und Gruppen“ **Benutzer** aus.
4. Klicken Sie mit der rechten Maustaste auf **Administrator**, und wählen Sie **Eigenschaften** aus.
5. Wählen Sie **Kennwort läuft nie ab** und anschließend **OK** aus. 
![Screenshot der Administratoreigenschaften.](media/6_adminprops.png)

## <a name="uploading-the-image-vhd"></a>Hochladen der Image-VHD
Sie können die virtuelle Festplatte anhand des folgenden Skripts hochladen. Zuvor benötigen Sie jedoch die Publish-Einstellungsdatei für Ihr Azure-Konto. Rufen Sie die [Azure-Dateieinstellungen](https://azure.microsoft.com/downloads/) ab.

Dies ist das Skript:

```powershell
Get-AzurePublishSettingsFile 

Login-AzureRmAccount
 
      # Import publishsettings
      Import-AzurePublishSettingsFile -PublishSettingsFile <LocationOfPublishingFile>
      $subscriptionId = 'xxxx-xxxx-xxxx-xxxx-xxxxx'
 
      # Set NodeFlight subscription as default subscription
      Select-AzureRmSubscription -SubscriptionId $subscriptionId
      Set-AzureRmContext -SubscriptionId $subscriptionId
      $rgName = "<resourcegroupname>"
    
      $urlOfUploadedImageVhd = "<BlobUrl>/<NameForVHD>.vhd"
      Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd -LocalFilePath "<FilePath>"  
```
## <a name="deploy-the-image-in-azure"></a>Bereitstellen des Images auf Azure
In diesem Abschnitt stellen Sie die Image-VHD auf Azure bereit. 

> [!IMPORTANT]
> Verwenden Sie auf Azure keine vordefinierten Benutzer-Images.

1.  Erstellen Sie eine neue [Ressourcengruppe](https://docs.microsoft.com/rest/api/resources/resourcegroups/createorupdate). 
2.  Erstellen Sie innerhalb der Ressourcengruppe ein neues [Speicherblob](https://docs.microsoft.com/rest/api/storageservices/put-blob).
3.  Erstellen Sie innerhalb des Speicherblobs einen [Container](https://docs.microsoft.com/rest/api/storageservices/create-container).
4.  Kopieren Sie die URL des Blobspeichers aus den Eigenschaften.
5.  Verwenden Sie das oben bereitgestellte Skript, um Ihr Image in das neue Speicherblob hochzuladen.
6.  Erstellen Sie einen [Datenträger](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image) für Ihre virtuelle Festplatte.   
     a. Wechseln Sie zu „Datenträger“, und klicken Sie auf **Hinzufügen**.  
     b. Geben Sie einen Namen für den Datenträger ein. Wählen Sie das Abonnement aus, das Sie verwenden möchten, legen Sie die Region fest, und wählen Sie den Kontotyp aus.   
     c. Wählen Sie für den Quelltyp „Speicher“ aus. Navigieren Sie anhand des Skripts zum Speicherort der Blob-VHD.  
     d. Wählen Sie den Betriebssystemtyp „Windows“ und die Größe „(Standard: 1023)“ aus.   
     e. Klicken Sie auf **Erstellen**.   

7.  Wechseln Sie zum erstellten Datenträger, und klicken Sie auf **VM erstellen**.   
     a. Benennen Sie die VM.   
     b. Wählen Sie die vorhandene Gruppe aus, die Sie in Schritt 5 erstellt und in die Sie den Datenträger hochgeladen haben.   
     c. Wählen Sie eine Größe und einen SKU-Plan für Ihre VM aus.   
     d. Wählen Sie auf der Seite „Einstellungen“ eine Netzwerkschnittstelle aus. Stellen Sie sicher, dass bei der Netzwerkschnittstelle die folgende Regel angegeben wurde:
 
        PORT:3389 Protocol: TCP Action: Allow Priority: 1000 Name: ‘RDP-Rule’.   
     e. Klicken Sie auf **Erstellen**.




