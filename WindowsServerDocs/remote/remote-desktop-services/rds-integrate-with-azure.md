---
title: 'RDS: Integration mit Azure-Diensten'
description: Erfahren Sie, wie Sie RDS in Ihre Azure-Bereitstellung und Azure in Ihre RDS-Bereitstellung integrieren.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.topic: article
author: lizap
ms.openlocfilehash: 2c792a22608fe0e7ae826b27d6917202037559e4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80855073"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>Remotedesktopdienste: Integration mit Azure-Diensten

Windows Server 2016 kombiniert die leistungsstarke, sichere Bereitstellung von Desktops und Apps über Remotedesktopdienste mit den flexiblen, skalierbaren Diensten, die von Microsoft Azure bereitgestellt werden. Sie können RDS mit Azure-Diensten bereitstellen, um die Infrastruktur-Wartungskosten für lokale Server reduzieren zu helfen, um die Stabilität mithilfe von Azure-Diensten, die Hochverfügbarkeit sicherstellen, zu erhöhen, um die Sicherheit mithilfe von mehrstufiger Authentifizierung zu verbessern und um das Erlebnis Ihrer Benutzer zu verbessern, indem Sie vorhandene Identitäten für den Zugriff auf Ressourcen in RDS verwenden.

Verwenden Sie die folgende Informationen, um Azure in Ihre Remotedesktopbereitstellung zu integrieren:

- [Informationen zur Verwendung der Multi-Factor Authentication mit RDS](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [Integration von Azure Active Directory Domain Services mit der RDS-Bereitstellung](rds-azure-adds.md)
- [Veröffentlichen von Remotedesktop mit Azure AD-Anwendungsproxy](/azure/active-directory/application-proxy-publish-remote-desktop)

Um zu erfahren, wie diese Dienste die Architektur Ihrer Remotedesktopbereitstellung vereinfachen, lesen Sie [RDS-Architekturen mit eindeutigen Azure-PaaS-Rollen](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles).