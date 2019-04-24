---
title: Konfigurieren von "Features bei Bedarf" unter Windows Server
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c77bd088a02d405b17a4f7decd6093785296d5e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818931"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Konfigurieren von "Features bei Bedarf" unter Windows Server

>Gilt für: Windows Server 2016

In diesem Thema wird beschrieben, wie Featuredateien in einer Features-bei-Bedarf-Konfiguration mithilfe des Cmdlets "Uninstall-WindowsFeature" entfernt werden.

Features bei Bedarf ist ein Feature, eingeführt in Windows 8 und Windows Server 2012, die Ihnen ermöglicht, entfernen Sie Rollen-und featuredateien (auch als Features bezeichnet *Nutzlast*) vom Betriebssystem zum Einsparen von Speicherplatz, und Installieren von Rollen und Features von Remotestandorten oder Installationsmedien aus anstatt mithilfe lokaler Computer. Sie können Featuredateien von ausgeführten physischen und virtuellen Computern entfernen. Sie können Featuredateien Windows-Imagedateien (WIM) oder offline geschalteten virtuellen Festplatten (VHDs) hinzufügen oder von diesen entfernen, um eine reproduzierbare Kopie von „Features bei Bedarf“-Konfigurationen zu erstellen.

In einer Features-bei-Bedarf-Konfiguration featuredateien nicht auf einem Computer verfügbar, wenn eine Installation diese featuredateien jedoch benötigt sind kann Windows Server 2012 R2 oder Windows Server 2012 geleitet werden, die Dateien aus einem Seite-an-Seite featurespeicher (einem freigegeben Ordner abzurufen. die featuredateien, und auf dem Computer im Netzwerk verfügbar ist), Windows Update oder vom Installationsmedium. Wenn Featuredateien nicht auf dem Zielserver verfügbar sind, sucht die Funktion "Features bei Bedarf" nach fehlenden Featuredateien, indem die folgenden Schritte in der angegebenen Reihenfolge erfolgen.

1.  Durchsuchen eines Speicherorts, der von den Benutzern das Hinzufügen von Rollen und Features-Assistenten oder DISM-installationsbefehlen angegeben wurde

2.  Überprüfen der Konfiguration der Einstellung der Gruppenrichtlinie, **Computerkonfiguration\Administrative vorlagen\system\einstellungen für die Installation optionaler Komponenten und Reparatur von Komponenten**

3.  Durchsuchen von Windows Update

Sie können das standardmäßige Features-bei-Bedarf-Verhalten über eine der folgenden Aktionen überschreiben.

-   Angeben eines anderen Quellpfads als Teil des Cmdlets `Install-WindowsFeature` durch Hinzufügen des `Source` -Parameters

-   Angeben eines anderen Quellpfads auf der **Installationsoptionen bestätigen** Seite während der Installation von Features mithilfe des Hinzufügen von Rollen und Features-Assistenten

-   Konfigurieren der Gruppenrichtlinieneinstellung **Einstellungen für die Installation optionaler Komponenten und die Reparatur von Komponenten angeben**

Dieses Thema enthält die folgenden Abschnitte:

