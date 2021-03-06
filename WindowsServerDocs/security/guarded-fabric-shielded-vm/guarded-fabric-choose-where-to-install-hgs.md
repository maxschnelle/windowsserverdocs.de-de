---
title: Wählen Sie aus, ob HGS in einer eigenen neuen Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installiert werden sollen.
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: e1b4c015aa9b4f504d4cdf79bb2f38686588cfdd
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989535"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>Wählen Sie aus, ob HGS in einer eigenen dedizierten Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installiert werden.

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016


Die Active Directory-Gesamtstruktur für HGS ist sensibel, da die Administratoren Zugriff auf die Schlüssel haben, mit denen abgeschirmte VMS gesteuert werden.
Bei der Standardinstallation wird eine neue, für HGS dedizierte Gesamtstruktur eingerichtet und andere Abhängigkeiten konfiguriert.
Diese Option wird empfohlen, da die Umgebung eigenständig ist und bekanntermaßen sicher ist, wenn Sie erstellt wird.

Die einzige Technische Voraussetzung für die Installation von HGS in einer vorhandenen Gesamtstruktur ist, dass Sie der Stamm Domäne hinzugefügt wird. nicht-Stamm Domänen werden nicht unterstützt. Es gibt aber auch Betriebsanforderungen und sicherheitsrelevante bewährte Methoden für die Verwendung einer vorhandenen Gesamtstruktur.
Geeignete Gesamtstrukturen werden absichtlich erstellt, um eine sensible Funktion zu erfüllen, z. b. die Gesamtstruktur, die von [privileged Access Management für AD DS](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) oder eine [Erweiterte Sicherheits Verwaltungs Umgebung (ESAE)](../../identity/securing-privileged-access/securing-privileged-access-reference-material.md#esae-administrative-forest-design-approach)verwendet wird.
Diese Gesamtstrukturen weisen in der Regel die folgenden Merkmale auf:

- Sie haben nur wenige Administratoren (getrennt von Fabric-Administratoren).
- Sie verfügen über eine geringe Anzahl von Anmeldungen.
- Dabei handelt es sich nicht um allgemeine Zwecke.

Allgemeine Gesamtstrukturen, wie z. b. Produktions Gesamtstrukturen, sind nicht für die Verwendung durch HGS geeignet.
Fabric-Gesamtstrukturen sind auch ungeeignet, da HGS von fabricadministratoren isoliert werden müssen.

## <a name="next-step"></a>Nächster Schritt

Wählen Sie die Installationsoption, die für Ihre Umgebung am besten geeignet ist:

- [Installieren von HGS in einer eigenen dedizierten Gesamtstruktur](guarded-fabric-install-hgs-default.md)
- [Installieren von HGS in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-install-hgs-in-a-bastion-forest.md)