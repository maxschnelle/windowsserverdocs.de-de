---
title: Installieren des vertrauenswürdigen TPM-Stammzertifikate
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/11/2018
ms.openlocfilehash: 65c5eb25f7a98e4db6a44e705a2968f185f3f962
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447378"
---
# <a name="install-trusted-tpm-root-certificates"></a>Installieren des vertrauenswürdigen TPM-Stammzertifikate

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie Host-Überwachungsdienst auf TPM-nachweisen konfiguriert haben, müssen Sie auch so konfigurieren Sie HGS für die Verwendung der Hersteller die TPMs in Ihren Servern vertrauen.
Dieser zusätzliche Überprüfung wird sichergestellt, dass nur die TPMs authentischen und trustworthy mit Ihrem Host-Überwachungsdienst bestätigen können.
Wenn Sie versuchen, eine nicht vertrauenswürdige TPM mit registrieren `Add-HgsAttestationTpmHost`, erhalten Sie eine Fehlermeldung, der angibt, der TPM-Hersteller ist nicht vertrauenswürdig.

Um Ihre TPMs vertrauen zu können, müssen die Stamm- und Signierung Zwischenzertifikate, die sich den Endorsement Key in Ihrer Server TPMs auf Host-Überwachungsdienst installiert werden.
Wenn Sie mehr als eine TPM-Modell in Ihrem Datencenter verwenden, müssen Sie möglicherweise verschiedene Zertifikate für jedes Modell zu installieren.
Host-Überwachungsdienst sieht in der "TrustedTPM_RootCA" und "TrustedTPM_IntermediateCA" der Zertifikatspeicher für die Anbieter-Zertifikate.

> [!NOTE]
> Die TPM-Hersteller-Zertifikate unterscheiden sich von denen standardmäßig unter Windows installiert und die spezifische Stamm und Zwischenzertifikate von TPM-Hersteller verwendet dar.

Eine Auflistung von vertrauenswürdigen TPM-Stammzertifizierungsstellen und Zwischenzertifizierungsstellen-Zertifikate wird der Einfachheit halber von Microsoft veröffentlicht.
Sie können die folgenden Schritte zum Installieren dieser Zertifikate verwenden.
Wenn Ihr TPM-Zertifikate nicht in der folgenden Paket enthalten sind, wenden Sie sich an Ihre TPM-Hersteller oder OEM-Server, um die Stamm- und Zwischenzertifikate für Ihre spezifischen TPM-Modell zu erhalten.

Wiederholen Sie die folgenden Schritte auf **jeder HGS-Server**:

1.  Laden Sie das neueste Paket aus [ https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab ](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

2.  Erweitern Sie die Cab-Datei aus.

    ```
    mkdir .\TrustedTPM
    expand.exe -F:* <Path-To-TrustedTpm.cab> .\TrustedTPM
    ```

3.  Standardmäßig wird das Konfigurationsskript Zertifikate für jedes TPM-Anbieter installieren. Wenn Sie nur das Importieren von Zertifikaten für Ihre spezifischen TPM-Hersteller möchten, löschen Sie die Ordner für TPM-Hersteller, die von Ihrer Organisation nicht vertraut.

4.  Installieren Sie das vertrauenswürdige Zertifikatspaket durch Ausführen des Setupskripts im Ordner "Erweitert".

    ```
    cd .\TrustedTPM
    .\setup.cmd
    ```

Um neue Zertifikate oder solche absichtlich nicht während einer früheren Installation hinzuzufügen, wiederholen Sie einfach die oben genannten Schritte auf jedem Knoten im Cluster-Host-Überwachungsdienst.
Bleiben vorhandene Zertifikate vertrauenswürdiger, aber neue Zertifikate finden Sie in der erweiterten Cab-Datei werden hinzugefügt, das vertrauenswürdige TPM gespeichert.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns-tpm.md)



