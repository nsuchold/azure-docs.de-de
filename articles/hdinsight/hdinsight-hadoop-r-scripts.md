---
title: Verwenden von R in HDInsight zum Anpassen von Clustern | Microsoft Docs
description: Erfahren Sie, wie Sie R mit Skriptaktionen installieren und wie Sie R in HDInsight-Clustern verwenden.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: jgao
translationtype: Human Translation
ms.sourcegitcommit: 0587dfcd6079fc8df91bad5a5f902391d3657a6b
ms.openlocfilehash: 8b74f2e4169ac97e09da12d5ed85e0e24b50e150
ms.lasthandoff: 12/08/2016


---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Installieren und Verwenden von R in HDInsight Hadoop-Clustern
Erfahren Sie, wie Sie mithilfe von Skriptaktionen Windows-basierte HDInsight-Cluster mit R anpassen und wie Sie R in HDInsight-Clustern verwenden. Beim [HDInsight-Angebot](https://azure.microsoft.com/pricing/details/hdinsight/) ist R Server Teil Ihres HDInsight-Clusters. Dadurch können R-Skripts MapReduce und Spark verwenden, um verteilte Berechnungen auszuführen. Weitere Informationen finden Sie unter [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md)(Erste Schritte mit R Server in HDInsight). Informationen zur Verwendung von R mit einem Linux-basierten Cluster finden Sie unter [Installieren und Verwenden von R in HDinsight Hadoop-Clustern (Linux)](hdinsight-hadoop-r-scripts-linux.md).

Mithilfe von *Skriptaktionen*können Sie R in einem beliebigen Clustertyp (Hadoop, Storm, HBase, Spark) in Azure HDInsight installieren. Ein Beispielskript zum Installieren von R in einem HDInsight-Cluster steht in einem schreibgeschützten Azure Storage-BLOB unter [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)zur Verfügung.

**Verwandte Artikel**

* [Installieren und Verwenden von R in HDInsight Hadoop-Clustern (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Erstellen von Hadoop-Clustern in HDInsight](hdinsight-provision-clusters.md): Allgemeine Informationen zum Erstellen von HDInsight-Clustern
* [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen][hdinsight-cluster-customize]: Allgemeine Informationen zum Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen
* [Entwickeln von Script Action-Skripts für HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Was ist R?
Das <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> ist eine Open-Source-Sprache und -Umgebung für statistische Berechnungen. R bietet Hunderte integrierter Statistikfunktionen und eine eigene Programmiersprache, die Aspekte der funktionalen und objektorientierten Programmierung kombiniert. Darüber hinaus werden umfangreiche Grafikfunktionen geboten. R ist in einer Vielzahl von Feldern für die meisten professionellen Statistiker und Analysten die bevorzugte Programmierungsumgebung.

R ist mit Azure-BLOB-Speicher (WASB) kompatibel, weshalb darin gespeicherte Daten mit R in HDInsight verarbeitet werden können.  

## <a name="install-r"></a>Installieren von R
Ein [Beispielskript](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) zum Installieren von R in einem HDInsight-Cluster steht in einem schreibgeschützten BLOB in Azure Storage zur Verfügung. Dieser Abschnitt enthält Anweisungen zum Verwenden des Beispielskripts während der Erstellung des Clusters mithilfe des Azure-Portals.

> [!NOTE]
> Das Beispielskript funktioniert nur mit HDInsight-Clustern der Version 3.1. Weitere Informationen zu HDInsight-Clusterversionen finden Sie unter [HDInsight-Clusterversionen](hdinsight-component-versioning.md).
>
>

1. Wenn Sie einen HDInsight-Cluster im Portal erstellen, klicken Sie auf **Optionale Konfiguration** und anschließend auf **Skriptaktionen**.
2. Geben Sie auf der Seite **Skriptaktionen** die folgenden Werte ein:

    ![Anpassen eines Clusters mithilfe einer Skriptaktion](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Anpassen eines Clusters mithilfe einer Skriptaktion")

    <table border='1'>
        <tr><th>Eigenschaft</th><th>Wert</th></tr>
        <tr><td>Name</td>
            <td>Geben Sie einen Namen für die Skriptaktion an, z.B. <b>R installieren</b>.</td></tr>
        <tr><td>Skript-URI</td>
            <td>Geben Sie den URI des Skripts, das aufgerufen wird, um den Cluster anzupassen. Beispiel: <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Knotentyp</td>
            <td>Gibt die Knoten an, auf denen das Anpassungsskript ausgeführt wird. Sie können <b>Alle Knoten</b>, <b>Nur Hauptknoten</b> oder <b>Nur Workerknoten</b> auswählen.
        <tr><td>Parameter</td>
            <td>Geben Sie die Parameter an, sofern dies für das Skript erforderlich ist. Für das Skript zum Installieren von R sind keine Parameter erforderlich, sodass Sie dieses Feld leer lassen können.</td></tr>
    </table>

    Sie können dem Cluster mehr als eine Skriptaktion zum Installieren von mehreren Komponenten hinzufügen. Nachdem Sie die Skripts hinzugefügt haben, klicken Sie auf das Häkchen, um mit dem Erstellen des Clusters zu beginnen.

Sie können das Skript auch zum Installieren von R in HDInsight mit Azure PowerShell oder dem HDInsight .NET SDK verwenden. Anweisungen zu diesen Verfahren finden Sie nachfolgend in diesem Artikel.

## <a name="run-r-scripts"></a>Ausführen von R-Skripts
In diesem Abschnitt wird beschrieben, wie ein R-Skript in einem Hadoop-Cluster mit HDInsight ausgeführt wird.

1. **Richten Sie eine Remotedesktopverbindung mit dem Cluster ein**: Aktivieren Sie im Azure-Portal Remotedesktop für den Cluster, den Sie mit installiertem R erstellt haben, und stellen Sie dann eine Remoteverbindung mit dem Cluster her. Anweisungen hierzu finden Sie unter [Herstellen einer Verbindung mit HDInsight-Clustern mit RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Öffnen der R-Konsole**: Nach der Installation von R befindet sich eine Verknüpfung mit der R-Konsole auf dem Desktop des Hauptknotens. Klicken Sie darauf, um die R-Konsole zu öffnen.
3. **Ausführen des R-Skripts**: Das R-Skript kann direkt über die R-Konsole ausgeführt werden, indem es darin eingefügt, ausgewählt und die EINGABETASTE gedrückt wird. Hier ist ein einfaches Beispielskript, das die Zahlen von 1 bis 100 generiert und diese anschließend mit 2 multipliziert.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Die ersten beiden Zeilen rufen die mit R installierten RHadoop-Bibliotheken auf. Die letzte Zeile gibt die Ergebnisse in der Konsole aus. Die Ausgabe sollte wie folgt aussehen:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Installieren von R mit Azure PowerShell
Weitere Informationen finden Sie unter [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Das Beispiel veranschaulicht das Installieren von Spark mithilfe von Azure PowerShell. Sie müssen das Skript für die Verwendung von [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)anpassen.

## <a name="install-r-using-net-sdk"></a>Installieren von R mit dem .NET SDK
Weitere Informationen finden Sie unter [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Das Beispiel veranschaulicht das Installieren von Spark mithilfe des .NET SDK. Sie müssen das Skript für die Verwendung von [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)anpassen.

## <a name="see-also"></a>Siehe auch
* [Installieren und Verwenden von R in HDInsight Hadoop-Clustern (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Erstellen von Hadoop-Clustern in HDInsight](hdinsight-provision-clusters.md): Allgemeine Informationen zum Erstellen von HDInsight-Clustern
* [Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen][hdinsight-cluster-customize]: Allgemeine Informationen zum Anpassen von HDInsight-Clustern mithilfe von Skriptaktionen
* [Entwickeln von Script Action-Skripts für HDInsight](hdinsight-hadoop-script-actions.md)
* [Installieren und Verwenden von Spark in HDInsight-Clustern][hdinsight-install-spark]: Skriptaktionsbeispiel zum Installieren von Spark
* [Installieren von Giraph in HDInsight-Clustern](hdinsight-hadoop-giraph-install.md): Skriptaktionsbeispiel zum Installieren von Giraph
* [Installieren von Solr in HDInsight-Clustern](hdinsight-hadoop-solr-install-linux.md): Skriptaktionsbeispiel zum Installieren von Solr

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md

