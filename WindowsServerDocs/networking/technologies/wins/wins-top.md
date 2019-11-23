---
title: Windows Internet Name Service (WINS)
description: Dieses Thema enthält Informationen zur Außerbetriebnahme von WINS und zum Verwenden von DNS für die Namensauflösungsdienste in Ihrem Netzwerk.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 219c313dfeb26319cd5f537df417724de7044648
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405244"
---
#  <a name="windows-internet-name-service-wins"></a>Windows Internet Name Service (WINS)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet.

Wenn WINS nicht bereits in Ihrem Netzwerk bereitgestellt wurde, stellen Sie WINS stattdessen bereit, und stellen Sie Domain Name System \(DNS-\)bereit. DNS bietet auch Dienste für die Registrierung und Auflösung von Computernamen und umfasst viele zusätzliche Vorteile gegenüber WINS, wie z. b. die Integration mit Active Directory Domain Services.

Weitere Informationen finden Sie unter [Domain Name System (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

Wenn Sie WINS bereits in Ihrem Netzwerk bereitgestellt haben, wird empfohlen, dass Sie DNS bereitstellen und dann WINS außer Betrieb setzen.
