---
title: Datagramm-TLS-Protokoll (Transport Layer Security)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: 6f8d7d10ccaace0f75bb470647e3f4571940d9c0
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284327"
---
# <a name="datagram-transport-layer-security-protocol"></a>Datagramm-TLS-Protokoll (Transport Layer Security)

WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

In diesem Referenzthema für IT-Experten wird beschrieben, das Datagram Transport Layer Security (DTLS)-Protokoll, das Teil von Schannel Security Support Provider (SSP) ist.

## <a name="BKMK_DTLS"></a>
Im Schannel SSP in Windows Server 2012 und Windows 8 eingeführt, bietet das DTLS-Protokoll Kommunikation datagrammprotokollen für Datenschutz. Informationen über die DTLS-Version wird in Windows-Versionen unterstützt, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx). Das Protokoll ermöglicht Client- und Serveranwendungen, so zu kommunizieren, dass Lauschangriffe, Manipulationen oder Nachrichtenfälschung verhindert werden. Das DTLS-Protokoll basiert auf dem Transport Layer Security-Protokoll (TLS) und bietet gleichwertige Sicherheitsgarantien. Dies mindert die Notwendigkeit, IPsec zu verwenden oder ein benutzerdefiniertes Sicherheitsprotokoll für die Anwendungsschicht zu entwerfen.

Datagramme werden häufig beim Streamen von Medien, wie z. B. spielen oder sicheren Videokonferenzen. Entwickler können Anwendungen das DTLS-Protokoll, im Rahmen der Security Support Provider Interface (SSPI)-Modell von Windows-Authentifizierung verwenden, zum Sichern der Kommunikation zwischen Clients und Servern entwickeln. Das DTLS-Protokoll basiert auf dem Protokoll UDP (User Datagram). DTLS soll TLS so ähnlich wie möglich um infrastrukturwiederverwendung zu minimieren und Maximieren Sie die Menge an Code und die Infrastruktur wiederverwendet werden.

Die Verschlüsselungssammlungen, die für die Konfiguration verfügbar sind, sind nach den abgebildet, die Sie für TLS konfigurieren können. RC4 ist nicht zulässig. Schannel nutzt weiterhin Cryptography Next Generation (CNG). Diese nutzt die Vorteile der FIPS 140-Zertifizierung, die in Windows Vista eingeführt wurde.

## <a name="see-also"></a>Siehe auch

[IETF RFC 4347 Datagram Transport Layer Security](http://tools.ietf.org/html/rfc4347)


