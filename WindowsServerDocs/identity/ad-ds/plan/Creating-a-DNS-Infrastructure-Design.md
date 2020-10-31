---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: Erstellen eines Entwurfs der DNS-Infrastruktur
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: a0052c791a0af7184845be7bbdbc52db6e66f6f0
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068903"
---
# <a name="creating-a-dns-infrastructure-design"></a>Erstellen eines Entwurfs der DNS-Infrastruktur

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie Ihre Active Directory Gesamtstruktur-und Domänen Entwürfe erstellt haben, müssen Sie eine Domain Name System (DNS)-Infrastruktur entwerfen, um die logische Active Directory-Struktur zu unterstützen. DNS ermöglicht es Benutzern, anzeigen Amen zu verwenden, die sich leicht merken können, eine Verbindung mit Computern und anderen Ressourcen in IP-Netzwerken herzustellen. Für Active Directory Domain Services (AD DS) in Windows Server 2008 ist DNS erforderlich.

Der Prozess zum Entwerfen von DNS zur Unterstützung von AD DS variiert abhängig davon, ob Ihre Organisation bereits über einen DNS-Server Dienst verfügt oder Sie einen neuen DNS-Server Dienst bereitstellen:

- Wenn Sie bereits über eine vorhandene DNS-Infrastruktur verfügen, müssen Sie den Active Directory-Namespace in diese Umgebung integrieren. Weitere Informationen finden Sie unter [integrieren von AD DS in eine vorhandene DNS-Infrastruktur](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md).
- Wenn Sie nicht über eine DNS-Infrastruktur verfügen, müssen Sie eine neue DNS-Infrastruktur entwerfen und bereitstellen, um AD DS zu unterstützen. Weitere Informationen finden Sie unter Bereitstellen von [Domain Name System (DNS)](/previous-versions/windows/it-pro/windows-server-2003/cc780661(v=ws.10)).

Wenn Ihre Organisation über eine vorhandene DNS-Infrastruktur verfügt, müssen Sie sicherstellen, dass Sie verstehen, wie Ihre DNS-Infrastruktur mit dem Active Directory-Namespace interagiert. Für ein Arbeitsblatt, das Sie bei der Dokumentation Ihres vorhandenen DNS-Infrastruktur Entwurfs unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus den [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) herunter, und öffnen Sie "DNS Inventory" (DSSLOGI_8.doc).

> [!NOTE]
> Zusätzlich zu IPv4-Adressen (IP Version 4) unterstützt Windows Server auch IPv6-Adressen (IP Version 6). Ein Arbeitsblatt, das Sie beim Auflisten der IPv6-Adressen unterstützt, während Sie die Methode für die rekursive Namensauflösung Ihrer aktuellen DNS-Struktur dokumentieren, finden Sie unter [Anhang a: DNS-Inventur](../../ad-ds/plan/Appendix-A--DNS-Inventory.md).

Bevor Sie Ihre DNS-Infrastruktur für die Unterstützung von AD DS entwerfen, kann es hilfreich sein, sich über die DNS-Hierarchie, den DNS-Namens Auflösungsprozess und die Unterstützung von DNS AD DS zu informieren. Weitere Informationen zur DNS-Hierarchie und zum namens Auflösungsprozess finden Sie in der [technischen Referenz zu DNS](/previous-versions/windows/it-pro/windows-server-2003/cc779926(v=ws.10)). Weitere Informationen zur Unterstützung von AD DS durch DNS finden Sie unter [DNS-Unterstützung für Active Directory Technische Referenz](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10)).

## <a name="in-this-section"></a>In diesem Abschnitt

- [Überprüfen von DNS-Konzepten](../../ad-ds/plan/Reviewing-DNS-Concepts.md)
- [DNS und AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)
- [Zuweisen des DNS für die AD DS-Rolle „Besitzer“](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)
- [Integrieren der AD DS in eine vorhandene DNS-Infrastruktur](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)
