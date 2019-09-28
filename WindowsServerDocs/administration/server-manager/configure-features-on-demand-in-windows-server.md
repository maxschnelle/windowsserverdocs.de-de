---
title: Konfigurieren von "Features bei Bedarf" unter Windows Server
description: Server-Manager
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e663bbea-d025-41fa-b16c-c2bff00a88e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f834ca2e4c4acd045ccaeb4f46142dcc0e86f674
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383268"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Konfigurieren von "Features bei Bedarf" unter Windows Server

>Gilt für: Windows Server 2016

In diesem Thema wird beschrieben, wie Featuredateien in einer Features-bei-Bedarf-Konfiguration mithilfe des Cmdlets "Uninstall-WindowsFeature" entfernt werden.

Features bei Bedarf ist ein Feature, das in Windows 8 und Windows Server 2012 eingeführt wurde, mit dem Sie Rollen-und Featuredateien (manchmal auch als Funktions *Nutzlast*bezeichnet) aus dem Betriebssystem entfernen können, um Speicherplatz zu sparen, und Rollen und Features aus installieren. Remote Standorte oder Installationsmedien anstelle von lokalen Computern. Sie können Featuredateien von ausgeführten physischen und virtuellen Computern entfernen. Sie können Featuredateien Windows-Imagedateien (WIM) oder offline geschalteten virtuellen Festplatten (VHDs) hinzufügen oder von diesen entfernen, um eine reproduzierbare Kopie von „Features bei Bedarf“-Konfigurationen zu erstellen.

Wenn in einer Features-bei-Bedarf-Konfiguration Featuredateien auf einem Computer nicht verfügbar sind und eine Installation diese Featuredateien erfordert, kann Windows Server 2012 R2 oder Windows Server 2012 angewiesen werden, die Dateien aus einem parallelen Funktions Speicher (einem freigegebenen Ordner) zu erhalten. , das Featuredateien enthält und für den Computer im Netzwerk verfügbar ist, von Windows Update oder vom Installationsmedium. Wenn Featuredateien nicht auf dem Zielserver verfügbar sind, sucht die Funktion "Features bei Bedarf" nach fehlenden Featuredateien, indem die folgenden Schritte in der angegebenen Reihenfolge erfolgen.

1.  Durchsuchen eines Speicher Orts, der von Benutzern des Assistenten zum Hinzufügen von Rollen und Features oder von "-Installations Befehlen" angegeben wurde

2.  Auswerten der Konfiguration der Gruppenrichtlinie Einstellung, **Computerkonfiguration\Administrative vorlagen\system\einstellungen für die Installation optionaler Komponenten und die Reparatur von Komponenten angeben**

3.  Durchsuchen von Windows Update

Sie können das standardmäßige Features-bei-Bedarf-Verhalten über eine der folgenden Aktionen überschreiben.

-   Angeben eines anderen Quellpfads als Teil des Cmdlets `Install-WindowsFeature` durch Hinzufügen des `Source` -Parameters

-   Angeben eines alternativen Quell Pfads auf der Seite **Installationsoptionen bestätigen** während der Installation von Features mithilfe des Assistenten zum Hinzufügen von Rollen und Features

-   Konfigurieren der Gruppenrichtlinieneinstellung **Einstellungen für die Installation optionaler Komponenten und die Reparatur von Komponenten angeben**

Dieses Thema enthält die folgenden Abschnitte:

