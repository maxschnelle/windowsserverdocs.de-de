---
title: Verwalten von Ressourcen in mehreren ActiveDirectory-Gesamtstrukturen
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2bbd303df635af314cee2126a75f0569ede2f5de
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282186"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>Verwalten von Ressourcen in mehreren ActiveDirectory-Gesamtstrukturen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erfahren, wie Sie IPAM zum Verwalten von Domänencontroller, DHCP-Server und DNS-Servern in mehreren Active Directory-Gesamtstrukturen zu verwenden.  
  
Verwendung von IPAM zum Verwalten von Ressourcen in Active Directory-Remotegesamtstrukturen müssen jede Gesamtstruktur, die Sie verwalten möchten zwei Weise mit der Gesamtstruktur vertrauen, auf dem IPAM installiert ist.  
  
Um den Ermittlungsprozess für die verschiedenen Active Directory-Gesamtstrukturen zu starten, öffnen Sie Server-Manager, und klicken Sie auf IPAM. Klicken Sie in der IPAM-Clientkonsole auf **Serverermittlung konfigurieren**, und klicken Sie dann auf **erhalten Gesamtstrukturen**. Hierdurch wird ein Hintergrundtask, mit dem vertrauenswürdigen Gesamtstrukturen und deren Domänen ermittelt initiiert. Nachdem der Ermittlungsvorgang abgeschlossen ist, klicken Sie auf **Serverermittlung konfigurieren**, dadurch wird das folgende Dialogfeld geöffnet.  
  
![Konfigurieren der Serverermittlung](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>Für die Gruppenrichtlinie\-für ein Szenario für die gesamtstrukturübergreifende Active Directory-Bereitstellung basiert, stellen Sie sicher, dass Sie das folgende Windows PowerShell-Cmdlet auf dem IPAM-Server und nicht auf die vertrauende Domäne Domänencontroller ausführen. Als Beispiel, wenn der IPAM-Server Mitglied der Gesamtstruktur %% amp;quot;corp.contoso.com%%amp;quot; und die vertrauende Gesamtstruktur ist "Fabrikam.com", können Sie Ausführen der folgende Windows PowerShell-Cmdlet auf dem IPAM-Server in "corp.contoso.com" für die Gruppenrichtlinie\-basierte Bereitstellung auf der Gesamtstruktur für "Fabrikam.com". Um dieses Cmdlet ausführen zu können, müssen Sie Mitglied der Gruppe "Domänen-Admins" in der Gesamtstruktur "Fabrikam.com" sein.

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

In der **Serverermittlung konfigurieren** Dialogfeld klicken Sie auf **wählen Sie die Gesamtstruktur**, und wählen Sie dann auf die Gesamtstruktur, die Sie mit IPAM verwalten möchten. Wählen Sie auch die Domänen, die Sie verwalten möchten, und klicken Sie dann auf **hinzufügen**.

In **wählen Sie die Serverrollen zur Ermittlung**, für jede Domäne, die Sie verwalten möchten, geben Sie den Server, um zu ermitteln. Die Optionen sind **Domänencontroller**, **DHCP-Server**, und **DNS-Server**.

Domänencontroller, DHCP-Server und DNS-Servern ermittelt werden – also wenn Sie nicht, um einen dieser Typen von Servern zu ermitteln möchten, stellen Sie sicher, dass Sie das Kontrollkästchen für diese Option deaktivieren, in der Standardeinstellung.

Klicken Sie in der oben genannten Beispiel Abbildung der IPAM-Server in der Gesamtstruktur "contoso.com" installiert ist, und die Stammdomäne der Gesamtstruktur "Fabrikam.com" ist für die IPAM-Verwaltung hinzugefügt. Die ausgewählten Serverrollen ermöglichen IPAM, zu ermitteln und Verwalten von Domänencontroller, DHCP-Server und DNS-Server in der Root-Domäne "Fabrikam.com" und der Root-Domäne "contoso.com".

Wenn Sie Gesamtstrukturen, Domänen und Serverrollen angegeben haben, klicken Sie auf **OK**. IPAM führt die Ermittlung, und nach Abschluss der Ermittlung können Sie Ressourcen in der lokalen und Remotecomputern Gesamtstruktur verwalten.
