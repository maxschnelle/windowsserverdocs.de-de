---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: Sammeln von Informationen zum Netzwerk
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6792d565e08a188e1957c67ce419676d4a044d82
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624388"
---
# <a name="collecting-network-information"></a>Sammeln von Informationen zum Netzwerk

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der erste Schritt beim Entwerfen einer effektiven Standort Topologie in Active Directory Domain Services (AD DS) besteht darin, die Netzwerkgruppe Ihrer Organisation zu bitten, Informationen zu sammeln und regelmäßig über die physische Netzwerktopologie mit Ihnen zu kommunizieren.

## <a name="creating-a-location-map"></a>Erstellen einer Location map

Erstellen Sie eine Standort Zuordnung, die die physische Netzwerkinfrastruktur Ihres Unternehmens darstellt. Identifizieren Sie auf der Location map die geografischen Standorte, die Gruppen von Computern mit interner Konnektivität von 10 meits pro Sekunde (Mbit/s) oder höher (LAN-Geschwindigkeit (Local Area Network) oder höher) enthalten.

## <a name="listing-communication-links-and-available-bandwidth"></a>Auflisten von Kommunikations Links und verfügbarer Bandbreite

Nachdem Sie eine Speicherort Zuordnung erstellt haben, dokumentieren Sie den Typ des Kommunikations Links, seine Verbindungsgeschwindigkeit und die verfügbare Bandbreite zwischen den einzelnen Standorten. Rufen Sie eine WAN-Topologie (Wide Area Network) von ihrer Netzwerkgruppe ab. Eine Liste der allgemeinen WAN-Verbindungstypen und ihrer Bandbreiten finden Sie im Abschnitt "Bestimmen der Kosten" unter [Erstellen eines Standort](../../ad-ds/plan/Creating-a-Site-Link-Design.md)Verknüpfungs Entwurfs. Sie benötigen diese Informationen, um später im Entwurfsprozess der Standort Topologie Standort Verknüpfungen zu erstellen.

Bandbreite bezieht sich auf die Datenmenge, die Sie in einem bestimmten Zeitraum über einen Kommunikationskanal übertragen können. Verfügbare Bandbreite bezieht sich auf die Menge an Bandbreite, die zur Verwendung durch AD DS tatsächlich verfügbar ist. Sie können Informationen zur verfügbaren Bandbreite von ihrer Netzwerkgruppe abrufen, oder Sie können den Datenverkehr auf den einzelnen Links analysieren, indem Sie eine Protokollanalyse wie Netzwerkmonitor verwenden. Weitere Informationen zum Installieren von Netzwerkmonitor finden Sie im Artikel über [Wachen von Netzwerk Datenverkehr](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc783075(v=ws.10)).

Dokumentieren Sie jeden Standort und die anderen verknüpften Speicherorte. Notieren Sie außerdem den Typ der Kommunikations Verknüpfung und die verfügbare Bandbreite. Ein Arbeitsblatt, das Sie bei der Auflistung von Kommunikations Verknüpfungen und der verfügbaren Bandbreite unterstützt, finden Sie unter [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Herunterladen von Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Öffnen von "geografische Standorte und Kommunikations Links" (DSSTOPO_1. doc).

## <a name="listing-ip-subnets-within-each-location"></a>Auflisten von IP-Subnetzen an jedem Standort

Nachdem Sie die Kommunikations Links und die verfügbare Bandbreite zwischen den einzelnen Standorten dokumentiert haben, notieren Sie die IP-Subnetze innerhalb der einzelnen Speicherorte. Wenn Sie die Subnetzmaske und die IP-Adresse innerhalb der einzelnen Speicherorte nicht bereits kennen, wenden Sie sich an Ihre Netzwerkgruppe.

AD DS ordnet eine Arbeitsstation einem Standort zu, indem Sie die IP-Adresse der Arbeitsstation mit den Subnetzen vergleicht, die den einzelnen Standorten zugeordnet sind. Wenn Sie einer Domäne Domänen Controller hinzufügen, werden AD DS auch Ihre IP-Adressen untersucht und am am besten geeigneten Standort platziert.

Ein Arbeitsblatt, das Sie beim Auflisten der IP-Subnetze an den einzelnen Standorten unterstützt, finden Sie unter [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Herunterladen von Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Öffnen von "Speicherorten und Subnetzen" (DSSTOPO_2. doc).

> [!NOTE]
> Zusätzlich zu IPv4-Adressen (IP Version 4) unterstützt Windows Server auch IPv6-Subnetzpräfixe (IP Version 6). Ein Arbeitsblatt, das Sie beim Auflisten der IPv6-Subnetzpräfixe unterstützt, finden Sie unter [Anhang a: Standorte und Subnetzpräfixe](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md).

## <a name="listing-domains-and-number-of-users-for-each-location"></a>Auflisten von Domänen und der Anzahl von Benutzern für jeden Standort

Die Anzahl der Benutzer für jede regionale Domäne, die an einem Standort dargestellt wird, ist einer der Faktoren, die die Platzierung von regionalen Domänen Controllern und globalen Katalog Servern bestimmen. Dies ist der nächste Schritt im Entwurfsprozess der Standort Topologie. Planen Sie z. b., einen regionalen Domänen Controller an einem Speicherort zu platzieren, der mehr als 100 regionale Domänen Benutzer enthält, damit Sie sich weiterhin bei der Domäne anmelden können, wenn die WAN-Verbindung fehlschlägt.

Notieren Sie die Standorte, die an jedem Standort dargestellten Domänen und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird. Ein Arbeitsblatt, in dem Sie die Domänen und die Anzahl der an jedem Standort dargestellten Benutzer auflisten können, finden Sie unter [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Herunterladen von Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Öffnen von "Domänen und Benutzer an jedem Standort" (DSSTOPO_3. doc).
