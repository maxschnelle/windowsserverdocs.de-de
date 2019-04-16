---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: "Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5b5a8d198f93772903ea9b0a2b4b01075799bf0f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie beabsichtigen, eine Verbundserverfarm-Umgebung in Active Directory Federation Services \(AD FS\) konfigurieren, müssen Sie erstellen und konfigurieren ein dediziertes Dienstkonto in Active Directory Domain Services \(AD DS\), in denen die Farm befinden wird. Klicken Sie dann konfigurieren Sie jeden Verbundserver in der Farm für dieses Konto verwenden. Sie müssen die folgenden Aufgaben in Ihrer Organisation abschließen, wenn Sie Clients im Unternehmensnetzwerk einen Verbundserver in einer AD FS-Farm mithilfe der integrierten Windows-Authentifizierung authentifizieren Computer zulassen möchten.  
  
> [!NOTE]  
> Sie müssen die Aufgaben in dieser Vorgehensweise nur einmal für die gesamte Verbundserverfarm ausführen. Später, wenn Sie einen Verbundserver mithilfe von AD FS Federation Server-Konfigurations-Assistenten erstellen, geben Sie dieses Konto auf dem **Dienstkonto** Seite des Assistenten auf jedem Verbundserver in der Farm.  
  
#### <a name="create-a-dedicated-service-account"></a>Erstellen eines dedizierten Dienstkontos  
  
1.  Erstellen Sie ein dediziertes Konto für die durch den Benutzer bzw. eines Diensts in der Active Directory-Gesamtstruktur, die in der identitätsanbieterorganisation befindet. Dieses Konto ist erforderlich, damit die Kerberos-Authentifizierungsprotokoll in einem farmszenario funktionieren und die Pass\-through-Authentifizierung auf jedem Verbundserver ermöglicht. Verwenden Sie dieses Konto nur für die Zwecke der Verbundserverfarm.  
  
2.  Bearbeiten der Eigenschaften des Benutzerkontos, und wählen Sie die **Kennwort läuft nie ab** Kontrollkästchen. Dadurch wird sichergestellt, dass die Funktion des Dienstkontos nicht aufgrund von änderungsanforderungen für das Domänenkennwort unterbrochen wird.  
  
    > [!NOTE]  
    > Verwenden das Netzwerkdienstkonto für dieses dedizierte Konto führt zu zufällig generierten Fehlern beim Zugriff über die integrierte Windows-Authentifizierung, da Kerberos-Tickets nicht serverübergreifend zu einem anderen versucht wird.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>Festlegen des SPN des Dienstkontos  
  
1.  Da die Identität des Anwendungspools für die AD FS-AppPool als Domänenkonto durch den Benutzer-Dienst ausgeführt wird, müssen Sie die Dienstprinzipalnamen \(SPN\) für dieses Konto in der Domäne mit dem Befehlszeilentool Setspn.exe konfigurieren. Setspn.exe wird standardmäßig auf Computern unter Windows Server 2008 installiert. Führen Sie den folgenden Befehl auf einem Computer, der mit der gleichen Domäne angehört, in dem durch den Benutzer/Dienstkonto befindet:  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    Z. B. in einem Szenario, in dem alle Verbundserver Cluster unter dem Domain Name System \(DNS\) Host Name "FS.Fabrikam.com" und der Dienstkontonamen an, der die die AD FS-AppPool zugewiesen ist, heißt adfs2farm, geben Sie den Befehl wie folgt aus, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    Es ist erforderlich, um diese Aufgabe für dieses Konto nur einmal ausführen.  
  
2.  Nach der AD FS-AppPool-Identität in das Dienstkonto geändert wird, legen Sie die Access-Steuerelement Listen \(ACLs\) auf SQL Server-Datenbank Lesezugriff auf dieses neue Konto zulassen, damit die AD FS-AppPool die Richtliniendaten lesen kann.  
  

