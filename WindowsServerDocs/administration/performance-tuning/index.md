---
title: 'Windows Server 2016: Richtlinien zur Optimierung der Leistung'
description: Richtlinien zur Optimierung der Leistung für Windows Server 2016
ms.topic: landing-page
ms.author: phstee
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 69b65e9a7cb5e935a8c6b1a8ab500e33307a092d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896698"
---
# <a name="performance-tuning-guidelines-for-windows-server-2016"></a>Richtlinien zur Optimierung der Leistung für Windows Server 2016

Wenn Sie ein Serversystem in Ihrer Organisation ausführen, werden die geschäftlichen Anforderungen mit Standardservereinstellungen möglicherweise nicht erfüllt. Beispielsweise benötigen Sie vielleicht den niedrigstmöglichen Energieverbrauch, die niedrigstmögliche Latenz oder den maximal möglichen Durchsatz auf Ihrem Server. Dieses Handbuch enthält eine Reihe von Richtlinien, mit denen Sie die Servereinstellungen in Windows Server 2016 optimieren und Leistungs- oder Energieeffizienzsteigerungen erzielen können, insbesondere wenn sich die Art der Auslastung im Laufe der Zeit nur wenig ändert.

Es ist wichtig, dass Sie bei Ihren Optimierungsänderungen die Hardware, die Arbeitsauslastung, den Energiehaushalt und die Leistungsziele Ihres Servers berücksichtigen. In diesem Handbuch werden jede Einstellung und ihre möglichen Auswirkungen beschrieben, damit sie eine fundierte Entscheidung bezüglich ihrer Relevanz für Ihr System, Ihre Arbeitsauslastung, Leistung und Energienutzungsziele treffen können.

> [!warning]
> Registrierungseinstellungen und Optimierungsparameter haben sich von Version zu Version von Windows Server erheblich geändert. Achten Sie darauf, aktuelle Optimierungsrichtlinien zu verwenden, um unerwartete Ergebnisse zu vermeiden.

## <a name="in-this-guide"></a>Inhalt dieser Anleitung
Die Leitfäden zu Leistung und Optimierung für Windows Server 2016 sind in diesem Handbuch in drei Optimierungskategorien gegliedert:

|Serverhardware | Serverrolle | Serversubsystem |
|:---:|:---:|:---:|
|[Überlegungen zur Hardwareleistung](hardware/index.md) |[Active Directory-Server](role/active-directory-server/index.md) |[Cache- und Arbeitsspeicherverwaltung](subsystem/cache-memory-management/index.md)|
|[Überlegungen zum Hardwareenergiebedarf](hardware/power.md)|[Dateiserver](role/file-server/index.md)|[Netzwerksubsystem](../../networking/technologies/network-subsystem/net-sub-performance-top.md)|
||[Hyper-V-Server](role/hyper-v-server/index.md)|[Direkte Speicherplätze](subsystem/storage-spaces-direct/index.md)|
||[Remotedesktopdienste](role/remote-desktop/session-hosts.md)|[Software-Defined Networking (SDN)](subsystem/software-defined-networking/index.md)|
||[Webserver](role/web-server/index.md)||
||[Windows Server-Container](role/windows-server-container/index.md)||


## <a name="changes-in-this-version"></a>Änderungen in dieser Version

### <a name="sections-added"></a>Hinzugefügte Abschnitte
- [Überlegungen zur Konfiguration des Nano Server-Installationstyps](../../get-started/getting-started-with-nano-server.md)


- [Software Defined Networking](subsystem/software-defined-networking/index.md), einschließlich [HNV](subsystem/software-defined-networking/hnv-gateway-performance.md) und [SLB-Gateway-Konfigurationsleitfaden](subsystem/software-defined-networking/slb-gateway-performance.md)

- [Direkte Speicherplätze](subsystem/storage-spaces-direct/index.md)

- [HTTP1.1 und HTTP2](role/web-server/http-performance.md)

- [Windows Server-Container](role/windows-server-container/index.md)

### <a name="sections-changed"></a>Geänderte Abschnitte

- Updates des Abschnitts [Active Directory-Leitfaden](role/active-directory-server/index.md)

- Updates des Abschnitts [Dateiserverleitfaden](role/file-server/index.md)

- Updates des Abschnitts [Webserverleitfaden](role/web-server/index.md)

- Updates des Abschnitts [Hardwareenergiebedarf-Leitfaden](hardware/power.md)

- Updates des Abschnitts [PowerShell-Optimierungsleitfaden](powershell/index.md)

- Wichtige Updates des Abschnitts [Hyper-V-Leitfaden](role/hyper-v-server/index.md)

- *Leistungsoptimierung für Auslastungen wurde entfernt*, Zeiger zu relevanten Ressourcen wurden dem [Artikel über zusätzliche Optimierungsressourcen](additional-resources.md) hinzugefügt

- *Entfernen dedizierter Speicherabschnitte* zugunsten des neuen Abschnitts [Direkte Speicherplätze](subsystem/storage-spaces-direct/index.md) und von kanonischem TechNet-Inhalt

- *Entfernen des dedizierten Netzwerkabschnitts* zugunsten von kanonischem TechNet-Inhalt