-   [Erstellen einer Featuredatei oder eines parallelen Stores](#BKMK_store)

-   [Methoden zum Entfernen von Featuredateien](#BKMK_methods)

-   [Entfernen von Featuredateien mithilfe von "Uninstall-Windows Feature"](#BKMK_remove)

## <a name="BKMK_store"></a>Erstellen einer Featuredatei oder eines parallelen Stores
In diesem Abschnitt wird das Einrichten eines freigegebenen Remote Ordners für Featuredateien beschrieben, in dem die Dateien gespeichert werden, die zum Installieren von Rollen, Rollen Diensten und Features auf Servern, auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, erforderlich sind. Nachdem Sie einen featurespeicher eingerichtet haben, können Sie Rollen, Rollen Dienste und Features auf Servern mit diesen Betriebssystemen installieren und den featurespeicher als Speicherort der Installations Quelldateien angeben.

#### <a name="to-create-a-feature-file-store"></a>So erstellen Sie einen Speicher für Featuredateien

1.  Erstellen Sie auf einem Server im Netzwerk einen freigegebenen Ordner. Beispielsweise *\\ \ network\share\sxs*.

2.  Vergewissern Sie sich, dass Sie über die ordnungsgemäßen Berechtigungen für den Featurespeicher verfügen. Der Quellpfad oder die Dateifreigabe muss entweder der Gruppe **jeder** (nicht empfohlen aus Sicherheitsgründen) oder den Computer Konten (*Domäne*\\*Servername*$) der Server, auf denen Sie die Installation planen, **Lese** Berechtigungen erteilen. Features mithilfe dieses featurestores das Gewähren des Benutzerkonto Zugriffs ist nicht ausreichend.

    Sie können auf Einstellungen zu Dateifreigaben und Berechtigungen über eine der folgenden Aktionen auf dem Windows-Desktop zugreifen.

    -   Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner, klicken Sie auf **Eigenschaften**, und ändern Sie anschließend auf der Registerkarte **Sicherheit** die zulässigen Benutzer und ihre Zugriffsrechte.

    -   Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner, zeigen Sie auf **Freigeben für**, und klicken Sie anschließend auf **Bestimmte Personen**.

    > [!NOTE]
    > Server in Arbeitsgruppen können nicht auf externe Dateifreigaben zugreifen, auch wenn das Computerkonto des Arbeitsgruppenservers für die externe Freigabe über die Berechtigung **Lesen** verfügt. Alternative Quellspeicherorte, die für Arbeitsgruppenserver funktionieren, sind u. a. Installationsmedien, Windows Update sowie VHD- oder WIM-Dateien, die auf dem lokalen Arbeitsgruppenserver gespeichert sind.

3.  Kopieren Sie den Ordner **Sources\SxS** vom Installationsmedium von Windows Server in den freigegebenen Ordner, den Sie in Schritt 1 erstellt haben.

## <a name="BKMK_methods"></a>Methoden zum Entfernen von Featuredateien
Es gibt zwei Möglichkeiten zum Entfernen von Featuredateien aus Windows Server in einer „Features bei Bedarf“-Konfiguration.

-   Der Parameter "`remove`" des Cmdlets "`Uninstall-WindowsFeature`" ermöglicht das Löschen von Featuredateien von einem Server oder einer offline geschalteten virtuellen Festplatte (VHD), auf dem Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Gültige Werte für den `remove`-Parameter sind die Namen von Rollen, Rollen Diensten und Features.

-   DISM-Befehle (Deployment Image Servicing and Management, Abbildverwaltung für die Bereitstellung) ermöglichen das Erstellen benutzerdefinierter WIM-Dateien zum Einsparen von Festplattenspeicher, indem Featuredateien weggelassen werden, die entweder nicht benötigt werden oder aus anderen Remotequellen abgerufen werden können. Weitere Informationen zum Vorbereiten benutzerdefinierter Images mit DISM finden Sie unter [How to Enable or Disable Windows Features](https://technet.microsoft.com/library/hh824822.aspx).

## <a name="BKMK_remove"></a>Entfernen von Featuredateien mithilfe von "Uninstall-Windows Feature"
Mit dem Cmdlet "Uninstall-Windows Feature" können Sie sowohl Rollen, Rollen Dienste und Features von Servern als auch offline-VHDs, auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, deinstallieren und Featuredateien löschen. Wenn gewünscht, können Sie dieselben Rollen, Rollen Dienste und Features im gleichen Befehl deinstallieren und löschen.

> [!IMPORTANT]
> Wenn Sie Featuredateien für eine Rolle, einen Rollen Dienst oder eine Funktion löschen, werden Rollen, Rollen Dienste und Features, die von den Dateien abhängen, die Sie entfernen, ebenfalls gelöscht. Wenn Sie Featuredateien für einen Rollendienst oder Unterfeature löschen und keine anderen Rollendienste oder Unterfeatures für die übergeordnete Rolle bzw. das übergeordnete Feature installiert sind, werden Dateien für die gesamte übergeordnete Rolle bzw. das gesamte übergeordnete Feature gelöscht. Fügen Sie zum Anzeigen aller Features, die durch den Befehl `Uninstall-WindowsFeature -remove` gelöscht würden, den `whatif`-Parameter dem Befehl hinzu, um diesen auszuführen und Ergebnisse anzuzeigen, ohne Featuredateien tatsächlich zu löschen.

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>So entfernen Sie Rollen- und Featuredateien mithilfe von "Uninstall-WindowsFeature"

1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.

    > [!NOTE]
    > Wenn Sie Rollen und Features von einem Remote Server deinstallieren, müssen Sie Windows PowerShell nicht mit erhöhten Benutzerrechten ausführen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie im Windows- **Start** Bildschirm mit der rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

    -   Geben Sie auf einem Server, auf dem die Server Core-Installationsoption ausgeführt wird, **PowerShell** in die Eingabeaufforderung ein, und drücken Sie dann die **Eingabe**Taste.

2.  Geben Sie Folgendes ein, und drücken Sie dann dieEINGABETASTE.

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **Beispiel** „Remotedesktoplizenzierung“ ist der letzte verbleibende Rollendienst der installierten Remotedesktopdienste. Der Befehl deinstalliert "Remotedesktoplizenzierung" und anschließend die Featuredateien der gesamten Rolle "Remotedesktopdienste" vom angegebenen Server *contoso_1*.

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **Beispiel** Im folgenden Beispiel entfernt der Befehl Active Directory-Domänen Dienste und Gruppenrichtlinie Verwaltung von einer Offline-VHD. Zunächst werden die Rolle und das Feature deinstalliert. Anschließend werden die Featuredateien vollständig von der Offline-VHD *Contoso.vhd* entfernt.

    > [!NOTE]
    > Sie müssen den Parameter "`computerName`" hinzufügen, wenn Sie das Cmdlet auf einem Computer mit Windows 8.1 oder Windows 8 ausführen.
    > 
    > Wenn Sie den Namen einer VHD-Datei auf einer Netzwerkfreigabe eingeben, muss diese Freigabe dem Computer Konto des Servers, den Sie zum Einbinden der VHD ausgewählt haben, **Lese** -und **Schreib** Berechtigungen erteilen. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>Siehe auch
[Installieren oder Deinstallieren von Rollen, Rollen Diensten oder Features](install-or-uninstall-roles-role-services-or-features.md)
[Windows Server-Installationsoptionen](https://technet.microsoft.com/library/hh831786.aspx)
[Aktivieren oder Deaktivieren von Windows-Features](https://technet.microsoft.com/library/hh824822.aspx)
[Bereitstellung Abbild Wartung und-Verwaltung (Übersicht)](https://technet.microsoft.com/library/hh825236.aspx)


