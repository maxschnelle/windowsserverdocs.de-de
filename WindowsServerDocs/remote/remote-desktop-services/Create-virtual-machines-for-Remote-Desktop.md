---
title: Erstellen virtueller Computer für Remotedesktop
description: Erstellen Sie virtuelle Computer, auf dem Host Remote Desktop-Komponenten in der Cloud.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0f62d6f-0915-44ca-afef-be44a922e20e
author: lizap
manager: dongill
ms.openlocfilehash: 5c61d9f08cb799d6a63a004bedab924a6ba37fdc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446728"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>Erstellen virtueller Computer für Remotedesktop

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um die virtuellen Computer in der Mandanten-Umgebung zu erstellen, die zum Ausführen von Windows Server 2016-Rollen, Dienste und Funktionen für eine desktophostingbereitstellung verwendet werden.   
  
Dieses Beispiel, für eine einfache Bereitstellung wird das Minimum von 3 VMs erstellt werden. Ein virtueller Computer hostet die Rollendienste Remote Desktop (RD)-Verbindungsbroker und License Server und einer Dateifreigabe für die Bereitstellung. Ein zweiter virtueller Computer hostet der Rollendienste RD-Gateway und Web Access.  Ein dritter virtuellen Computer hosten, den RD-Sitzungshost-Rollendienst. Für sehr kleine Bereitstellungen können Sie VM-Kosten reduzieren, indem Sie AAD App Proxy verwenden, um alle öffentlichen Endpunkten aus der Bereitstellung zu vermeiden, und kombinieren alle Rollendienste auf einem einzelnen virtuellen Computer. Für größere Bereitstellungen können Sie die verschiedenen Rollendienste auf einzelnen virtuellen Computern, um eine bessere Skalierung ermöglichen installieren.  
  
