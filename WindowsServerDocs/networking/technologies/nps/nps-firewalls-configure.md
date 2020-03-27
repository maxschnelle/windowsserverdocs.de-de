---
title: Konfigurieren von Firewalls für den RADIUS-Datenverkehr
description: Dieses Thema bietet einen Überblick über die Konfiguration von Firewalls, um RADIUS-Datenverkehr für den Netzwerk Richtlinien Server unter Windows Server 2016 zuzulassen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 57661fee2cf633a1efe8e264b0f7fe717b81e20d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316096"
---
# <a name="configure-firewalls-for-radius-traffic"></a>Konfigurieren von Firewalls für den RADIUS-Datenverkehr

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Firewalls können so konfiguriert werden, dass Sie Typen von IP-Datenverkehr auf den Computer oder das Gerät, auf dem die Firewall ausgeführt wird, zulassen oder blockieren. Wenn Firewalls nicht ordnungsgemäß konfiguriert sind, um RADIUS-Datenverkehr zwischen RADIUS-Clients, RADIUS-Proxys und RADIUS-Servern zuzulassen, kann die Netzwerk Zugriffs Authentifizierung fehlschlagen, sodass Benutzer keinen Zugriff auf Netzwerkressourcen haben 

Möglicherweise müssen Sie zwei Arten von Firewalls konfigurieren, um RADIUS-Datenverkehr zuzulassen:

- Windows Defender Firewall mit erweiterter Sicherheit auf dem lokalen Server, auf dem der Netzwerk Richtlinien Server (NPS) ausgeführt wird.
- Firewalls, die auf anderen Computern oder Hardware Geräten ausgeführt werden.

## <a name="windows-firewall-on-the-local-nps"></a>Windows-Firewall auf dem lokalen NPS

Standardmäßig sendet und empfängt NPS RADIUS-Datenverkehr über das User Datagram-Protokoll \(UDP\) Ports 1812, 1813, 1645 und 1646. Die Windows Defender Firewall auf dem NPS wird während der Installation von NPS automatisch mit Ausnahmen konfiguriert, damit dieser RADIUS-Datenverkehr gesendet und empfangen werden kann.

Wenn Sie also die UDP-Standardports verwenden, müssen Sie die Konfiguration von Windows Defender Firewall nicht ändern, um RADIUS-Datenverkehr zu und von NPSS zuzulassen.

In einigen Fällen möchten Sie möglicherweise die Ports ändern, die NPS für RADIUS-Datenverkehr verwendet. Wenn Sie NPS und Ihre Netzwerk Zugriffs Server für das Senden und empfangen von RADIUS-Datenverkehr über andere Ports als die Standardeinstellungen konfigurieren, gehen Sie wie folgt vor:

- Entfernen Sie die Ausnahmen, die RADIUS-Datenverkehr auf den Standardports zulassen.
- Erstellen Sie neue Ausnahmen, die RADIUS-Datenverkehr für die neuen Ports zulassen.

Weitere Informationen finden Sie unter [Konfigurieren von NPS-UDP-Port Informationen](nps-udp-ports-configure.md).

## <a name="other-firewalls"></a>Weitere Firewalls

In der gängigsten Konfiguration ist die Firewall mit dem Internet verbunden, und NPS ist eine Intranetressource, die mit dem Umkreis Netzwerk verbunden ist.

Um den Domänen Controller innerhalb des Intranets zu erreichen, hat der NPS möglicherweise Folgendes:

- Eine Schnittstelle im Umkreis Netzwerk und eine Schnittstelle im Intranet (IP-Routing ist nicht aktiviert). 
- Eine einzelne Schnittstelle im Umkreis Netzwerk. In dieser Konfiguration kommuniziert NPS über eine andere Firewall, die das Umkreis Netzwerk mit dem Intranet verbindet, mit Domänen Controllern.

## <a name="configuring-the-internet-firewall"></a>Konfigurieren der Internet Firewall

Die Firewall, die mit dem Internet verbunden ist, muss mit Eingabe-und Ausgabefiltern auf der Internet Schnittstelle \(und optional mit der zugehörigen Netzwerk Umkreis Schnittstelle\)konfiguriert werden, um die Weiterleitung von RADIUS-Nachrichten zwischen den NPS-und RADIUS-Clients oder Proxys im Internet zuzulassen. Zusätzliche Filter können verwendet werden, um das Übergeben von Datenverkehr an Webserver, VPN-Server und andere Server Typen im Umkreis Netzwerk zuzulassen.

