---
title: Windows Internet Name Service (WINS)
description: Dieses Thema enthält Informationen zur Außerbetriebnahme von WINS und zum Verwenden von DNS für die Namensauflösungsdienste in Ihrem Netzwerk.
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36dc2b0e8bbb6b65b0cc3568641017aa51122650
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955497"
---
#  <a name="windows-internet-name-service-wins"></a>Windows Internet Name Service (WINS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Windows Internet Name Service (WINS) ist ein Legacy Dienst für die Registrierung und Auflösung von Computernamen, der NetBIOS-Namen von Computern IP-Adressen zuordnet.

Wenn WINS nicht bereits in Ihrem Netzwerk bereitgestellt wurde, stellen Sie WINS stattdessen bereit, und stellen Sie Domain Name System \( DNS bereit \) . DNS bietet auch Dienste für die Registrierung und Auflösung von Computernamen und umfasst viele zusätzliche Vorteile gegenüber WINS, wie z. b. die Integration mit Active Directory Domain Services.

Weitere Informationen finden Sie unter [Domain Name System (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

Wenn Sie WINS bereits in Ihrem Netzwerk bereitgestellt haben, wird empfohlen, dass Sie DNS bereitstellen und dann WINS außer Betrieb setzen.
