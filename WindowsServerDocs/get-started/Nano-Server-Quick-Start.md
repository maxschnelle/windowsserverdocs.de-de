---
title: Nano Server-Schnellstart
description: Schritte zum schnellen Bereitstellen einer einfachen Nano Server-Instanz auf einem physischen oder virtuellen Computer
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/05/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 488d0bed661cf2078d20e491a8c68b2a29a42b73
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859521"
---
# <a name="nano-server-quick-start"></a>Nano Server-Schnellstart

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Mit dem Beginn von Windows Server, Version 1709 steht Nano Server nur als [Basisimage des Betriebssystems für den Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sehen Sie sich [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahren Sie, was dies bedeutet. 

Führen Sie die Schritte in diesem Abschnitt aus, wenn Sie schnell mit einer einfachen Bereitstellung von Nano Server mithilfe von DHCP zum Abrufen einer IP-Adresse beginnen möchten. Sie können eine Nano Server-VHD entweder auf einem virtuellen Computer ausführen oder von einem physischen Computer aus starten. Die Schritte unterscheiden sich leicht.

Nachdem Sie die Grundlagen mithilfe dieser Schnellstartschritte ausprobiert haben, finden Sie weitere Informationen zum Erstellen Ihrer eigenen benutzerdefinierten Images, zur Paketverwaltung mithilfe verschiedener Methoden, zu Domänenvorgängen usw. unter [Deploy Nano Server (Bereitstellen von Nano Server)](Deploy-Nano-Server.md).
  
**Nano Server auf einem virtuellen Computer**  
  
Führen Sie diese Schritte aus, um eine Nano Server-VHD zu erstellen, die auf einem virtuellen Computer ausgeführt wird.  
  
## <a name="to-quickly-deploy-nano-server-in-a-virtual-machine"></a>So stellen Sie Nano Server schnell auf einem virtuellen Computer bereit  
  
1.  Kopieren Sie den Ordner *NanoServerImageGenerator* aus dem Ordner „\NanoServer“ in der Windows Server 2016-ISO-Datei in einen Ordner auf Ihrer Festplatte.  
  
2.  Starten Sie Windows PowerShell als Administrator, ändern Sie das Verzeichnis in den Ordner, in dem Sie den Ordner "NanoServerImageGenerator" platziert wurden, und importieren Sie das Modul mit `Import-Module .\NanoServerImageGenerator -Verbose`  
>[!NOTE]  
>Möglicherweise müssen Sie die Windows PowerShell-Ausführungsrichtlinie anpassen. `Set-ExecutionPolicy RemoteSigned` sollte gut funktionieren.  
  
3.  Erstellen Sie eine VHD für die Standardedition, die einen Computernamen festlegt und die Hyper-V-**Gasttreiber** einschließt, indem Sie den folgenden Befehl ausführen, der Sie dazu auffordern wird, ein Administratorkennwort für die neue VHD einzugeben:  
  
    `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhd -ComputerName <computer name>` WHERE  
  
    -   **-MediaPath <Stammverzeichnis des Installationsmediums\>** gibt einen Pfad zum Stamm der Inhalte der Windows Server 2016-ISO-Datei an. Wenn Sie z.B. die Inhalte der ISO-Datei in „d:\TP5ISO“ kopiert haben, würden Sie diesen Pfad verwenden.  
  
    -   **-BasePath** (optional) gibt einen Ordner an, der erstellt wird, um die Nano Server-WIM und -Pakete hinein zu kopieren.  
  
    -   **-TargetPath** gibt einen Pfad an, einschließlich des Dateinamens und der Erweiterung, in dem die resultierende VHD oder VHDX erstellt wird.  
  
    -   **Computer_name** gibt den Computernamen des virtuellen Nano Server-Computers an, den Sie erstellen.  
  
    **Beispiel:** `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1`  
  
    Dieses Beispiel erstellt eine VHD aus einer ISO-DATEI, die als f:\\ bereitgestellt wird. Beim Erstellen der VHD wird ein Ordner namens „Base“ im gleichen Verzeichnis verwendet, in dem New-NanoServerImage ausgeführt wurde. Die VHD („Nano.vhd“ genannt) wird in einem Ordner namens „Nano1“ in dem Ordner abgelegt, von dem aus der Befehl ausgeführt wird. Der Computername wird „Nano1“ lauten. Die resultierende VHD wird die Standardedition von Windows Server 2016 enthalten und für die Bereitstellung eines virtuellen Hyper-V-Computers geeignet sein. Wenn Sie einen virtuellen Computer der Generation 1 möchten, erstellen Sie ein VHD-Image, indem Sie eine **.vhd**-Erweiterung für -TargetPath angeben. Wenn Sie einen virtuellen Computer der Generation 2 möchten, erstellen Sie ein VHDX-Image, indem Sie eine **.vhdx**-Erweiterung für -TargetPath angeben. Sie können auch direkt eine WIM-Datei generieren, indem Sie eine **.wim**-Erweiterung für -TargetPath angeben.  
  
    > [!NOTE]  
    > New-NanoServerImage wird unter Windows 8.1, Windows 10, Windows Server 2012 R2 und Windows Server 2016 unterstützt.  
  
4.  Erstellen Sie in Hyper-V-Manager einen neuen virtuellen Computer, und verwenden Sie die in Schritt 3 erstellte VHD.  
  
5.  Starten Sie den virtuellen Computer, und stellen Sie in Hyper-V-Manager eine Verbindung zum virtuellen Computer her.  
  
6.  Melden Sie sich bei der Wiederherstellungskonsole an (siehe Abschnitt „Nano Server-Wiederherstellungskonsole“ in diesem Leitfaden), indem Sie den Administrator und das Kennwort verwenden, die Sie während der Ausführung des Skripts in Schritt 3 bereitgestellt haben.  
 > [!NOTE]  
    > Die Wiederherstellungskonsole unterstützt nur grundlegende Tastaturfunktionen. Tastaturbeleuchtung, Nummernblöcke und Tastaturlayoutwechsel wie z.B. FESTSTELLTASTE und Num-Lock-Taste werden nicht unterstützt.
  
7.  Fordern Sie die IP-Adresse des virtuellen Nano Server-Computers an, und verwenden Sie Windows PowerShell-Remoting oder andere Remoteverwaltungstools, um eine Verbindung mit dem virtuellen Computer herzustellen und diesen remote zu verwalten.  
  
**Nano Server-Instanz auf einem physischen computer**  
  
Sie können auch eine VHD erstellen, die Nano Server auf einem physischen Computer ausführen wird, indem Sie die vorinstallierten Gerätetreiber verwenden. Wenn Ihre Hardware einen Treiber benötigt, der nicht bereits bereitgestellt ist, um ein Netzwerk zu starten bzw. eine Verbindung mit einem Netzwerk herzustellen, führen Sie die Schritte im Abschnitt „Hinzufügen zusätzlicher Treiber“ dieses Leitfadens aus.  
  
## <a name="to-quickly-deploy-nano-server-on-a-physical-computer"></a>So stellen Sie Nano Server schnell auf einem physischen Computer bereit  
  
1.  Kopieren Sie den Ordner *NanoServerImageGenerator* aus dem Ordner „\NanoServer“ in der Windows Server 2016-ISO-Datei in einen Ordner auf Ihrer Festplatte.  
  
2.  Starten Sie Windows PowerShell als Administrator, ändern Sie das Verzeichnis in den Ordner, in dem Sie den Ordner "NanoServerImageGenerator" platziert wurden, und importieren Sie das Modul mit `Import-Module .\NanoServerImageGenerator -Verbose`  
  
>[!NOTE]  
>Möglicherweise müssen Sie die Windows PowerShell-Ausführungsrichtlinie anpassen. `Set-ExecutionPolicy RemoteSigned` sollte gut funktionieren.  
  
3.  Erstellen Sie eine VHD, die einen Computernamen festlegt und die OEM-Treiber und Hyper-V einschließt, indem Sie den folgenden Befehl ausführen, der Sie dazu auffordern wird, ein Administratorkennwort für die neue VHD einzugeben:  
  
    `New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.vhd -ComputerName <computer name> -OEMDrivers -Compute -Clustering` WHERE  
  
    -   **-MediaPath <Stammverzeichnis des Installationsmediums\>** gibt einen Pfad zum Stamm der Inhalte der Windows Server 2016-ISO-Datei an. Wenn Sie z.B. die Inhalte der ISO-Datei in „d:\TP5ISO“ kopiert haben, würden Sie diesen Pfad verwenden.  
  
    -   **BasePath** gibt einen Ordner an, der erstellt wird, um die Nano Server-WIM und -Pakete hinein zu kopieren (Dieser Parameter ist optional.)  
  
    -   **TargetPath** gibt einen Pfad an, einschließlich des Dateinamens und der Erweiterung, in dem die resultierende VHD oder VHDX erstellt wird.  
  
    -   **Computer_name** ist der Computername der Nano Server-INstanz, die Sie erstellen.  
  
    **Beispiel:**`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers -Compute -Clustering`  
  
    Dieses Beispiel erstellt eine VHD aus einer ISO-DATEI, die als F:\\ bereitgestellt wird. Beim Erstellen der VHD wird ein Ordner namens „Base“ im gleichen Verzeichnis verwendet, in dem New-NanoServerImage ausgeführt wurde. Die VHD wird in einem Ordner namens „Nano1“ in dem Ordner abgelegt, von dem aus der Befehl ausgeführt wird. Der Computername wird „Nano-srv1“ lauten, die OEM-Treiber für die häufigste Hardware werden darauf installiert sein, und die Hyper-V-Rolle sowie die Clustering-Funktion werden aktiviert sein. Die Standard-Nano-Edition wird verwendet.  
  
4.  Melden Sie sich als Administrator auf dem physischen Server an, auf dem Sie die Nano Server-VHD ausführen möchten.  
  
5.  Kopieren Sie die VHD, die dieses Skript erstellt, auf den physischen Computer, und konfigurieren Sie diesen so, dass er von dieser neuen VHD aus gestartet wird. Gehen Sie hierzu folgendermaßen vor:  
  
    1.  Stellen Sie die generierte VHD bereit. In diesem Beispiel erfolgt die Bereitstellung unter „D:\\“.  
  
    2.  Führen Sie **bcdboot d:\windows** aus.  
  
    3.  Heben Sie die Bereitstellung der VHD auf.  
  
6.  Starten Sie den physischen Computer in der Nano Server-VHD.  
  
7.  Melden Sie sich bei der Wiederherstellungskonsole an (siehe Abschnitt „Nano Server-Wiederherstellungskonsole“ in diesem Leitfaden), indem Sie den Administrator und das Kennwort verwenden, die Sie während der Ausführung des Skripts in Schritt 3 bereitgestellt haben.
> [!NOTE]  
    > Die Wiederherstellungskonsole unterstützt nur grundlegende Tastaturfunktionen. Tastaturbeleuchtung, Nummernblöcke und Tastaturlayoutwechsel wie z.B. FESTSTELLTASTE und Num-Lock-Taste werden nicht unterstützt. 
  
8.  Fordern Sie die IP-Adresse des Nano Server-Computers an, und verwenden Sie Windows PowerShell-Remoting oder andere Remoteverwaltungstools, um eine Verbindung mit dem virtuellen Computer herzustellen und diesen remote zu verwalten.  
