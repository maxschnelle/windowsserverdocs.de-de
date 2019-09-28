---
title: Azure AD Domain Services und Remotedesktopdienste
description: Hier erfährst du, wie du Azure AD Domain Services in deine RDS-Bereitstellung integrierst.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/02/2017
ms.tgt_pltfrm: na
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: d3fe370f18df980acaeaa847bd96642b97613f80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387632"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>Integrieren von Azure AD Domain Services in deine RDS-Bereitstellung

[Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) kann in einer Remotedesktopdienste-Bereitstellung anstelle von Windows Server Active Directory verwendet werden. Mit Azure AD DS kannst du deine bereits vorhandenen Azure AD-Identitäten in klassischen Windows-Workloads verwenden.

Azure AD DS ermöglicht Folgendes: 
- Erstellen einer Azure-Umgebung mit einer lokalen Domäne für native Cloudorganisationen 
- Erstellen einer isolierten Azure-Umgebung mit den gleichen Identitäten, die auch für deine lokale und onlinebasierte Umgebung verwendet werden, ohne ein Site-to-Site-VPN oder eine ExpressRoute-Verbindung erstellen zu müssen 

Nach der Integration von Azure AD DS in deine Remotedesktopbereitstellung sieht deine Architektur in etwa wie folgt aus:

![Architekturdiagramm: RDS mit Azure AD DS](media/aadds-rds.png)

Unter [Architektur der Remotedesktopdienste](desktop-hosting-logical-architecture.md) wird diese Architektur mit anderen RDS-Bereitstellungsszenarien verglichen.

Ausführlichere Informationen zu Azure AD DS findest du unter [Azure Active Directory-Domänendienste (AD)](/azure/active-directory-domain-services/active-directory-ds-overview) sowie unter [So entscheiden Sie, ob die Azure AD Domain Services für Ihren Anwendungsfall geeignet sind](/azure/active-directory-domain-services/active-directory-ds-comparison).

Im Anschluss erfährst du, wie du Azure AD DS mit RDS bereitstellst.

## <a name="prerequisites"></a>Voraussetzungen

Um deine Identitäten aus Azure AD in einer RDS-Bereitstellung verwenden zu können, musst du zunächst [Azure AD zum Speichern der Kennworthashes für die Identitäten deiner Benutzer konfigurieren](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync). Bei nativen Cloudorganisationen sind dazu keine weiteren Änderungen am Verzeichnis erforderlich. Lokale Organisationen müssen dagegen die Synchronisierung und Speicherung von Kennworthashes in Azure AD zulassen, was in einigen Organisationen möglicherweise nicht zulässig ist. Nach dieser Konfigurationsänderung müssen die Benutzer ihre Kennwörter zurücksetzen.

## <a name="deploy-azure-ad-ds-and-rds"></a>Bereitstellen von Azure AD DS und RDS 
Führe die folgenden Schritte aus, um Azure AD DS und RDS bereitzustellen:

1. Aktiviere [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started). Der verlinkte Artikel enthält Folgendes:
   - Exemplarische Vorgehensweise zum Erstellen der entsprechenden Azure AD-Gruppen für die Domänenadministration
   - Deutliche Hinweise, wenn Benutzer ggf. ihr Kennwort ändern müssen, damit ihre Konten mit Azure AD DS verwendet werden können
   
2. Richte RDS ein. Du kannst entweder eine Azure-Vorlage verwenden oder RDS manuell bereitstellen.
   - Verwende die [vorhandene AD-Vorlage](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/). Passe Folgendes an:
   
     - **Einstellungen**
       - **Ressourcengruppe:** Verwende die Ressourcengruppe, in der du die RDS-Ressourcen erstellen möchtest.
         > [!NOTE] 
         > Aktuell muss es sich dabei um die gleiche Ressourcengruppe handeln, die auch das virtuelle Azure Resource Manager-Netzwerk enthält.

       - **Präfix für DNS-Bezeichnung:** Gib die URL ein, die Benutzer für den RD-Webzugriff verwenden sollen.
       - **AD-Domänenname:** Gib den vollständigen Namen deiner Azure AD-Instanz ein (beispielsweise „contoso.onmicrosoft.com“ oder „contoso.com“).
       - **AD-VNET-Name** und **AD-Subnetzname**: Gib die gleichen Werte ein, die du auch bei der Erstellung des virtuellen Azure Resource Manager-Netzwerks verwendet hast. Hierbei handelt es sich um das Subnetz, mit dem die RDS-Ressourcen eine Verbindung herstellen.
       - **Administratorbenutzername** und **Administratorkennwort**: Gib die Anmeldeinformationen für einen Administratorbenutzer ein, der der Gruppe **AAD DC-Administratoren** in Azure AD angehört.
   
     - **Vorlage**
        - Entferne alle Eigenschaften von **dnsServers**: Wähle dazu auf der Seite „Azure-Schnellstartvorlagen“ die Option **Vorlage bearbeiten** aus, suche nach „dnsServers“, und entferne die Eigenschaft. 

           Beispiel vor dem Entfernen der Eigenschaft **dnsServers**:
      
           ![Azure-Schnellstartvorlage mit Eigenschaft „dnsSettings“](media/rds-remove-dnssettings-before.png)

           Nach dem Entfernen der Eigenschaft sieht die Datei wie folgt aus:

           ![Azure-Schnellstartvorlage nach dem Entfernen der Eigenschaft „dnsSettings“](media/rds-remove-dnssettings-after.png)
   
   - [Stelle RDS manuell bereit.](rds-deploy-infrastructure.md) 

