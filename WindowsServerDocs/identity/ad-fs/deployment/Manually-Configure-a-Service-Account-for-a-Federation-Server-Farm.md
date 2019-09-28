---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8240903b3c446d4f02ca93dc053e520480f5e8ca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359489"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>Manuelles Konfigurieren eines Dienstkontos für eine Verbundserverfarm

Wenn Sie beabsichtigen, eine Verbund Serverfarm-Umgebung in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 zu konfigurieren, müssen Sie ein dediziertes Dienst Konto in Active Directory Domain Services \(AD DS @ no__t-3 erstellen und konfigurieren, in dem die Farm wird gespeichert. Dann legen Sie in der Konfiguration jedes Verbundservers in der Farm fest, dass dieses Konto verwendet wird. Sie müssen die folgenden Aufgaben in Ihrer Organisation durchführen, wenn Sie zulassen möchten, dass sich Client Computer im Unternehmensnetzwerk mithilfe der integrierten Windows-Authentifizierung bei einem der Verbund Server in einer AD FS-Farm authentifizieren können.  

> [!IMPORTANT]
> Ab AD FS 3,0 (Windows Server 2012 R2) unterstützt AD FS die Verwendung eines [Gruppen verwalteten Dienst Kontos](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) \(gmsa @ no__t-2 als Dienst Konto.  Dies ist die empfohlene Option, da es nicht mehr erforderlich ist, das Dienst Konto Kennwort über einen Zeitraum zu verwalten.  In diesem Dokument werden die alternativen Fälle bei der Verwendung eines herkömmlichen Dienst Kontos behandelt, z. b. in Domänen, die noch eine Windows Server 2008 R2-oder frühere Domänen Funktionsebene \(dfl @ no__t-1 ausführen.

> [!NOTE]  
> Die Aufgaben in dieser Prozedur müssen Sie nur einmal für die gesamte Verbundserverfarm ausführen. Wenn Sie später einen Verbund Server mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server erstellen, müssen Sie dieses Konto auf der Assistenten Seite **Dienst Konto** auf jedem Verbund Server in der Farm angeben.  
  
#### <a name="create-a-dedicated-service-account"></a>Erstellen eines dedizierten Dienstkontos  
  
1.  Erstellen Sie ein dediziertes Benutzerkonto "@ no__t-0service" in der Active Directory-Gesamtstruktur, die sich in der Identitäts Anbieter Organisation befindet. Dieses Konto ist erforderlich, damit das Kerberos-Authentifizierungsprotokoll in einem Farm Szenario funktioniert und Pass @ no__t-0through-Authentifizierung auf jedem der Verbund Server zulässt. Verwenden Sie dieses Konto nur für die Verbund Serverfarm.  
  
2.  Bearbeiten Sie die Benutzerkonteneigenschaften, und aktivieren Sie das Kontrollkästchen **Kennwort läuft nie ab** . Mit dieser Aktion stellen Sie sicher, dass die Funktion dieses Dienstkontos nicht aufgrund von Änderungsanforderungen für das Domänenkennwort unterbrochen wird.  
  
    > [!NOTE]  
    > Die Verwendung des Netzwerkdienstkontos für dieses dedizierte Konto führt zu beliebigen Fehlern, wenn ein Zugriff über die integrierte Windows-Authentifizierung versucht wird, da Kerberos-Tickets nicht von einem Server zu einem anderen validiert werden.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>Sie richten Sie den SPN des Dienstkontos ein  
  
1.  Da die Anwendungs Pool Identität für den AD FS AppPool als Domänen Benutzer @ no__t-0service-Konto ausgeführt wird, müssen Sie den Dienst Prinzipal Namen \(spn @ no__t-2 für dieses Konto in der Domäne mit dem Befehl "Setspn. exe" @ no__t-3LINE konfigurieren. Setspn. exe wird standardmäßig auf Computern installiert, auf denen Windows Server 2008 ausgeführt wird. Führen Sie den folgenden Befehl auf einem Computer aus, der mit derselben Domäne verknüpft ist, in der sich das Benutzerkonto "@ no__t-0service" befindet:  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    Beispiel: in einem Szenario, in dem alle Verbund Server unter dem Domain Name System \(dns @ no__t-1-Hostname) gruppiert sind und der Dienst Konto Name, der dem AD FS AppPool zugewiesen ist, den Namen adfs2farm hat, geben Sie den Befehl wie folgt ein, und Drücken Sie dann die EINGABETASTE:  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    Sie müssen diese Aufgabe für dieses Konto nur einmal durchführen.  
  
2.  Nachdem die AD FS AppPool-Identität in das Dienst Konto geändert wurde, legen Sie die Zugriffs Steuerungs Listen \(acls @ no__t-1 für die SQL Server-Datenbank fest, um Lesezugriff auf dieses neue Konto zuzulassen, damit der AD FS AppPool die Richtlinien Daten lesen kann.  
  

