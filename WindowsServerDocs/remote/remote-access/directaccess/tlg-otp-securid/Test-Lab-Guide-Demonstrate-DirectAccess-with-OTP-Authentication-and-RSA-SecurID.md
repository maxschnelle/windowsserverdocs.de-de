---
title: 'Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: 10c7a49c-5671-4bec-b562-13fdd67f4629
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 90ffbb012c927e689f1ae852fdf7704520bc098d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958538"
---
# <a name="test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid"></a>Testumgebungsanleitung: Vorführung von DirectAccess mit OTP-Authentifizierung und RSA SecurID

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Der Remote Zugriff ist eine Server Rolle im Betriebssystem Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, das Remote Benutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder virtuelle private Netzwerke (Virtual Private Networks, VPNs) mit dem Routing-und RAS-Dienst (RRAS) ermöglicht. Diese Anleitung enthält Schritt-für-Schritt-Anweisungen zum Erweitern der [Test Umgebungs Anleitung: veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004) , um eine Konfiguration des einmaligen Zugriffs per Remote Zugriff zu veranschaulichen.

> [!WARNING]
> Der Entwurf dieser Test Umgebungs Anleitung umfasst Infrastruktur Server, z. b. einen Domänen Controller und eine Zertifizierungsstelle (Certification Authority, ca), die entweder Windows Server 2012 R2 oder Windows Server 2012 ausführen. Die Verwendung dieser Test Umgebungs Anleitung zum Konfigurieren von Infrastruktur Servern, auf denen andere Betriebssysteme ausgeführt werden, wurde nicht getestet, und Anweisungen zum Konfigurieren anderer Betriebssysteme sind in diesem Handbuch nicht enthalten.

## <a name="about-this-guide"></a>Über diesen Leitfaden
Der Remote Zugriff in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 bietet Unterstützung für die Client Authentifizierung mit OTP. Im Rahmen dieser Testumgebung wird nur RSA SecurID verwendet, um die OTP-Funktionalität mit Remote Zugriff zu veranschaulichen. Andere auf RADIUS basierende OTP-Lösungen werden ebenfalls unterstützt, sind jedoch außerhalb des Umfangs dieses Testlabors. Diese Anleitung enthält Anweisungen zum Konfigurieren und Veranschaulichen des Remotezugriffs mit sechs Servern und zwei Clientcomputern. Der abgeschlossene Remote Zugriff mit OTP-Test Labor simuliert ein Intranet, das Internet und ein Heimnetzwerk und veranschaulicht die Remote Zugriffs Funktionalität in verschiedenen Internetverbindungs Szenarien.

> [!IMPORTANT]
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.



