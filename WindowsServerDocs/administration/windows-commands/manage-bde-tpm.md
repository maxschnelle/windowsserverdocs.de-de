---
title: manage-bde TPM
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6495bfbfedea7219ae175145f72fc12314ce7ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839763"
---
# <a name="manage-bde-tpm"></a>manage-bde: TPM

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> [!IMPORTANT]
> Dieser Befehl wird nicht für die Verwendung auf Computern mit Windows 8, Windows Server 2012 oder höheren Betriebssystemen unterstützt. Für diese Computer können Sie die [TPM-Verwaltungs-Cmdlets für Windows PowerShell](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)verwenden.
> Wenn Sie diesen Befehl auf einem Computer mit Windows 7 oder Windows Server 2008 verwenden, können Sie die Trusted Platform Module des Computers (TPM) mithilfe dieses Befehls weiterhin konfigurieren. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).
> ## <a name="syntax"></a>Syntax
> ```
> manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
> ```
> #### <a name="parameters"></a>Parameter
> 
> |    Parameter    |                                                                              Beschreibung                                                                               |
> |-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |     -turnon     |              Aktiviert und aktiviert das TPM, sodass das TPM-Besitzer Kennwort festgelegt werden kann. Sie können auch **-t** als abgekürzte Version dieses Befehls verwenden.              |
> | -Take Ownership  |                      Übernimmt den Besitz des TPM durch Festlegen eines Besitzer Kennworts. Sie können **-o** auch als abgekürzte Version dieses Befehls verwenden.                       |
> | <OwnerPassword> |                                                      Stellt das Besitzer Kennwort dar, das Sie für das TPM angeben.                                                       |
> |  -Computername  | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
> |     <Name>      |    Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.     |
> |    -? oder /?     |                                                               Zeigt eine kurze Hilfe an der Eingabeaufforderung an.                                                               |
> |   -Help oder-h   |                                                             Zeigt die gesamte Hilfe an der Eingabeaufforderung an.                                                              |
> 
> ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
> Im folgenden Beispiel wird veranschaulicht, wie der **-TPM-** Befehl verwendet wird, um das TPM zu aktivieren.
> ```
> manage-bde  tpm -turnon
> ```
> Das folgende Beispiel veranschaulicht die Verwendung des **TPM** -Befehls, um den Besitz des TPM zu übernehmen und das Besitzer Kennwort auf 0wnerP@ssfestzulegen.
> ```
> manage-bde  tpm  takeownership 0wnerP@ss
> ```
> ## <a name="additional-references"></a>Weitere Verweise
> -   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> -   [manage-bde](manage-bde.md)
