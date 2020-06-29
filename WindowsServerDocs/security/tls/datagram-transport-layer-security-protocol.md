---
title: Datagram TLS-Protokoll (Transport Layer Security)
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: 79477aa441b82854852fe35a9b45bafdee664532
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475267"
---
# <a name="datagram-transport-layer-security-protocol"></a>Datagram TLS-Protokoll (Transport Layer Security)

Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

In diesem Referenz Thema für IT-Experten wird das DTLS-Protokoll (Datagram Transport Layer Security) beschrieben, das Teil des SChannel Security Support Provider (SSP) ist.

## <a name="BKMK_DTLS"></a>
Das DTLS-Protokoll, das im Schannel SSP in Windows Server 2012 und Windows 8 eingeführt wurde, bietet Kommunikationsdaten Schutz für Datagramm-Protokolle. Informationen dazu, welche DTLS-Version in Windows-Versionen unterstützt wird, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx). Das Protokoll ermöglicht Client- und Serveranwendungen, so zu kommunizieren, dass Lauschangriffe, Manipulationen oder Nachrichtenfälschung verhindert werden. Das DTLS-Protokoll basiert auf dem Transport Layer Security-Protokoll (TLS) und bietet gleichwertige Sicherheitsgarantien. Dies mindert die Notwendigkeit, IPsec zu verwenden oder ein benutzerdefiniertes Sicherheitsprotokoll für die Anwendungsschicht zu entwerfen.

Datagramme sind häufig in Streamingmedien, z. b. Spiele oder gesicherte Videokonferenzen. Entwickler können Anwendungen entwickeln, um das DTLS-Protokoll im Kontext des SSPI-Modells (Security Support Provider Interface) der Windows-Authentifizierung zu verwenden, um die Kommunikation zwischen Clients und Servern zu sichern. Das DTLS-Protokoll basiert auf dem User Datagram-Protokoll (UDP). DTLS ist so konzipiert, dass es so ähnlich wie möglich ist, um die neue Sicherheits Erfindung zu minimieren und den Umfang der Code-und Infrastruktur Wiederverwendung zu maximieren.

Die Verschlüsselungs Sammlungen, die für die Konfiguration verfügbar sind, werden nach den für die Konfiguration konfigurierten Verschlüsselungs Sammlungen gemustert. RC4 ist nicht zulässig. SChannel verwendet weiterhin Cryptography Next Generation (CNG). Dadurch wird die in Windows Vista eingeführte in Windows Vista eingeführte PPS 140-Zertifizierung genutzt.

## <a name="additional-references"></a>Zusätzliche Referenzen

[IETF RFC 4347 Datagram Transport Layer Security](http://tools.ietf.org/html/rfc4347)


