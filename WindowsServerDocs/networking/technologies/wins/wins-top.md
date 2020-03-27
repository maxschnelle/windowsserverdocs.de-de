---
title: Windows Internet Name Service (WINS)
description: Dieses Thema enthält Informationen zur Außerbetriebnahme von WINS und zum Verwenden von DNS für die Namensauflösungsdienste in Ihrem Netzwerk.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 54e3f69500ccb3dbf6b2dfe47f6dd035e0a20511
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315166"
---
#  <a name="windows-internet-name-service-wins"></a>Windows Internet Name Service (WINS)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet.

Wenn WINS nicht bereits in Ihrem Netzwerk bereitgestellt wurde, stellen Sie WINS stattdessen bereit, und stellen Sie Domain Name System \(DNS-\)bereit. DNS bietet auch Dienste für die Registrierung und Auflösung von Computernamen und umfasst viele zusätzliche Vorteile gegenüber WINS, wie z. b. die Integration mit Active Directory Domain Services.

Weitere Informationen finden Sie unter [Domain Name System (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

Wenn Sie WINS bereits in Ihrem Netzwerk bereitgestellt haben, wird empfohlen, dass Sie DNS bereitstellen und dann WINS außer Betrieb setzen.
