---
title: Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 39d519f0d588a7c2ba6a671eeace14cfe788f6b0
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517915"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie mit IPAM Domänen Controller, DHCP-Server und DNS-Server in mehreren Active Directory Gesamtstrukturen verwalten.

Wenn Sie IPAM zur Verwaltung von Ressourcen in Remote Active Directory-Gesamtstrukturen verwenden möchten, muss jede zu verwaltende Gesamtstruktur eine bidirektionale Vertrauensstellung mit der Gesamtstruktur aufweisen, in der IPAM installiert ist.

Öffnen Sie Server-Manager, und klicken Sie auf IPAM, um den Ermittlungsprozess für verschiedene Active Directory Gesamtstrukturen zu starten. Klicken Sie in der IPAM-Client Konsole auf **Server Ermittlung konfigurieren**, und klicken Sie dann auf Gesamtstruktur **erhalten**. Dadurch wird eine Hintergrundaufgabe initiiert, die vertrauenswürdige Gesamtstrukturen und deren Domänen ermittelt. Nachdem der Ermittlungs Vorgang abgeschlossen ist, klicken Sie auf **Server Ermittlung konfigurieren**, um das folgende Dialogfeld zu öffnen.

![Konfigurieren der Serverermittlung](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)

>[!NOTE]
>Stellen Sie für die Gruppenrichtlinie \- basierte Bereitstellung eines Active Directory Gesamtstruktur übergreifenden Szenarios sicher, dass Sie das folgende Windows PowerShell-Cmdlet auf dem IPAM-Server und nicht auf den vertrauenden Domänen Controllern ausführen. Wenn der IPAM-Server z. b. mit der Gesamtstruktur verbunden ist Corp.contoso.com und die vertrauende Gesamtstruktur Fabrikam.com ist, können Sie das folgende Windows PowerShell-Cmdlet auf dem IPAM-Server in Corp.contoso.com für die Gruppenrichtlinie basierte Bereitstellung in der Fabrikam.com-Gesamtstruktur ausführen \- . Zum Ausführen dieses Cmdlets müssen Sie Mitglied der Gruppe "Domänen-Admins" in der Fabrikam.com-Gesamtstruktur sein.

```powershell
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
```

Klicken Sie im Dialogfeld **Server Ermittlung konfigurieren** auf Gesamtstruktur **auswählen**, und wählen Sie dann die Gesamtstruktur aus, die Sie mit IPAM verwalten möchten. Wählen Sie außerdem die Domänen aus, die Sie verwalten möchten, und klicken Sie dann auf **Hinzufügen**.

Geben Sie unter **Wählen Sie die zu**ermittelnden Server Rollen aus für jede Domäne, die Sie verwalten möchten, den zu ermittelnden Servertyp an. Bei den Optionen handelt es sich um **Domänen Controller**, **DHCP-Server**und **DNS-Server**.

Standardmäßig werden Domänen Controller, DHCP-Server und DNS-Server ermittelt. Wenn Sie eine dieser Server Typen nicht ermitteln möchten, müssen Sie das Kontrollkästchen für diese Option deaktivieren.

In der obigen Beispiel Abbildung wird der IPAM-Server in der contoso.com-Gesamtstruktur installiert, und die Stamm Domäne der Fabrikam.com-Gesamtstruktur wird für die IPAM-Verwaltung hinzugefügt. Mit den ausgewählten Server Rollen können IPAM Domänen Controller, DHCP-Server und DNS-Server in der Stamm Domäne fabrikam.com und in der Stamm Domäne contoso.com ermitteln und verwalten.

Nachdem Sie die Gesamtstrukturen, Domänen und Server Rollen festgelegt haben, klicken Sie auf **OK**. Die Ermittlung wird von IPAM ausgeführt. wenn die Ermittlung abgeschlossen ist, können Sie Ressourcen sowohl in der lokalen als auch in der Remote Gesamtstruktur verwalten.
