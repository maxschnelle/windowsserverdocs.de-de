---
title: Wählen Sie aus, ob HGS in einer eigenen neuen Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installiert werden sollen.
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 52376a4e193b8021dc58214003e9b7579b096a79
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856883"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>Wählen Sie aus, ob HGS in einer eigenen dedizierten Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installiert werden.

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016


Die Active Directory-Gesamtstruktur für HGS ist sensibel, da die Administratoren Zugriff auf die Schlüssel haben, mit denen abgeschirmte VMS gesteuert werden. Bei der Standardinstallation wird eine neue, für HGS dedizierte Gesamtstruktur eingerichtet und andere Abhängigkeiten konfiguriert. Diese Option wird empfohlen, da die Umgebung eigenständig ist und bekanntermaßen sicher ist, wenn Sie erstellt wird. 

Die einzige Technische Voraussetzung für die Installation von HGS in einer vorhandenen Gesamtstruktur ist, dass Sie der Stamm Domäne hinzugefügt wird. nicht-Stamm Domänen werden nicht unterstützt. Es gibt aber auch Betriebsanforderungen und sicherheitsrelevante bewährte Methoden für die Verwendung einer vorhandenen Gesamtstruktur. Geeignete Gesamtstrukturen werden absichtlich erstellt, um eine sensible Funktion zu erfüllen, z. b. die Gesamtstruktur, die von [privileged Access Management für AD DS](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) oder eine [Erweiterte Sicherheits Verwaltungs Umgebung (ESAE)](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM)verwendet wird. Diese Gesamtstrukturen weisen in der Regel die folgenden Merkmale auf:

- Sie haben nur wenige Administratoren (getrennt von Fabric-Administratoren).
- Sie verfügen über eine geringe Anzahl von Anmeldungen.
- Dabei handelt es sich nicht um allgemeine Zwecke. 

Allgemeine Gesamtstrukturen, wie z. b. Produktions Gesamtstrukturen, sind nicht für die Verwendung durch HGS geeignet. Fabric-Gesamtstrukturen sind auch ungeeignet, da HGS von fabricadministratoren isoliert werden müssen.

## <a name="next-step"></a>Nächster Schritt

Wählen Sie die Installationsoption, die für Ihre Umgebung am besten geeignet ist:

- [Installieren von HGS in einer eigenen dedizierten Gesamtstruktur](guarded-fabric-install-hgs-default.md)
- [Installieren von HGS in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-install-hgs-in-a-bastion-forest.md)


