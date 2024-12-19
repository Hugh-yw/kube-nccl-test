# k8s in NCCL Test
此项目主要介绍如何便捷验证GPU服务器的NCCL性能，节省了依赖安装、编译、配置端口、免密等繁琐步骤。

NCCL（Nvidia Collective multi-GPU Communication Library，读作 "Nickel"）是一个提供GPU间通信基元的库，它具有拓扑感知能力，可以轻松集成到应用程序中。NCCL做了很多优化，以在PCIe、Nvlink、InfiniBand上实现较高的通信速度。NCCL支持安装在单个节点或多个节点上的大量GPU卡上，并可用于单进程或多进程（如MPI）应用。

# Test
```bash
kubectl logs -f nccl-tests-h100-launcher 
Defaulted container "nccl" out of: nccl, kubectl-delivery (init)
+ POD_NAME=nccl-tests-h100-worker-1
+ shift
+ /opt/kube/kubectl exec nccl-tests-h100-worker-1 -- /bin/sh -c    OPAL_PREFIX=/opt/hpcx/ompi ; export OPAL_PREFIX;    PATH=/opt/hpcx/ompi/bin:$PATH ; export PATH ; LD_LIBRARY_PATH=/opt/hpcx/ompi/lib:${LD_LIBRARY_PATH:-} ; export LD_LIBRARY_PATH ; DYLD_LIBRARY_PATH=/opt/hpcx/ompi/lib:${DYLD_LIBRARY_PATH:-} ; export DYLD_LIBRARY_PATH ;   /opt/hpcx/ompi/bin/orted -mca ess "env" -mca ess_base_jobid "3064987648" -mca ess_base_vpid 2 -mca ess_base_num_procs "3" -mca orte_node_regex "nccl-tests-h[3:100]-launcher,nccl-tests-h[3:100]-worker-0,nccl-tests-h[3:100]-worker-1@0(3)" -mca orte_hnp_uri "3064987648.0;tcp://10.233.86.109:57373" -mca plm "rsh" --tree-spawn -mca routed "radix" -mca orte_parent_uri "3064987648.0;tcp://10.233.86.109:57373" -mca orte_default_hostfile "/etc/mpi/hostfile" -mca plm_rsh_agent "/etc/mpi/kubexec.sh" -mca hwloc_base_binding_policy "none" -mca pmix "^s1,s2,cray,isolated"
+ POD_NAME=nccl-tests-h100-worker-0
+ shift
+ /opt/kube/kubectl exec nccl-tests-h100-worker-0 -- /bin/sh -c    OPAL_PREFIX=/opt/hpcx/ompi ; export OPAL_PREFIX;    PATH=/opt/hpcx/ompi/bin:$PATH ; export PATH ; LD_LIBRARY_PATH=/opt/hpcx/ompi/lib:${LD_LIBRARY_PATH:-} ; export LD_LIBRARY_PATH ; DYLD_LIBRARY_PATH=/opt/hpcx/ompi/lib:${DYLD_LIBRARY_PATH:-} ; export DYLD_LIBRARY_PATH ;   /opt/hpcx/ompi/bin/orted -mca ess "env" -mca ess_base_jobid "3064987648" -mca ess_base_vpid 1 -mca ess_base_num_procs "3" -mca orte_node_regex "nccl-tests-h[3:100]-launcher,nccl-tests-h[3:100]-worker-0,nccl-tests-h[3:100]-worker-1@0(3)" -mca orte_hnp_uri "3064987648.0;tcp://10.233.86.109:57373" -mca plm "rsh" --tree-spawn -mca routed "radix" -mca orte_parent_uri "3064987648.0;tcp://10.233.86.109:57373" -mca orte_default_hostfile "/etc/mpi/hostfile" -mca plm_rsh_agent "/etc/mpi/kubexec.sh" -mca hwloc_base_binding_policy "none" -mca pmix "^s1,s2,cray,isolated"
# nThread 1 nGpus 1 minBytes 536870912 maxBytes 8589934592 step: 2(factor) warmup iters: 5 iters: 20 agg iters: 1 validation: 1 graph: 0
#
# Using devices
#  Rank  0 Group  0 Pid     16 on nccl-tests-h100-worker-0 device  0 [0x19] NVIDIA H100 80GB HBM3
#  Rank  1 Group  0 Pid     17 on nccl-tests-h100-worker-0 device  1 [0x3a] NVIDIA H100 80GB HBM3
#  Rank  2 Group  0 Pid     18 on nccl-tests-h100-worker-0 device  2 [0x4c] NVIDIA H100 80GB HBM3
#  Rank  3 Group  0 Pid     19 on nccl-tests-h100-worker-0 device  3 [0x5c] NVIDIA H100 80GB HBM3
#  Rank  4 Group  0 Pid     20 on nccl-tests-h100-worker-0 device  4 [0x9a] NVIDIA H100 80GB HBM3
#  Rank  5 Group  0 Pid     21 on nccl-tests-h100-worker-0 device  5 [0xba] NVIDIA H100 80GB HBM3
#  Rank  6 Group  0 Pid     22 on nccl-tests-h100-worker-0 device  6 [0xca] NVIDIA H100 80GB HBM3
#  Rank  7 Group  0 Pid     23 on nccl-tests-h100-worker-0 device  7 [0xda] NVIDIA H100 80GB HBM3
#  Rank  8 Group  0 Pid     16 on nccl-tests-h100-worker-1 device  0 [0x19] NVIDIA H100 80GB HBM3
#  Rank  9 Group  0 Pid     17 on nccl-tests-h100-worker-1 device  1 [0x3a] NVIDIA H100 80GB HBM3
#  Rank 10 Group  0 Pid     18 on nccl-tests-h100-worker-1 device  2 [0x4c] NVIDIA H100 80GB HBM3
#  Rank 11 Group  0 Pid     19 on nccl-tests-h100-worker-1 device  3 [0x5c] NVIDIA H100 80GB HBM3
#  Rank 12 Group  0 Pid     20 on nccl-tests-h100-worker-1 device  4 [0x9a] NVIDIA H100 80GB HBM3
#  Rank 13 Group  0 Pid     21 on nccl-tests-h100-worker-1 device  5 [0xba] NVIDIA H100 80GB HBM3
#  Rank 14 Group  0 Pid     22 on nccl-tests-h100-worker-1 device  6 [0xca] NVIDIA H100 80GB HBM3
#  Rank 15 Group  0 Pid     23 on nccl-tests-h100-worker-1 device  7 [0xda] NVIDIA H100 80GB HBM3
#
#                                                              out-of-place                       in-place          
#       size         count      type   redop    root     time   algbw   busbw #wrong     time   algbw   busbw #wrong
#        (B)    (elements)                               (us)  (GB/s)  (GB/s)            (us)  (GB/s)  (GB/s)       
   536870912     134217728     float     sum      -1   5202.3  103.20  193.50      0   5377.7   99.83  187.19      0
  1073741824     268435456     float     sum      -1    10314  104.11  195.20      0    10339  103.85  194.73      0
  2147483648     536870912     float     sum      -1    20565  104.42  195.79      0    20583  104.33  195.62      0
  4294967296    1073741824     float     sum      -1    41198  104.25  195.47      0    41040  104.65  196.22      0
  8589934592    2147483648     float     sum      -1    81958  104.81  196.52      0    81960  104.81  196.51      0
# Out of bounds values : 0 OK
# Avg bus bandwidth    : 194.675 
#
```
