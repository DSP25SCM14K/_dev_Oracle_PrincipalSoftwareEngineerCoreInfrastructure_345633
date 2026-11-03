# Oracle Principal Software Engineer, Core Infrastructure — role research

Research date: November 2, 2026. This research is a separate supporting document; it is not portfolio copy. Resume claims below are attributed to the supplied resume and have not been independently audited.

## Posting and role shape

The official Oracle posting is [Principal Software Engineer, Core Infrastructure, requisition 345633](https://careers.oracle.com/en/sites/jobsearch/job/345633). It lists Seattle, Washington and Santa Clara, California, and describes a regular individual-contributor position. The posting's experience band is 6–10+ years. The work centers on core infrastructure and distributed systems: high-throughput data paths, system performance, resilient services, operational readiness, in-service changes, and debugging production behavior across hardware and software boundaries.

The breadth of the posting points to a principal-level engineer who can reason across the packet or storage path and the service lifecycle around it. Relevant topics include multithreaded C/C++, Linux, kernel and driver behavior, firmware and hardware bring-up, Intel/AMD/ARM, network and storage I/O, DPU/SmartNIC offload, P4/DOCA, virtualization, and availability under faults. The post also stresses safe changes, observability, remediation, collaboration, and mentoring. The current site's diagrams are conceptual illustrations, not Oracle architecture or live telemetry.

## Oracle and OCI context

Oracle Cloud Infrastructure is Oracle's cloud platform. Oracle describes OCI networking in terms of high performance, low latency, security, and isolation; its networking pages discuss RDMA/RoCE and large-scale GPU networking. These are company product claims and technical context, not claims about the exact team or its internal implementation. [Oracle Cloud Networking](https://www.oracle.com/cloud/networking/)

Oracle's public HPC documentation describes cluster networking for tightly coupled workloads and RDMA. This makes east-west traffic, congestion, placement, and observability relevant concepts when reasoning about GPU workloads. It does not prove this opening is on a specific GPU product team. [OCI high-performance computing](https://docs.oracle.com/en-us/iaas/Content/Compute/References/high-performance-compute.htm)

Oracle's physical architecture documentation describes regions, availability domains, and fault domains. The security overview also describes isolation and layered security controls. These materials help ground discussions about blast radius, redundancy, failure domains, and safe operations in the public OCI model. [OCI physical architecture](https://docs.oracle.com/en-us/iaas/Content/GSG/Concepts/concepts-physical.htm) · [OCI security services](https://docs.oracle.com/en-us/iaas/Content/Security/Concepts/security_features.htm)

## Engineering implications — analysis, not Oracle interview guidance

- **Data path performance:** show how a packet or I/O request travels from NIC or device, through queueing and memory ownership, into policy and onward. Benchmark throughput alongside p99 latency, CPU cost, queue pressure, packet loss, and fallback behavior.
- **Offload boundaries:** a DPU can reduce host work, but correctness depends on policy placement, host/device ownership, telemetry, exception paths, and safe fallback. Explain what stays on host and what moves to the device.
- **Failure semantics:** availability depends on bounded retries, load shedding, rate limiting, replication state, health signals, and recoverable upgrades. Explain how a component behaves during a partition or brownout, not only when everything is healthy.
- **Hardware/software integration:** drivers, firmware, DMA, interrupts, NUMA locality, PCIe placement, and virtualization boundaries can determine end-to-end performance. Describe ownership and teardown as carefully as the fast path.
- **Operational quality:** dashboards, KPIs, fault injection, hardware-in-the-loop tests, health gates, rollback, and security remediation turn a fast design into a system that can be changed safely.

## Resume-to-role evidence

The attached resume reports 8+ years spanning core infrastructure, embedded Linux, data-plane networking, storage, firmware, and platform bring-up. Its experience bullets report:

- Sprouts AI: 3× packet throughput to 12 Mpps per core with C++/DPDK; 30% host CPU cores freed using BlueField/ConnectX, DOCA, SR-IOV, and vDPA; 20% higher GPU utilization after analyzing RDMA/RoCE and AllReduce behavior; 99.99% availability under dependency outages; 40% lower MTTR with telemetry, IaC/CI/CD, and zero-downtime upgrades.
- Resilience Inc: 2.5× NVMe I/O throughput and 40% lower p99 latency; 99.99% uptime with no customer maintenance windows; 20+ pre-production durability defects caught with fault injection; 40% lower host CPU involvement in packet forwarding with P4; 60% faster rollout through HIL automation and Terraform.
- Tata Steel: three ARM/Intel embedded Linux controller bring-ups; 90% less sensor data loss using kernel drivers; 45% better control-loop determinism; 35% fewer firmware field failures; 60% less manual test effort, with mentoring for five engineers.

These experiences connect directly to the posting's combination of accelerated data paths, Linux and device-level engineering, reliability, observability, safe rollouts, and technical leadership. The portfolio uses the resume's own quantified results, without extending them to broader claims.

## Project selection and link policy

Oxide-HV and Character Device Driver are featured because their supplied descriptions demonstrate hypervisor and kernel-driver work. All 23 supplied projects are listed with their source repositories. Technical Demo links appear only for the four projects for which the user supplied demo URLs: Oxide-HV, TradeSentinel, AskMyStore, and STRANGERS. EXPOS is listed once. The IEEE publication and certificate links are in the research section.

## Suggested preparation topics

These prompts are my analysis of the job and resume, not disclosed Oracle interview questions:

1. Trace a packet through the DPDK or P4 path and explain throughput, CPU, latency, and fallback measurements.
2. Describe DPU offload boundaries, control-plane updates, telemetry, and recovery when the device or link fails.
3. Explain DMA/buffer ownership, NUMA placement, polled queues, and p99 results in the NVMe work.
4. Walk through an in-service upgrade during partial failure: compatibility, traffic management, health gates, rollback, and SLO evidence.
5. Connect GPU AllReduce timing to RDMA/RoCE counters, packet loss, congestion controls, and utilization.
6. Explain how fault-injection and HIL tests exposed durability or firmware defects before release.