-   [Erstellen Sie eine Featuredatei oder eine Seite-an-Seite-Speicher](#BKMK_store)

-   [Methoden zum Entfernen von featuredateien](#BKMK_methods)

-   [Entfernen von featuredateien mithilfe des Uninstall-WindowsFeature](#BKMK_remove)

## <a name="BKMK_store"></a>Erstellen Sie eine Featuredatei oder eine Seite-an-Seite-Speicher
Dieser Abschnitt beschreibt, wie Sie einen remote-Funktion freigegebenen Ordner (auch als einen Seite-an-Seite-Speicher) einrichten, die speichert die Dateien, die zum Installieren von Rollen, Rollendienste und Features auf Servern mit Windows Server 2012 R2 oder Windows Server 2012 erforderlich. Nachdem Sie einen featurespeicher eingerichtet haben, können Sie Rollen, Rollendienste und Features auf Servern unter diesen Betriebssystemen installieren und den featurespeicher als Speicherort der Installationsquelldateien angeben.

#### <a name="to-create-a-feature-file-store"></a>So erstellen Sie einen Speicher für Featuredateien

1.  Erstellen Sie auf einem Server im Netzwerk einen freigegebenen Ordner. Z. B.  *\\\network\share\sxs*.

2.  Vergewissern Sie sich, dass Sie über die ordnungsgemäßen Berechtigungen für den Featurespeicher verfügen. Muss die Quelle oder die Dateifreigabe gewähren **lesen** Berechtigungen entweder auf die **jeder** (nicht empfohlen aus Sicherheitsgründen), Gruppe oder den Computerkonten (*Domäne* \\ *SERverNAME*$) der Server, auf dem Sie Features mithilfe des featurespeichers installieren möchten, benutzerkontenzugriff zu gewähren, ist nicht ausreichend.

    Sie können auf Einstellungen zu Dateifreigaben und Berechtigungen über eine der folgenden Aktionen auf dem Windows-Desktop zugreifen.

    -   Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner, klicken Sie auf **Eigenschaften**, und ändern Sie anschließend auf der Registerkarte **Sicherheit** die zulässigen Benutzer und ihre Zugriffsrechte.

    -   Klicken Sie mit der rechten Maustaste auf den freigegebenen Ordner, zeigen Sie auf **Freigeben für**, und klicken Sie anschließend auf **Bestimmte Personen**.

    > [!NOTE]
    > Server in Arbeitsgruppen können nicht auf externe Dateifreigaben zugreifen, auch wenn das Computerkonto des Arbeitsgruppenservers für die externe Freigabe über die Berechtigung **Lesen** verfügt. Alternative Quellspeicherorte, die für Arbeitsgruppenserver funktionieren, sind u. a. Installationsmedien, Windows Update sowie VHD- oder WIM-Dateien, die auf dem lokalen Arbeitsgruppenserver gespeichert sind.

3.  Kopieren Sie den Ordner **Sources\SxS** vom Installationsmedium von Windows Server in den freigegebenen Ordner, den Sie in Schritt 1 erstellt haben.

## <a name="BKMK_methods"></a>Methoden zum Entfernen von featuredateien
Es gibt zwei Möglichkeiten zum Entfernen von Featuredateien aus Windows Server in einer „Features bei Bedarf“-Konfiguration.

-   Die `remove` Parameter, der die `Uninstall-WindowsFeature` Cmdlet können Sie das Löschen von featuredateien von einem Server oder einer offline geschalteten virtuellen Festplatte (VHD), auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Gültige Werte für die `remove` Parameter sind die Namen der Rollen, Rollendienste und Features.

-   DISM-Befehle (Deployment Image Servicing and Management, Abbildverwaltung für die Bereitstellung) ermöglichen das Erstellen benutzerdefinierter WIM-Dateien zum Einsparen von Festplattenspeicher, indem Featuredateien weggelassen werden, die entweder nicht benötigt werden oder aus anderen Remotequellen abgerufen werden können. Weitere Informationen zum Vorbereiten benutzerdefinierter Images mit DISM finden Sie unter [How to Enable or Disable Windows Features](https://technet.microsoft.com/library/hh824822.aspx).

## <a name="BKMK_remove"></a>Entfernen von featuredateien mithilfe des Uninstall-WindowsFeature
Sie können das Cmdlet "Uninstall-WindowsFeature" verwenden, sowohl zum Deinstallieren von Rollen, Rollendienste und Features von Servern und offline-VHDs, die Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden, und featuredateien löschen. Sie können sowohl deinstallieren und löschen ggf. die gleichen Rollen, Rollendienste und Features im selben Befehl.

> [!IMPORTANT]
> Wenn Sie featuredateien für eine Rolle löschen, werden Rollendienst oder Feature, Rollen, Rollendienste und Features, die die Dateien abhängig, die Sie entfernen möchten, ebenfalls gelöscht. Wenn Sie Featuredateien für einen Rollendienst oder Unterfeature löschen und keine anderen Rollendienste oder Unterfeatures für die übergeordnete Rolle bzw. das übergeordnete Feature installiert sind, werden Dateien für die gesamte übergeordnete Rolle bzw. das gesamte übergeordnete Feature gelöscht. Fügen Sie zum Anzeigen aller Features, die durch den Befehl `Uninstall-WindowsFeature -remove` gelöscht würden, den `whatif`-Parameter dem Befehl hinzu, um diesen auszuführen und Ergebnisse anzuzeigen, ohne Featuredateien tatsächlich zu löschen.

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>So entfernen Sie Rollen- und Featuredateien mithilfe von "Uninstall-WindowsFeature"

1.  Führen Sie einen der folgenden Schritte aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.

    > [!NOTE]
    > Wenn Sie Rollen und Features von einem Remoteserver aus deinstallieren möchten, müssen Sie nicht zum Ausführen von Windows PowerShell mit erhöhten Benutzerrechten.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie auf der Windows **starten** Bildschirm rechten Maustaste auf die Kachel Windows PowerShell, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.

    -   Geben Sie auf einem Server, auf denen die Server Core-Installationsoption ausgeführt wird, **PowerShell** an einer Eingabeaufforderung, und drücken Sie dann die **EINGABETASTE**.

2.  Geben Sie Folgendes ein, und drücken Sie dann die **** EINGABETASTE.

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **Beispiel:** „Remotedesktoplizenzierung“ ist der letzte verbleibende Rollendienst der installierten Remotedesktopdienste. Der Befehl deinstalliert "Remotedesktoplizenzierung" und anschließend die Featuredateien der gesamten Rolle "Remotedesktopdienste" vom angegebenen Server *contoso_1*.

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **Beispiel:** Im folgenden Beispiel entfernt der Befehl active Directory-Domänendienste und Gruppenrichtlinienverwaltung von einer offline-VHD an. Zunächst werden die Rolle und das Feature deinstalliert. Anschließend werden die Featuredateien vollständig von der Offline-VHD *Contoso.vhd* entfernt.

    > [!NOTE]
    > Sie müssen hinzufügen, die `computerName` -Parameters, wenn Sie dem Cmdlet auf einem Computer, die ausgeführt werden für Windows 8.1 oder Windows 8 ausgeführt wird.
    > 
    > Wenn Sie den Namen einer VHD-Datei von einer Netzwerkfreigabe eingeben, muss die Freigabe gewähren **lesen** und **schreiben** Berechtigungen für das Computerkonto des Servers, der zum Einbinden der VHD ausgewählt. Die Zugriffsberechtigungen des Benutzerkontos reichen nicht aus. Die Freigabe kann der Gruppe **Jeder** die Berechtigungen **Lesen** und **Schreiben** gewähren, um den Zugriff auf die VHD zu ermöglichen, dies wird aber aus Sicherheitsgründen nicht empfohlen.

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>Siehe auch
[Installieren oder Deinstallieren von Rollen, Rollendienste oder Features](install-or-uninstall-roles-role-services-or-features.md)
[Windows Server-Installationsoptionen](https://technet.microsoft.com/library/hh831786.aspx)
[aktivieren oder Deaktivieren von Windows-Features](https://technet.microsoft.com/library/hh824822.aspx) 
 [Deployment Image Servicing and Management (DISM) – Übersicht](https://technet.microsoft.com/library/hh825236.aspx)