In diesem Abschnitt wird beschrieben, die erforderlichen Schritte zum Bereitstellen von virtuellen Computern für jede Rolle basierend auf Windows Server-Images in die [Microsoft Azure Marketplace](https://azure.microsoft.com/marketplace/). Wenn Sie zum Erstellen virtueller Maschinen aus einem benutzerdefinierten Image, das PowerShell erforderlich ist benötigen, lesen Sie [Erstellen einer Windows-VM mit Resource Manager und PowerShell](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-ps-create/). Klicken Sie dann hier zum Anfügen von Azure-Datenträgern für die Dateifreigabe, und geben eine externe URL für Ihre Bereitstellung zurück.  
  
1. [Erstellen von Windows-VMs](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/) auf dem RD Connection Broker, Remotedesktop-Lizenzserver und Datei-Server gehostet.  
  
   Für unsere Zwecke verwendet haben wir die folgenden Benennungskonventionen:  
   - Remotedesktop-Lizenzserver und Dateiserver:   
       - VM: Contoso-Cb1  
       - Verfügbarkeitsgruppe: CbAvSet    
   - Web Access für Remotedesktop und RD-Gateway-Server:   
       - VM: Contoso-WebGw1  
       - Verfügbarkeitsgruppe: WebGwAvSet  
          
   - Remotedesktop-Sitzungshosts:   
       - VM: Contoso-Sh1  
       - Verfügbarkeitsgruppe: ShAvSet  
          
   Jeder virtuelle Computer wird die gleiche Ressourcengruppe verwendet.  
2. Erstellen Sie ein, und fügen Sie einen Azure-Datenträger für die Benutzer-Profil-Datenträgern (UPD)-Freigabe:  
   1.  Im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung aus, und klicken Sie dann auf den virtuellen Computer für den Remotedesktop-Verbindungsbroker (z. B. Contoso-Cb1) erstellt.  
   2.  Klicken Sie auf **Einstellungen > Datenträger > neuen Anfügen**.  
   3.  Akzeptieren Sie die Standardwerte für Name und Typ.  
   4.  Geben Sie eine Größe (in GB), die zum Speichern von Netzwerkfreigaben für die Mandanten-Umgebung, einschließlich Benutzerprofil-Datenträger und Zertifikate groß genug ist. Sie können 5 GB pro Benutzer annäherungsweise implementieren, die Sie verwenden möchten  
   5.  Akzeptieren Sie die Standardwerte für den Speicherort und Host-caching, und klicken Sie dann auf **OK**.  
3. Erstellen Sie einen Load Balancer für den Zugriff auf die extern-Bereitstellung:
   1. Im Azure-Portal auf **Durchsuchen > Load Balancer**, und klicken Sie dann auf **hinzufügen**.
   2. Geben Sie eine **Namen**Option **öffentliche** als die **Typ** der Load Balancer, und wählen Sie das entsprechende **Abonnement**,  **Ressourcengruppe**, und **Speicherort**.
   3. Wählen Sie **eine öffentliche IP-Adresse**, **neu erstellen**, geben Sie einen Namen ein, und wählen **Ok**.
   4. Wählen Sie **erstellen** den Load Balancer zu erstellen.
4. Konfigurieren Sie den externen Lastenausgleich für die Bereitstellung
   1. Im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung aus, und klicken Sie dann auf den Load Balancer, die Sie für die Bereitstellung erstellt haben.
   2. Fügen Sie einen Back-End-Adresspool für den Load Balancer den Datenverkehr zu senden:
       1. Wählen Sie **Back-End-Pool** und **hinzufügen**.
       2. Geben Sie einen **Namen** , und wählen Sie  **\+ Hinzufügen eines virtuellen Computers**.
       3. Wählen Sie **verfügbarkeitsgruppe** und **WebGwAvSet**.
       4. Wählen Sie **VMs**, **Contoso-WebGw1**, **wählen**, **OK**, und **OK**.
   3. Fügen Sie einen Test hinzu, damit der Load Balancer weiß, welche Computer aktiv sind:
       1. Wählen Sie **Tests** und **hinzufügen**.
       2. Geben Sie einen **Namen** (z. B. HTTPS), wählen Sie **TCP**, geben Sie **Port** 443, und wählen **OK**.
   4. Geben Sie lastenausgleichsregeln, um den eingehenden Datenverkehr zu verteilen:
      1. Wählen Sie **Lastenausgleichsregeln** und **hinzufügen**
      2. Geben Sie einen **Namen** (z. B. HTTPS), wählen Sie **TCP**, und 443 für beide die **Port** und **Back-End-Port**.
          - Lassen Sie für eine Windows 10 und Windows Server 2016-Bereitstellung, **Sitzungspersistenz** als **keine**wählen Sie andernfalls **Client-IP-** .
      3. Wählen Sie **OK** , die HTTPS-Regel zu akzeptieren.
      4. Erstellen einer neuen Regel dazu **hinzufügen**.
      5. Geben Sie einen **Namen** (z. B. UDP), wählen Sie **UDP**, und 3391 für beide die <strong>Port und die ** Back-End-Port</strong>.
          - Lassen Sie bei einer Bereitstellung von Windows 10 und Windows Server 2016 **Sitzungspersistenz** als **keine**wählen Sie andernfalls **Client-IP-** .
      6. Wählen Sie **OK** , die UDP-Regel zu akzeptieren.
   5. Geben Sie eine eingehende NAT-Regel eine direkte Verbindung zum Contoso-WebGw1 herstellen
       1. Wählen Sie **NAT-Eingangsregeln** und **hinzufügen**.
       2. Geben Sie einen **Namen** (z. B. RDP-Contoso-WebGw1), wählen Sie **Customm** für den Dienst **TCP** für das Protokoll, und geben Sie 14000 für die **Port**.
       3. Wählen Sie **wählen Sie einen virtuellen Computer** und Contoso-WebGw1.
       4. Wählen Sie **benutzerdefinierte** Geben Sie für die portzuordnung 3389 für die **Target Port**, und wählen Sie **OK**.
5. Geben Sie einen externe URL/DNS-Namen für Ihre Bereitstellung für den externen Zugriff:  
   1.  Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung aus, und klicken Sie dann auf die öffentliche IP-Adresse, die Sie für Web Access für Remotedesktop und RD-Gateway erstellt haben.  
   2.  Klicken Sie auf **Konfiguration**, geben Sie einen DNS-Namen (z. B. an Contoso), und klicken Sie dann auf **speichern**. Diese DNS-namensbezeichnung (contoso.westus.cloudapp.azure.com) ist der DNS-Name, die Sie für die Verbindung mit Ihrem Server Web Access für Remotedesktop und RD-Gateway verwenden.  

