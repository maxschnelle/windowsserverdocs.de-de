---
title: 'RDS: Integration mit Azure-Diensten'
description: Erfahren Sie, wie Sie RDS in Ihre Azure-Bereitstellung und Azure in Ihre RDS-Bereitstellung integrieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.openlocfilehash: e582612496591356ed96b34522333d0e8bf34093
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712609"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>Remotedesktopdienste: Integration mit Azure-Diensten

Windows Server 2016 kombiniert die leistungsstarke, sichere Bereitstellung von Desktops und Apps über Remotedesktopdienste mit den flexiblen, skalierbaren Diensten, die von Microsoft Azure bereitgestellt werden. Sie können RDS mit Azure-Diensten bereitstellen, um die Infrastruktur-Wartungskosten für lokale Server reduzieren zu helfen, um die Stabilität mithilfe von Azure-Diensten, die Hochverfügbarkeit sicherstellen, zu erhöhen, um die Sicherheit mithilfe von mehrstufiger Authentifizierung zu verbessern und um das Erlebnis Ihrer Benutzer zu verbessern, indem Sie vorhandene Identitäten für den Zugriff auf Ressourcen in RDS verwenden.

Verwenden Sie die folgende Informationen, um Azure in Ihre Remotedesktopbereitstellung zu integrieren:

- [Informationen zur Verwendung der Multi-Factor Authentication mit RDS](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [Integration von Azure Active Directory Domain Services mit der RDS-Bereitstellung](rds-azure-adds.md)
- [Veröffentlichen von Remotedesktop mit Azure AD-Anwendungsproxy](/azure/active-directory/application-proxy-publish-remote-desktop)

Um zu erfahren, wie diese Dienste die Architektur Ihrer Remotedesktopbereitstellung vereinfachen, lesen Sie [RDS-Architekturen mit eindeutigen Azure-PaaS-Rollen](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles).