---
title: Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b01680d4b35461ff85965781ebc60e7a613d1cb8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, erfahren Sie, wie Sie IPAM verwenden, um Domänencontroller, DHCP-Server und DNS-Server in mehreren Active Directory-Gesamtstrukturen zu verwalten.  
  
Um IPAM Ressourcen in Active Directory-Gesamtstrukturen remote verwalten, muss jede Gesamtstruktur, die Sie verwalten möchten haben zwei Weise mit der Gesamtstruktur vertrauen, auf dem IPAM installiert ist.  
  
Um den Ermittlungsprozess für andere Active Directory-Gesamtstrukturen zu starten, öffnen Sie Server-Manager, und klicken Sie auf IPAM. Klicken Sie in der IPAM-Clientkonsole auf **Serverermittlung konfigurieren**, und klicken Sie dann auf **erhalten Gesamtstrukturen**. Initiiert eine Hintergrundaufgabe, die vertrauenswürdigen Gesamtstrukturen und ihre Domänen ermittelt. Klicken Sie nach Abschluss der Ermittlung **Serverermittlung konfigurieren**, die das folgende Dialogfeld geöffnet.  
  
![Konfigurieren der Serverermittlung](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>Stellen Sie sicher, dass Sie das folgende Windows PowerShell-Cmdlet auf dem IPAM-Server und nicht auf die vertrauende Domäne Domänencontroller ausführen, für die Gruppe wird-basierte Bereitstellung für ein Szenario gesamtstrukturübergreifende Active Directory. Beispielsweise können der IPAM-Server mit der Gesamtstruktur corp.contoso.com verbunden ist und die vertrauende Gesamtstruktur ist fabrikam.com, Sie das folgende Windows PowerShell-Cmdlet auf dem IPAM-Server im corp.contoso.com für die Gruppe wird basierend auf der Gesamtstruktur fabrikam.com Bereitstellung ausführen. Um dieses Cmdlet ausführen zu können, müssen Sie Mitglied der Gruppe "Domänen-Admins" in der Gesamtstruktur fabrikam.com sein.

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

In der **Serverermittlung konfigurieren** Dialogfeld, klicken Sie auf **wählen Sie die Gesamtstruktur**, und wählen Sie dann die Gesamtstruktur, die Sie mit IPAM verwalten möchten. Wählen Sie auch die Domänen, die Sie verwalten möchten, und klicken Sie dann auf **hinzufügen**.

In **Auswählen der Serverrollen zur Ermittlung**, für jede Domäne, die Sie verwalten möchten, geben Sie den Typ der zu ermitteln. Die Optionen sind **Domänencontroller**, **DHCP-Server**, und **DNS-Server**.

Standardmäßig werden Domänencontroller, DHCP-Server und DNS-Server ermittelt. – also wenn Sie nicht eine der folgenden Arten von Servern ermitteln möchten, stellen Sie sicher, dass Sie das Kontrollkästchen für diese Option deaktivieren.

Klicken Sie in der obigen Beispiel Abbildungder IPAM-Server in der Gesamtstruktur contoso.com installiert ist, und die Stammdomäne der Gesamtstruktur fabrikam.com ist für die IPAM-Verwaltung hinzugefügt. Die ausgewählten Serverrollen ermöglichen IPAM, zu ermitteln und zu verwalten, Domänencontroller, DHCP-Server und DNS-Server in der Stammdomäne fabrikam.com und der Stammdomäne contoso.com.

Nachdem Sie Gesamtstrukturen, Domänen und Serverrollen angegeben haben, klicken Sie auf **OK**. IPAM wird gesucht, und nach Abschluss der Ermittlung können Sie Ressourcen in der Gesamtstruktur lokal und remote verwalten.
