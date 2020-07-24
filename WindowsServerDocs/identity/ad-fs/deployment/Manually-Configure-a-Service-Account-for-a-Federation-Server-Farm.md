---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: Manuelle Konfiguration eines Dienstkontos für eine Verbundserverfarm
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5d0495d43eecd2508a6535411ef4e226db0ebacf
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964792"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>Manuelle Konfiguration eines Dienstkontos für eine Verbundserverfarm

Wenn Sie beabsichtigen, eine Verbund Serverfarm-Umgebung in Active Directory-Verbunddienste (AD FS) \( AD FS zu konfigurieren \) , müssen Sie ein dediziertes Dienst Konto in Active Directory Domain Services AD DS erstellen und konfigurieren, in dem sich \( \) die Farm befinden wird. Dann legen Sie in der Konfiguration jedes Verbundservers in der Farm fest, dass dieses Konto verwendet wird. Sie müssen die folgenden Aufgaben in Ihrer Organisation durchführen, wenn Sie zulassen möchten, dass sich Client Computer im Unternehmensnetzwerk mithilfe der integrierten Windows-Authentifizierung bei einem der Verbund Server in einer AD FS-Farm authentifizieren können.  

> [!IMPORTANT]
> Ab AD FS 3,0 (Windows Server 2012 R2) unterstützt AD FS die Verwendung eines [Gruppen verwalteten Dienst Kontos](../../../security/group-managed-service-accounts/group-managed-service-accounts-overview.md) ( \( GMSA) \) als Dienst Konto.  Dies ist die empfohlene Option, da es nicht mehr erforderlich ist, das Dienst Konto Kennwort über einen Zeitraum zu verwalten.  In diesem Dokument werden die alternativen Fälle bei der Verwendung eines herkömmlichen Dienst Kontos behandelt, z. b. in Domänen, die weiterhin eine Microsoft Windows Server 2008 R2-oder frühere Domänen Funktionsebene verwenden \( \) .

> [!NOTE]  
> Die Aufgaben in dieser Prozedur müssen Sie nur einmal für die gesamte Verbundserverfarm ausführen. Wenn Sie später einen Verbundserver mithilfe des Assistenten für die Konfiguration des AD FS-Verbundservers erstellen, müssen Sie dieses Konto auf der Assistentenseite **Dienstkonto** für jeden Verbundserver in der Farm angeben.  
  
#### <a name="create-a-dedicated-service-account"></a>Erstellen eines dedizierten Dienstkontos  
  
1.  Erstellen Sie ein dediziertes Benutzer \/ Dienst Konto in der Active Directory-Gesamtstruktur, die sich in der Identitäts Anbieter Organisation befindet. Dieses Konto ist erforderlich, damit das Kerberos-Authentifizierungsprotokoll in einem Farm Szenario funktioniert und die \- Passthrough-Authentifizierung auf jedem der Verbund Server zulässt. Verwenden Sie dieses Konto nur für die Verbund Serverfarm.  
  
2.  Bearbeiten Sie die Benutzerkonteneigenschaften, und aktivieren Sie das Kontrollkästchen **Kennwort läuft nie ab**. Mit dieser Aktion stellen Sie sicher, dass die Funktion dieses Dienstkontos nicht aufgrund von Änderungsanforderungen für das Domänenkennwort unterbrochen wird.  
  
    > [!NOTE]  
    > Die Verwendung des Netzwerkdienstkontos für dieses dedizierte Konto führt zu beliebigen Fehlern, wenn ein Zugriff über die integrierte Windows-Authentifizierung versucht wird, da Kerberos-Tickets nicht von einem Server zu einem anderen validiert werden.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>Sie richten Sie den SPN des Dienstkontos ein  
  
1.  Da die Anwendungs Pool Identität für den AD FS AppPool als Domänen Benutzer- \/ Dienst Konto ausgeführt wird, müssen Sie den Dienst Prinzipal Namen- \( SPN \) für dieses Konto in der Domäne mit dem Befehls \- Zeilen Tool Setspn.exe konfigurieren. Setspn.exe wird standardmäßig auf Computern installiert, auf denen Windows Server 2008 ausgeführt wird. Führen Sie den folgenden Befehl auf einem Computer aus, der mit derselben Domäne verknüpft ist, in der sich das Benutzer \/ Dienst Konto befindet:  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    Beispiel: in einem Szenario, in dem alle Verbund Server unter dem Domain Name System \( DNS \) -Hostname FS.fabrikam.com und der Dienst Konto Name, der dem AD FS AppPool zugewiesen ist, den Namen adfs2farm hat, geben Sie den Befehl wie folgt ein, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    Sie müssen diese Aufgabe für dieses Konto nur einmal durchführen.  
  
2.  Nachdem die AD FS AppPool-Identität in das Dienst Konto geändert wurde, legen Sie die Zugriffs Steuerungs Listen- \( ACLs \) für die SQL Server-Datenbank so fest, dass Sie Lesezugriff auf dieses neue Konto haben, damit der AD FS AppPool die Richtlinien Daten lesen kann.  
  
