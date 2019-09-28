---
title: Erforderliche Komponenten für die Bereitstellung von DirectAccess
description: Dieses Thema enthält die Voraussetzungen für die DirectAccess-Bereitstellung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6e04dbf1576277493ec849c8de82aeab51e97649
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388813"
---
# <a name="prerequisites-for-deploying-directaccess"></a>Erforderliche Komponenten für die Bereitstellung von DirectAccess

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In der folgenden Tabelle sind die Voraussetzungen für die Verwendung der Konfigurations-Assistenten für die Bereitstellung von DirectAccess aufgeführt.  
  
|||  
|-|-|  
|Szenario|Erforderliche Komponenten|  
|[Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-Die Windows-Firewall muss in allen Profilen aktiviert sein.<br /><br />: Wird nur für Clients unterstützt, auf denen Windows 10 @ no__t-0 ausgeführt wird. <br />              Windows @ no__t-0 8 und Windows @ no__t-1 8,1 Enterprise.<br /><br />-Eine Public Key-Infrastruktur ist nicht erforderlich.<br /><br />-Wird für die Bereitstellung der zweistufigen Authentifizierung nicht unterstützt. Für die Authentifizierung sind Domänenanmeldeinformationen erforderlich.<br /><br />-Stellt DirectAccess automatisch für alle mobilen Computer in der aktuellen Domäne bereit.<br /><br />-Der Datenverkehr an das Internet erfolgt nicht über DirectAccess. Die Konfiguration einer Tunnelerzwingung wird nicht unterstützt.<br /><br />-Der DirectAccess-Server ist der Netzwerkadressen Server.<br /><br />-Netzwerk Zugriffsschutz (Network Access Protection, NAP) wird nicht unterstützt.<br /><br />Das Ändern von Richtlinien mithilfe einer anderen Funktion als der DirectAccess-Verwaltungskonsole oder Windows PowerShell-Cmdlets wird nicht unterstützt.<br /><br />-Verwenden Sie für eine Konfiguration mit mehreren Standorten (jetzt oder in der Zukunft) zuerst die Anleitung unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).|  
|[Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-Eine Public Key-Infrastruktur muss bereitgestellt werden.<br />    Weitere Informationen finden Sie unter [test Lab Guide Mini-Module: Grundlegende PKI für Windows Server 2012 @ no__t-0.<br /><br />-Die Windows-Firewall muss in allen Profilen aktiviert sein.<br /><br />DirectAccess wird von den folgenden Server Betriebssystemen unterstützt.<br /><br />-Sie können alle Versionen von Windows Server 2016 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2012 R2 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2012 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2008 R2 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br /><br />DirectAccess wird von den folgenden Client Betriebssystemen unterstützt.<br /><br />-Windows 10 @ no__t-0 Enterprise<br />-Windows 10 @ no__t-0 Enterprise 2015 Long Term Servicing Branch (ltionb)<br />-Windows @ no__t-0 8 und 8,1 Enterprise<br />-Windows @ no__t-0 7 Ultimate<br />-Windows @ no__t-0 7 Enterprise<br /><br />-Tunnel Konfiguration erzwingen wird bei der kerbproxy-Authentifizierung nicht unterstützt.<br /><br />Das Ändern von Richtlinien mithilfe einer anderen Funktion als der DirectAccess-Verwaltungskonsole oder Windows PowerShell-Cmdlets wird nicht unterstützt.<br /><br />-Das Trennen von NAT64/DNS64-und IPHTTPS-Server Rollen auf einem anderen Server wird nicht unterstützt.|  
  


