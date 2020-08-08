---
title: Datagram TLS-Protokoll (Transport Layer Security)
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: adf57e05cd759d2524782507d6f3ce5f90e0d702
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954797"
---
# <a name="datagram-transport-layer-security-protocol"></a>Datagram TLS-Protokoll (Transport Layer Security)

Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

In diesem Referenz Thema für IT-Experten wird das DTLS-Protokoll (Datagram Transport Layer Security) beschrieben, das Teil des SChannel Security Support Provider (SSP) ist.

## <a name="BKMK_DTLS"></a>
Das DTLS-Protokoll, das im Schannel SSP in Windows Server 2012 und Windows 8 eingeführt wurde, bietet Kommunikationsdaten Schutz für Datagramm-Protokolle. Informationen dazu, welche DTLS-Version in Windows-Versionen unterstützt wird, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx). Das Protokoll ermöglicht Client- und Serveranwendungen, so zu kommunizieren, dass Lauschangriffe, Manipulationen oder Nachrichtenfälschung verhindert werden. Das DTLS-Protokoll basiert auf dem Transport Layer Security-Protokoll (TLS) und bietet gleichwertige Sicherheitsgarantien. Dies mindert die Notwendigkeit, IPsec zu verwenden oder ein benutzerdefiniertes Sicherheitsprotokoll für die Anwendungsschicht zu entwerfen.

Datagramme sind häufig in Streamingmedien, z. b. Spiele oder gesicherte Videokonferenzen. Entwickler können Anwendungen entwickeln, um das DTLS-Protokoll im Kontext des SSPI-Modells (Security Support Provider Interface) der Windows-Authentifizierung zu verwenden, um die Kommunikation zwischen Clients und Servern zu sichern. Das DTLS-Protokoll basiert auf dem User Datagram-Protokoll (UDP). DTLS ist so konzipiert, dass es so ähnlich wie möglich ist, um die neue Sicherheits Erfindung zu minimieren und den Umfang der Code-und Infrastruktur Wiederverwendung zu maximieren.

Die Verschlüsselungs Sammlungen, die für die Konfiguration verfügbar sind, werden nach den für die Konfiguration konfigurierten Verschlüsselungs Sammlungen gemustert. RC4 ist nicht zulässig. SChannel verwendet weiterhin Cryptography Next Generation (CNG). Dadurch wird die in Windows Vista eingeführte in Windows Vista eingeführte PPS 140-Zertifizierung genutzt.

## <a name="additional-references"></a>Weitere Verweise

[IETF RFC 4347 Datagram Transport Layer Security](http://tools.ietf.org/html/rfc4347)


