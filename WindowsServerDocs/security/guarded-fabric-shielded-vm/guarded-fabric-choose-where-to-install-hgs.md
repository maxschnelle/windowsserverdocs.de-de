---
title: Wählen Sie, ob Sie Host-Überwachungsdienst in eine eigene neue Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installieren
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4e02cd37391e629c9b947095fe32626bd15726ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827501"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>Wählen Sie, ob Sie Host-Überwachungsdienst in eigenen dedizierten Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur installieren

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Active Directory-Gesamtstruktur für die Host-Überwachungsdienst ist vertrauliche, weil die Administratoren Zugriff auf die Schlüssel, dass das Steuerelement von abgeschirmten VMs. Die Standardinstallation wird Einrichten einer neuen Gesamtstruktur dedizierte für Host-Überwachungsdienst und andere Abhängigkeiten konfigurieren. Diese Option wird empfohlen, da die Umgebung ist in sich geschlossen und bekannt, dass Sie sicher sein, bei der Erstellung. 

Die nur für technische Voraussetzung für die Installation von Host-Überwachungsdienst in einer vorhandenen Gesamtstruktur ist, dass sie der Root-Domäne hinzugefügt werden; nicht-Root-Domänen werden nicht unterstützt. Es gibt jedoch auch operativen Anforderungen und Sicherheits-best Practices für die Verwendung einer vorhandenen Gesamtstruktur. Geeignete Gesamtstrukturen werden absichtlich erstellt, um eine vertrauliche-Funktion, wie z. B. der Gesamtstruktur ein, die zu verarbeiten [Privileged Access Management für AD DS](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) oder [Enhanced Security Administrative Umgebung (esae-Basierter) Gesamtstruktur](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM). Diese Gesamtstrukturen weisen in der Regel die folgenden Merkmale auf:

- Sie haben einige Administratoren (getrennt von der Fabric-Administratoren)
- Sie haben eine geringe Anzahl von Anmeldungen
- Sie sind nicht ihrem Wesen nach allgemeine 

Allgemeiner Gesamtstrukturen wie z. B. Produktionsgesamtstrukturen eignen sich nicht von Host-Überwachungsdienst verwendet werden. Fabric-Gesamtstrukturen sind auch ungeeignet, da Host-Überwachungsdienst von Fabric-Administratoren isoliert sein muss.

## <a name="next-step"></a>Nächster Schritt

Wählen Sie die Option für die Installation, die Ihre Umgebung am besten geeignet ist:

- [Host-Überwachungsdienst in eigenen dedizierten Gesamtstruktur installieren](guarded-fabric-install-hgs-default.md)
- [Host-Überwachungsdienst in einer vorhandenen geschützten Gesamtstruktur installieren](guarded-fabric-install-hgs-in-a-bastion-forest.md)


