---
title: Installation für Data Center Bridging (DCB) in Windows Server oder Client
description: Dieses Thema enthält Anweisungen zum Installieren von Data Center Bridging in Windows Server oder Windows-Client.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7c20ef027279780181ff176afa39a19f2976c4c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845441"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Installieren von Data Center Bridging \(DCB\) in WindowsServer 2016 oder Windows 10

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema erfahren, wie zum Installieren von DCB in Windows Server 2016 oder Windows 10 verwenden.

## <a name="prerequisites-for-using-dcb"></a>Voraussetzungen für die Verwendung von DCB

Es folgen die Voraussetzungen für die Konfiguration und Verwaltung von DCB.

### <a name="install-a-compatible-operating-system"></a>Installieren Sie ein kompatibles Betriebssystem

Sie können die DCB-Befehle in diesem Handbuch in der folgenden Betriebssysteme verwenden.

- Windows Server (Semi-Annual Channel)
- Windows Server 2016
- Windows 10 \(alle Versionen\)

Eins der folgenden Betriebssysteme enthalten die frühere Versionen von DCB, die nicht mit den Befehlen kompatibel sind, die in der DCB-Dokumentation für Windows Server 2016 und Windows 10 verwendet werden.

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>Hardwareanforderungen

Es folgt eine Liste der hardwareanforderungen für DCB.

- DCB\-fähige Ethernet-Netzwerkadapter\(s\) muss installiert sein, in dem Computer, auf denen Windows Server 2016 DCB bereitstellen.
- DCB\-fähige Hardwareswitches müssen in Ihrem Netzwerk bereitgestellt werden.


## <a name="install-dcb-in-windows-server-2016"></a>Installieren Sie DCB wird in WindowsServer 2016.

Sie können in den folgenden Abschnitten verwenden, um DCB auf einem Computer unter Windows Server 2016 zu installieren.

**Administratoranmeldeinformationen**

Um diese Schritte ausführen zu können, müssen Sie Mitglied werden **Administratoren**.

### <a name="install-dcb-using-windows-powershell"></a>Installieren Sie DCB mithilfe von Windows PowerShell

Sie können das folgende Verfahren verwenden, DCB mithilfe von Windows PowerShell zu installieren.

1. Klicken Sie auf einem Computer unter Windows Server 2016, auf **starten**, per Rechtsklick das Windows PowerShell-Symbol. Ein Menü wird angezeigt. Klicken Sie im Menü auf **weitere**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmeldeinformationen für ein Konto, das über Administratorrechte auf dem Computer verfügt. Windows PowerShell wird mit Administratorrechten geöffnet.
2. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>Installieren Sie DCB mithilfe von Server-Manager

Sie können das folgende Verfahren verwenden, DCB mithilfe von Server-Manager installieren.

>[!NOTE]
>Nach dem Ausführen der erste Schritt in diesem Verfahren die **Vorbemerkungen** auf der Seite hinzufügen von Rollen und Features-Assistent wird nicht angezeigt, wenn Sie zuvor ausgewählt haben **auf dieser Seite standardmäßig überspringen** beim Hinzufügen Rollen und Features-Assistent ausgeführt wurde. Wenn die **Vorbemerkungen** Seite nicht angezeigt wird, aus Schritt 1 mit Schritt 3 fortfahren.

1. Klicken Sie auf DC1 im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.
2. Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.
3. Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.
4. Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.
5. Klicken Sie in **Serverrollen auswählen**auf **Weiter**.
6. In **Funktionen auswählen**im **Features**, klicken Sie auf **Data Center Bridging**. Ein Dialogfeld wird geöffnet, um gefragt, ob Sie DCB erforderliche Features hinzufügen möchten. Klicken Sie auf **Hinzufügen von Funktionen**.
7. In **Funktionen auswählen**, klicken Sie auf **Weiter**. 
8. 7. in **Installationsauswahl bestätigen**, klicken Sie auf **installieren**. Die **Installationsstatus** Seite zeigt den Status während des Installationsvorgangs. Nachdem die Meldung besagt, dass die Installation erfolgreich war, klicken Sie auf **schließen**.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>Konfigurieren Sie den Kerneldebugger, um QoS können \(Optional\)

 Standardmäßig blockiert die Kernel-Debugger NetQos. Unabhängig von der Methode, die Sie zum Installieren von DCB verwendet, wenn Sie einen Kernel-Debugger auf dem Computer installiert haben, müssen Sie konfigurieren den Debugger, um QoS aktiviert und konfiguriert werden, indem Sie den folgenden Befehl ausführen zu können.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Installieren Sie DCB unter Windows 10

Sie können das folgende Verfahren auf einem Windows 10-Computer ausführen.

Um dieses Verfahren auszuführen, müssen Sie Mitglied werden **Administratoren**.

### <a name="install-dcb"></a>Installieren von DCB

1. Klicken Sie auf **starten**, führen Sie einen Bildlauf nach unten, und klicken Sie auf **Windows System**.
2. Klicken Sie auf **Systemsteuerung**. Die **Systemsteuerung** Dialogfeld wird geöffnet.
3. In **Systemsteuerung**, klicken Sie auf **anzeigen, indem Sie**, und klicken Sie dann entweder **große Symbole** oder **kleine Symbole**.
4. Klicken Sie auf **Programme und Funktionen**. Das Dialogfeld "Programme und Funktionen" wird geöffnet.
5. In **Programme und Funktionen**, klicken Sie im linken Bereich auf **Aktivieren von Windows-Funktionen ein- oder ausschalten**. Die **Windows Features** Dialogfeld wird geöffnet.
6. In **Windows Features**, klicken Sie auf **Data Center Bridging**, und klicken Sie dann auf **OK**.

![Aktivieren Sie oder deaktivieren Sie im Dialogfeld Windows-features](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


