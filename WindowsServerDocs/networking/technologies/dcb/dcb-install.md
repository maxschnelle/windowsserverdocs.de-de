---
title: Installieren Sie Data Center Bridging (DCB) in Windows Server oder Client
description: In diesem Thema erhalten Sie Anweisungen zum Data Center Bridging in Windows Server oder Windows-Client installieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 491bdeb1a7458be1f991be68724e7a7b51f67ecf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Installieren von Data Center Bridging \(DCB\) in Windows Server 2016 oder Windows10

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie Informationen zum Installieren von DCB in Windows Server2016 oder Windows10.

## <a name="prerequisites-for-using-dcb"></a>Voraussetzungen für die Verwendung von DCB

Es folgen die Voraussetzungen für das Konfigurieren und Verwalten von DCB.

### <a name="install-a-compatible-operating-system"></a>Installieren von einem kompatiblen Betriebssystem

Sie können die DCB-Befehle in diesem Handbuch in den folgenden Betriebssystemen verwenden.

- Windows Server (Semikolons jährlichen Channel)
- Windows Server 2016
- Windows10 \(all Versions\)

Die folgenden Betriebssysteme enthalten die vorherige Versionen von DCB, die nicht kompatibel mit den Befehlen, die in DCB-Dokumentation für Windows Server2016 und Windows10 verwendet werden.

- Windows Server2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>Hardwareanforderungen

Es folgt eine Liste der Hardwareanforderungen für DCB.

- DCB\-fähige Ethernet-Netzwerk Adapter\(s\) muss auf Computern installiert werden, für die Windows Server2016 DCB bereitgestellt werden.
- DCB\-fähige Hardwareswitches müssen in Ihrem Netzwerk bereitgestellt werden.


## <a name="install-dcb-in-windows-server-2016"></a>Installieren Sie DCB in Windows Server 2016

In den folgenden Abschnitten können Sie um DCB auf einem Computer unter Windows Server2016 installieren.

**Administrative Anmeldeinformationen**

Zum Ausführen dieser Verfahren müssen Sie Mitglied der sein **Administratoren**.

### <a name="install-dcb-using-windows-powershell"></a>Installieren Sie DCB mithilfe von WindowsPowerShell

Das folgende Verfahren können DCB mithilfe von Windows PowerShell installieren.

1. Klicken Sie auf einem Computer unter Windows Server2016, auf **starten**, anschließend mit der Maustaste des Windows PowerShell-Symbol. Ein Menü angezeigt wird. Klicken Sie im Menü auf **weitere**, und klicken Sie dann auf **als Administrator ausführen**. Wenn Sie dazu aufgefordert werden, geben Sie die Anmeldeinformationen für ein Konto mit Administratorrechten auf dem Computer. Windows PowerShell wird mit Administratorrechten geöffnet.
2. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>Installieren Sie DCB mit Server-Manager

Das folgende Verfahren können Sie DCB mithilfe von Server-Manager installieren.

>[!NOTE]
>Nach dem Durchführen der erste Schrittin diesem Verfahren der **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde. Wenn die **Vorbemerkungen** Seite nicht angezeigt wird, fahren Sie mit Schritt3 aus Schritt1.

1. Klicken Sie auf DC1 im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.
2. In **Vorbemerkungen**, klicken Sie auf **Weiter**.
3. In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.
4. In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.
5. In **Serverrollen auswählen**, klicken Sie auf **Weiter**.
6. In **Features auswählen**im **Features**, klicken Sie auf **Data Center Bridging**. Ein Dialogfeld geöffnet, wenn Sie gefragt, ob Sie DCB erforderliche Features hinzufügen möchten. Klicken Sie auf **Hinzufügen von Features**.
7. In **Features auswählen**, klicken Sie auf **Weiter**. 
8. 7. In **Installationsauswahl bestätigen**, klicken Sie auf **installieren**. Die **Installationsstatus** Seite zeigt den Status während der Installation. Nachdem die Meldung angezeigt, dass wird die Installation erfolgreich war, klicken Sie auf **schließen**.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>Konfigurieren des Kerneldebuggers QoS \(Optional\) zulassen

 In der Standardeinstellung blockieren Kernel-Debugger NetQos. Unabhängig von der Methode, die Sie zum DCB, installieren, wenn Sie einen Kerneldebugger auf dem Computer installiert haben, müssen Sie konfigurieren den Debugger, um QoS aktiviert und konfiguriert werden, indem Sie den folgenden Befehl ausführen können.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Installieren Sie DCB in Windows10

Sie können das folgende Verfahren auf einem Windows10-Computer ausführen.

Zum Ausführen dieses Verfahrens müssen Sie Mitglied der sein **Administratoren **.

### <a name="install-dcb"></a>Installieren Sie DCB

1. Klicken Sie auf **starten**, führen Sie einen Bildlauf nach unten, und klicken Sie auf **Windows-System **.
2. Klicken Sie auf **Systemsteuerung **. Die **Systemsteuerung** Dialogfeld wird geöffnet.
3. In **Systemsteuerung**, klicken Sie auf **anzeigen, indem Sie**, und klicken Sie dann auf **große Symbole** oder **kleine Symbole **.
4. Klicken Sie auf **Programme und Funktionen **. Das Dialogfeld "Programme und Funktionen" wird geöffnet.
5. In **Programme und Funktionen**, klicken Sie im linken Bereich auf **Windows-Funktionen ein- oder ausschalten **. Die **Windows-Features** Dialogfeld wird geöffnet.
6. In **Windows-Features**, klicken Sie auf **Data Center Bridging**, und klicken Sie dann auf **OK **.

![Aktivieren Sie oder deaktivieren Sie im Dialogfeld der Windows-Features](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


