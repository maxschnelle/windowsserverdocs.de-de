---
title: Installieren von Data Center Bridging (DCB) in Windows Server oder Client
description: Dieses Thema enthält Anweisungen zum Installieren von Data Center Bridging in Windows Server oder Windows-Client.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: edca8269178d9e1de9f8d57abac04400da0ac5c1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312801"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Installieren von Data Center Bridging \(DCB-\) in Windows Server 2016 oder Windows 10

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie DCB in Windows Server 2016 oder Windows 10 installieren.

## <a name="prerequisites-for-using-dcb"></a>Voraussetzungen für die Verwendung von DCB

Im folgenden finden Sie die Voraussetzungen für das Konfigurieren und Verwalten von DCB.

### <a name="install-a-compatible-operating-system"></a>Installieren eines kompatiblen Betriebssystems

Sie können die DCB-Befehle in diesem Handbuch unter den folgenden Betriebssystemen verwenden.

- Windows Server (Semi-Annual Channel)
- Windows Server 2016
- Windows 10 \(alle Versionen\)

Die folgenden Betriebssysteme enthalten frühere Versionen von DCB, die nicht mit den Befehlen kompatibel sind, die in der DCB-Dokumentation für Windows Server 2016 und Windows 10 verwendet werden.

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>Hardwareanforderungen

Im folgenden finden Sie eine Liste der Hardwareanforderungen für DCB.

- Der DCB-\-fähige Ethernet-Netzwerkadapter\(s\) muss auf Computern installiert sein, die Windows Server 2016 DCB bereitstellen.
- DCB-\-fähige Hardware Switches müssen in Ihrem Netzwerk bereitgestellt werden.


## <a name="install-dcb-in-windows-server-2016"></a>Installieren von DCB in Windows Server 2016

In den folgenden Abschnitten finden Sie Informationen zum Installieren von DCB auf einem Computer mit Windows Server 2016.

**Administrator Anmelde Informationen**

Um diese Prozeduren ausführen zu können, müssen Sie Mitglied der Gruppe " **Administratoren**" sein.

### <a name="install-dcb-using-windows-powershell"></a>Installieren von DCB mithilfe von Windows PowerShell

Sie können das folgende Verfahren verwenden, um DCB mithilfe von Windows PowerShell zu installieren.

1. Klicken Sie auf einem Computer unter Windows Server 2016 auf **Start**, und klicken Sie dann mit der rechten Maustaste auf das Windows PowerShell-Symbol. Ein Menü wird angezeigt. Klicken Sie im Menü auf **mehr**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmelde Informationen eines Kontos ein, das über Administrator Rechte auf dem Computer verfügt. Windows PowerShell wird mit Administrator Rechten geöffnet.
2. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>Installieren von DCB mithilfe von Server-Manager

Mithilfe des folgenden Verfahrens können Sie DCB mithilfe von Server-Manager installieren.

>[!NOTE]
>Nachdem Sie den ersten Schritt in dieser Prozedur ausgeführt haben, wird die Seite **Vorbemerkungen** des Assistenten zum Hinzufügen von Rollen und Features nicht angezeigt, wenn Sie zuvor diese Seite beim Ausführen des Assistenten zum Hinzufügen von Rollen und Features **standardmäßig überspringen** ausgewählt haben. Wenn die Seite **Vorbemerkungen** nicht angezeigt wird, überspringen Sie von Schritt 1 zu Schritt 3.

1. Klicken Sie auf DC1 in Server-Manager auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.
2. Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.
3. Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.
4. Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.
5. Klicken Sie in **Serverrollen auswählen**auf **Weiter**.
6. Klicken Sie unter Features **auswählen**in **Features**auf **Data Center Bridging**. Es wird ein Dialogfeld geöffnet, in dem Sie gefragt werden, ob Sie DCB erforderliche Features hinzufügen möchten. Klicken Sie auf **Features hinzufügen**.
7. Klicken Sie unter **Features auswählen**auf **weiter**. 
8. 7.in **Installations Auswahl bestätigen**, klicken Sie auf **Installieren**. Auf der Seite **Installationsfortschritt** wird während des Installationsvorgangs der Status angezeigt. Wenn die Meldung angezeigt wird, dass die Installation erfolgreich war, klicken Sie auf **Schließen**.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>Konfigurieren Sie den Kernel Debugger so, dass QoS \(optional ist\)

 Standardmäßig blockieren Kernel-Debug-Geräte NetQoS. Unabhängig von der Methode, die Sie zum Installieren von DCB verwendet haben, müssen Sie den Debugger so konfigurieren, dass die Aktivierung und Konfiguration von QoS durch Ausführen des folgenden Befehls möglich ist, wenn ein Kernel Debugger auf dem Computer installiert ist.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Installieren von DCB in Windows 10

Sie können das folgende Verfahren auf einem Windows 10-Computer ausführen.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Administratoren**" sein.

### <a name="install-dcb"></a>Installieren von DCB

1. Klicken Sie auf **Start**, Scrollen Sie nach unten, und klicken Sie auf **Windows-System**.
2. Klicken Sie auf **Systemsteuerung**. Das Dialogfeld **Systemsteuerung** wird geöffnet.
3. Klicken Sie in der **Systemsteuerung**auf **Anzeigen von**, und klicken Sie dann entweder auf **große Symbole** oder auf **kleine Symbole**.
4. Klicken Sie auf **Programme und Funktionen**. Das Dialogfeld Programme und Funktionen wird geöffnet.
5. Klicken Sie im linken Bereich unter **Programme und Funktionen** **auf Windows-Funktionen ein-oder ausschalten**. Das Dialogfeld **Windows-Funktionen** wird geöffnet.
6. Klicken Sie unter **Windows-Features**auf **Data Center Bridging**, und klicken Sie dann auf **OK**.

![Dialogfeld "Windows-Funktionen ein-oder ausschalten"](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