Separate Eingabe-und Ausgabe Paketfilter können auf der Internet Schnittstelle und der Umkreis Netzwerkschnittstelle konfiguriert werden.

### <a name="configure-input-filters-on-the-internet-interface"></a>Konfigurieren von Eingabe Filtern an der Internet Schnittstelle

Konfigurieren Sie die folgenden Eingabe Paketfilter für die Internet Schnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1812 (0x714) des NPS.  Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1812.
- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1813 (0x715) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1813.
- \(optional\) Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1645 \(0x66D\) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(optional\) Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1646 \(0x66E\) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-internet-interface"></a>Konfigurieren von Ausgabefiltern an der Internet Schnittstelle

Konfigurieren Sie die folgenden Ausgabefilter für die Internet Schnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1812 (0x714) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1812.
- Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1813 (0x715) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1813.
- \(optional\) Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1645 \(0x66D\) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(optional\) Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1646 \(0x66E\) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>Konfigurieren von Eingabe Filtern an der Umkreis Netzwerkschnittstelle

Konfigurieren Sie die folgenden Eingabe Filter für die Umkreis Netzwerkschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1812 (0x714) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1812.
- Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1813 (0x715) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1813.
- \(optional\) Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1645 \(0x66D\) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(optional\) Quell-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Quellport 1646 \(0x66E\) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von NPS zu Internet basierten RADIUS-Clients. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>Konfigurieren von Ausgabefiltern an der Umkreis Netzwerkschnittstelle

Konfigurieren Sie die folgenden Ausgabe Paketfilter in der Umkreis Netzwerkschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1812 (0x714) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2865 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1812.
- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1813 (0x715) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der Standard-UDP-Port, der von NPS verwendet wird, wie in RFC 2866 definiert. Wenn Sie einen anderen Port verwenden, ersetzen Sie die Portnummer 1813.
- \(optional\) Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1645 \(0x66D\) des NPS. Dieser Filter ermöglicht RADIUS-Authentifizierungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.
- \(optional\) Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle und UDP-Zielport 1646 \(0x66E\) des NPS. Dieser Filter ermöglicht RADIUS-Buchhaltungs Datenverkehr von Internet basierten RADIUS-Clients an den NPS. Dies ist der UDP-Port, der von älteren RADIUS-Clients verwendet wird.

Zur zusätzlichen Sicherheit können Sie die IP-Adressen der einzelnen RADIUS-Clients, von denen die Pakete über die Firewall gesendet werden, verwenden, um Filter für den Datenverkehr zwischen dem Client und der IP-Adresse des NPS im Umkreis Netzwerk zu definieren.

### <a name="filters-on-the-perimeter-network-interface"></a>Filter für die Umkreis Netzwerkschnittstelle

Konfigurieren Sie die folgenden Eingabe Paketfilter in der Umkreis Netzwerkschnittstelle der Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Die Quell-IP-Adresse der Umkreis Netzwerkschnittstelle des NPS. Dieser Filter ermöglicht den Datenverkehr vom NPS im Umkreis Netzwerk.

Konfigurieren Sie die folgenden Ausgabefilter in der Umkreis Netzwerkschnittstelle der Intranetfirewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle des NPS. Dieser Filter ermöglicht den Datenverkehr zu den NPS im Umkreis Netzwerk.

### <a name="filters-on-the-intranet-interface"></a>Filter für die Intranetschnittstelle

Konfigurieren Sie die folgenden Eingabe Filter für die Intranetschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Ziel-IP-Adresse der Umkreis Netzwerkschnittstelle des NPS. Dieser Filter ermöglicht den Datenverkehr zu den NPS im Umkreis Netzwerk.

Konfigurieren Sie die folgenden Ausgabe Paketfilter für die Intranetschnittstelle der Firewall, um die folgenden Arten von Datenverkehr zuzulassen:

- Die Quell-IP-Adresse der Umkreis Netzwerkschnittstelle des NPS. Dieser Filter ermöglicht den Datenverkehr vom NPS im Umkreis Netzwerk.


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).




