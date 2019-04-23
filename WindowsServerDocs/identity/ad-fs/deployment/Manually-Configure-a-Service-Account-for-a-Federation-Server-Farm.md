---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7d215c80c03236df9479aff8046981741dfc83e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838151"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie beabsichtigen, eine Verbundserverfarm-Umgebung in Active Directory Federation Services konfigurieren \(AD FS\), müssen Sie erstellen und konfigurieren Sie ein dediziertes Dienstkonto in Active Directory Domain Services \(AD DS\) , in dem die Farm befinden. Dann legen Sie in der Konfiguration jedes Verbundservers in der Farm fest, dass dieses Konto verwendet wird. Wenn Sie Clients im Unternehmensnetzwerk einen Verbundserver in einer AD FS-Farm mithilfe der integrierten Windows-Authentifizierung authentifizieren zulassen möchten, müssen Sie die folgenden Aufgaben in Ihrer Organisation ausführen.  

> [!IMPORTANT]
> Zum Zeitpunkt der AD FS 3.0 (Windows Server 2012 R2) unterstützt AD FS die Verwendung von einem [Gruppenverwalteten Dienstkontos](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) \(gMSA\) als Dienstkonto.  Dies ist die empfohlene Option, da die Notwendigkeit entfällt für die Verwaltung des Kennworts für das im Laufe der Zeit.  Dieses Dokument beschreibt die alternative Groß-/Kleinschreibung mit einem herkömmlichen Dienst-Konto, z. B. in Domänen, die noch ausgeführt wird, ein Windows Server 2008 R2 oder früheren Domänenfunktionsebene \(Domänenfunktionsebene\).

> [!NOTE]  
> Die Aufgaben in dieser Prozedur müssen Sie nur einmal für die gesamte Verbundserverfarm ausführen. Später, wenn Sie einen Verbundserver mithilfe der AD FS Konfigurations-Assistenten erstellen, geben Sie dieses Konto auf dem **Dienstkonto** Seite des Assistenten auf jedem Verbundserver in der Farm.  
  
#### <a name="create-a-dedicated-service-account"></a>Erstellen eines dedizierten Dienstkontos  
  
1.  Erstellen Sie einen dedizierten Benutzer\/-Dienstkonto in Active Directory-Gesamtstruktur, die in der identitätsanbieterorganisation befindet. Dieses Konto ist erforderlich, damit die Kerberos-Authentifizierungsprotokoll in einem farmszenario funktionieren und Pass zu\-über die Authentifizierung auf jedem Verbundserver. Verwenden Sie dieses Konto nur für die Zwecke der die Verbundserverfarm gerichtet werden.  
  
2.  Bearbeiten Sie die Benutzerkonteneigenschaften, und aktivieren Sie das Kontrollkästchen **Kennwort läuft nie ab** . Mit dieser Aktion stellen Sie sicher, dass die Funktion dieses Dienstkontos nicht aufgrund von Änderungsanforderungen für das Domänenkennwort unterbrochen wird.  
  
    > [!NOTE]  
    > Die Verwendung des Netzwerkdienstkontos für dieses dedizierte Konto führt zu beliebigen Fehlern, wenn ein Zugriff über die integrierte Windows-Authentifizierung versucht wird, da Kerberos-Tickets nicht von einem Server zu einem anderen validiert werden.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>Sie richten Sie den SPN des Dienstkontos ein  
  
1.  Da die Identität des Anwendungspools für die AD FS-AppPool als Domänenbenutzer ausgeführt wird\/-Dienstkontos verwenden, müssen Sie den Dienstprinzipalnamen konfigurieren \(SPN\) für dieses Konto in der Domäne mit dem Befehl "Setspn.exe"\-Tools "Linie". Setspn.exe wird standardmäßig auf Computern unter Windows Server 2008 installiert. Führen den folgenden Befehl auf einem Computer, der mit der gleichen Domäne angehört, in denen der Benutzer\/Dienstkonto befindet:  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    Z. B. in einem Szenario, in der sich alle verbundnachrichtenklassen Server unter dem Domain Name System Cluster \(DNS\) Host Name "FS.Fabrikam.com" und den Namen des Dienstkontos aus, die die AD FS-AppPool zugeordnet ist, adfs2farm lautet, geben Sie den Befehl wie folgt, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    Sie müssen diese Aufgabe für dieses Konto nur einmal durchführen.  
  
2.  Nachdem die AD FS-AppPool-Identität für das Dienstkonto geändert wurde, legen Sie die Access Control Lists \(ACLs\) in der SQL Server-Datenbank, um Lesezugriff auf dieses neue Konto zulassen, damit der AD FS-AppPool die Richtliniendaten lesen kann.  
  

