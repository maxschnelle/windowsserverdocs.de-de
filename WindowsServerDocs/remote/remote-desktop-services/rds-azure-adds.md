---
title: Azure Active Directory-Domänendienste und Remotedesktopdienste
description: Erfahren Sie, wie Sie Azure AD Domain Services in Ihre RDS-Bereitstellung integrieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/02/2017
ms.tgt_pltfrm: na
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: 8b1baf642ffa3c8e8a0a2cfc70d2f49b58f208b3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446579"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>Integration von Azure Active Directory Domain Services mit der RDS-Bereitstellung

Sie können [Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) in der Remote Desktop Services-Bereitstellung anstelle der Windows Server Active Directory. Azure AD DS können Sie Ihre vorhandenen Azure AD-Identitäten, sich mit den klassischen Windows-Workloads zu verwenden.

Mit Azure AD DS können Sie folgende Aktionen ausführen: 
- Erstellen Sie eine Azure-Umgebung mit einer lokalen Domäne für das Ergebnis jahrelanger-in-the-Cloud-Organisationen. 
- Erstellen Sie eine isolierte Azure-Umgebung mit den gleichen Identitäten, die für Ihre lokalen und online-Umgebung verwendet werden, ohne eine Standort-zu-Standort-VPN oder ExpressRoute erstellen zu müssen. 

Wenn Sie die Integration von Azure AD DS in Ihrer remotedesktopbereitstellung fertig sind, wird Ihre Architektur wie folgt aussehen:

![Ein-Architekturdiagramm mit RDS mit Azure AD DS](media/aadds-rds.png)

Sehen Sie sich, um anzuzeigen, wie diese Architektur mit anderen RDS-Bereitstellungsszenarios vergleicht, [Remote Desktop Services Architekturen](desktop-hosting-logical-architecture.md).

Um ein besseres Verständnis von Azure AD DS zu erhalten, sehen Sie sich die [Übersicht über die Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-overview) und [Vorgehensweise entscheiden, ob es sich bei Azure AD DS für Ihren Anwendungsfall geeignet ist](/azure/active-directory-domain-services/active-directory-ds-comparison).

Verwenden Sie die folgende Informationen zum Bereitstellen von Azure AD DS mit RDS.

## <a name="prerequisites"></a>Vorraussetzungen

Bevor Sie Ihre Identitäten von Azure AD in einer RDS-Bereitstellung mit schalten können [Konfigurieren von Azure AD, um die verschlüsselte Kennwörter für die Identitäten Ihrer Benutzer speichern](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync). Das Ergebnis jahrelanger-in-the-Cloud-Organisationen müssen nicht in ihrem Verzeichnis keine weiteren Änderungen vornehmen. Allerdings müssen auf lokale Organisationen Kennworthashes synchronisiert und in Azure AD, die möglicherweise nicht zulässig, einige Organisationen gespeichert werden können. Benutzer haben ihre Kennwörter zurücksetzen, nach dem vornehmen dieser konfigurationsänderung.

## <a name="deploy-azure-ad-ds-and-rds"></a>Bereitstellen von Azure AD DS und RDS 
Verwenden Sie die folgenden Schritte zum Bereitstellen von Azure AD DS und RDS.

1. Aktivieren Sie [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started). Beachten Sie, dass es sich bei der verlinkten Artikel durch die folgende Funktion übernimmt:
   - Exemplarische Vorgehensweise zum Erstellen der entsprechenden Azure AD-Gruppen für die Verwaltung von Domänen.
   - Markieren Sie bei der Sie möglicherweise erzwingen, dass Benutzer ihr Kennwort zu ändern, sodass ihre Konten mit Azure AD DS arbeiten können.
   
2. Einrichten von RDS. Sie können eine Azure-Vorlage verwenden oder RDS manuell bereitstellen.
   - Verwenden der [vorhandene AD-Vorlage](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/). Stellen Sie sicher, dass Folgendes anpassen:
   
     - **Einstellungen**
       - **Ressourcengruppe**: Verwenden Sie die Ressourcengruppe, in dem Sie die RDS-Ressourcen erstellen möchten.
         > [!NOTE] 
         > Jetzt muss die gleiche Ressourcengruppe vorhanden ist, in dem die Azure Resource Manager-Netzwerk.

       - **Bezeichnung des DNS-Präfix**: Geben Sie die URL, die Benutzern auf RD-Web zugreifen sollen.
       - **AD-Domänenname**: Geben Sie den vollständigen Namen Ihrer Azure AD-Instanz, z. B. "contoso.onmicrosoft.com" oder "contoso.com".
       - **AD-Vnet-Name** und **Ad Subnetzname**: Geben Sie die gleichen Werte, die Sie verwendet werden, wenn Sie die Azure Resource Manager-Netzwerk erstellt haben. Dies ist das Subnetz, mit dem die RDS-Ressourcen verbunden werden.
       - **Benutzername des Administrators** und **Administratorkennwort**: Geben Sie die Anmeldeinformationen für einen Benutzer mit Administratorrechten, die ein Mitglied der **AAD DC Administrators** Gruppe in Azure AD.
   
     - **Vorlage**
        - Entfernen Sie alle Eigenschaften des **DnsServers**: nach der Auswahl **Bearbeitungsvorlage** klicken Sie auf der Azure-Schnellstart-Vorlage, suchen Sie nach "DnsServers", und entfernen Sie die Eigenschaft. 

           Angenommen, vor dem Entfernen der **DnsServers** Eigenschaft:
      
           ![Azure-schnellstartvorlage mit DnsSettings-Eigenschaft](media/rds-remove-dnssettings-before.png)

           Und hier ist die gleiche Datei nach dem Entfernen der Eigenschaft:

           ![Azure-schnellstartvorlage mit entfernten DnsSettings-Eigenschaft](media/rds-remove-dnssettings-after.png)
   
   - [Manuelles Bereitstellen von RDS](rds-deploy-infrastructure.md). 

