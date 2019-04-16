---
title: Datagram Transport Layer Security-Protokoll
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
ms.date: 10/12/2016
ms.openlocfilehash: 31c1cf1f3218c0511a4407b560be30d0c6f86233
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# Datagram Transport Layer Security-Protokoll

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Referenzthema für IT-Experten werden das Datagram Transport Layer Security (DTLS)-Protokoll, das Teil des Schannel Security Support Provider (SSP) beschrieben.

## <a name="BKMK_DTLS"></a>
In der Schannel-SSP in Windows Server2012 und Windows8 eingeführt wurde, enthält das DTLS-Protokoll Kommunikation datagrammprotokollen für Datenschutz. Informationen darüber, welche DTLS Version in Windows-Versionen unterstützt wird, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx). Das Protokoll ermöglicht Client- und Serveranwendungen, die in einer Weise zu kommunizieren, dass Lauschangriffe, Manipulationen oder nachrichtenfälschung verhindert. Das DTLS-Protokoll basiert auf dem Transport Layer Security (TLS)-Protokoll, und bietet gleichwertige Sicherheitsgarantien, das Reduzieren der Notwendigkeit, IPsec zu verwenden oder eine benutzerdefinierte Anwendungsschicht zu entwerfen.

Datagramme werden häufig beim Streamen von Medien, z.B. spielen oder sicheren Videokonferenzen. Entwickler können Anwendungsentwicklung, das DTLS-Protokoll im Kontext des Modells Security Support Provider-Schnittstelle (SSPI) Windows-Authentifizierung verwenden, um die Kommunikation zwischen Clients und Servern zu schützen. Das DTLS-Protokoll basiert auf das Protokoll UDP (User Datagram). DTLS, TLS so ähnlich wie möglich, um infrastrukturwiederverwendung zu minimieren und die Menge der Code- und Maximieren werden soll.

Der Verschlüsselungssammlungen, die für die Konfiguration verfügbar sind, werden nach den abgebildet, die Sie für TLS konfigurieren können. RC4 ist nicht zulässig. Schannel nutzt weiterhin Cryptography Next Generation (CNG) zu verwenden. Dies nutzt FIPS 140-Zertifizierung, die in Windows Vista eingeführt wurde.

## Siehe auch

[IETF RFC 4347 Datagram Transport Layer Security](http://tools.ietf.org/html/rfc4347)


