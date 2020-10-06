== [[BlockManagerSource]] BlockManagerSource -- Metrics Source for BlockManager

`BlockManagerSource` is the link:spark-metrics-Source.adoc[metrics source] of a xref:storage:BlockManager.adoc[BlockManager].

[[sourceName]]
`BlockManagerSource` is registered under the name *BlockManager* (when `SparkContext` is link:spark-SparkContext-creating-instance-internals.adoc#registerSource[created]).

[[metrics]]
.BlockManagerSource's Gauge Metrics (in alphabetical order)
[width="100%",cols="1,1,2",options="header"]
|===
| Name
| Type
| Description

| `disk.diskSpaceUsed_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their disk space used (`diskUsed`).

| `memory.maxMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their maximum memory limit (`maxMem`).

| `memory.maxOffHeapMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their off-heap memory remaining (`maxOffHeapMem`).

| `memory.maxOnHeapMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their on-heap memory remaining (`maxOnHeapMem`).

| `memory.memUsed_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their memory used (`memUsed`).

| `memory.offHeapMemUsed_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their off-heap memory used (`offHeapMemUsed`).

| `memory.onHeapMemUsed_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their on-heap memory used (`onHeapMemUsed`).

| `memory.remainingMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their memory remaining (`memRemaining`).

| `memory.remainingOffHeapMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their off-heap memory remaining (`offHeapMemRemaining`).

| `memory.remainingOnHeapMem_MB`
| long
| Requests `BlockManagerMaster` for xref:BlockManagerMaster.adoc#getStorageStatus[storage status] (for every xref:storage:BlockManager.adoc[BlockManager]) and sums up their on-heap memory remaining (`onHeapMemRemaining`).
|===

You can access the `BlockManagerSource` <<metrics, metrics>> using the web UI's port (as link:spark-webui-properties.adoc#spark.ui.port[spark.ui.port] configuration property).

```
$ http --follow http://localhost:4040/metrics/json \
    | jq '.gauges | keys | .[] | select(test(".driver.BlockManager"; "g"))'
"local-1528725411625.driver.BlockManager.disk.diskSpaceUsed_MB"
"local-1528725411625.driver.BlockManager.memory.maxMem_MB"
"local-1528725411625.driver.BlockManager.memory.maxOffHeapMem_MB"
"local-1528725411625.driver.BlockManager.memory.maxOnHeapMem_MB"
"local-1528725411625.driver.BlockManager.memory.memUsed_MB"
"local-1528725411625.driver.BlockManager.memory.offHeapMemUsed_MB"
"local-1528725411625.driver.BlockManager.memory.onHeapMemUsed_MB"
"local-1528725411625.driver.BlockManager.memory.remainingMem_MB"
"local-1528725411625.driver.BlockManager.memory.remainingOffHeapMem_MB"
"local-1528725411625.driver.BlockManager.memory.remainingOnHeapMem_MB"
```

[[creating-instance]]
[[blockManager]]
`BlockManagerSource` takes a xref:storage:BlockManager.adoc[BlockManager] when created.

`BlockManagerSource` is <<creating-instance, created>> when `SparkContext` is link:spark-SparkContext-creating-instance-internals.adoc#registerSource[created].