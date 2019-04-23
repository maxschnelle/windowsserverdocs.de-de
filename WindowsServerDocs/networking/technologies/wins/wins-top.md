---
title: Windows Internet Name Service (WINS)
description: Dieses Thema enthält Informationen zum Außerbetriebsetzen von WINS, und Verwenden von DNS für Namensauflösungsdienste in Ihrem Netzwerk.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bbc1871d29021aa3c99f14368a4711dac63f4cee
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843631"
---
#  <a name="windows-internet-name-service-wins"></a>Windows Internet Name Service (WINS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Internet Name Service (WINS) ist ein älterer Registrierungs- und Auflösungsdienst für Computernamen, der einem Computer-NetBIOS-Namen eine IP-Adresse zuordnet.

Wenn Sie nicht bereits WINS in Ihrem Netzwerk bereitgestellt haben, nicht WINS - stattdessen bereitstellen, Domain Name System bereitstellen \(DNS\). DNS bietet Namen "Computer" die Dienste für Registrierung und Auflösung auch und umfasst zahlreiche zusätzliche Vorteile über WINS, z. B. Integration in Active Directory Domain Services.

Weitere Informationen finden Sie unter [Domain Name System (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

Wenn Sie WINS bereits in Ihrem Netzwerk bereitgestellt haben, empfiehlt es sich, dass Sie beim Bereitstellen von DNS und dann außer Betrieb WINS setzen.
