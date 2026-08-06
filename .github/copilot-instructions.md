## Copilot instructions for ONTAP AFX documentation

### Repository overview
Product: ONTAP AFX

*NetApp ONTAP AFX* is a disaggregated hardware/software storage system for high-performance *NAS* and *S3* workloads, including AI/ML pipelines.
It uses a customized *ONTAP personality* and focuses on independent compute/storage scaling, low-latency access, and simplified administration. The disaggregated architecture separates compute from storage, allowing each to scale independently.

### Repository structure
- `_include/` — Shared include assets used across AFX documentation pages.
- `administer/` — Cluster administration tasks such as monitoring, networking, authentication, SVM management, support, upgrade, and firmware updates.
- `get-started/` — Product overview, architecture, AFX vs AFF/FAS comparison, quick start, and pre-administration preparation.
- `install-setup/` — AFX 1K hardware install, cabling, switch setup, power-on, and cluster setup workflow.
- `install-afx-2k/` — AFX 2K hardware install, cabling, switch setup, and power-on workflow.
- `learn-more/` — Additional external and related reference resources.
- `manage-data/` — SVM-level data operations for volumes, buckets, and storage troubleshooting.
- `media/` — Images, diagrams, icons, and hardware cabling visuals referenced by docs.
- `protect-data/` — Data protection with consistency groups, snapshots, policies, and replication relationships.
- `redirect/` — Redirect pages mapping legacy topic paths to current AFX topics (no actual content).
- `release-notes/` — AFX release updates and changes to defaults/limits.
- `rest/` — REST API onboarding, first-call walkthrough, and API reference links.
- `secure-data/` — Data security topics including encryption at rest and IP connection security.
- `svm-admin/` — Navigation section for SVM/data admin tasks spanning manage-data, protect-data, secure-data, and additional admin.

### Product-specific context
**Architecture and components:**
- *Controller nodes* run a specialized ONTAP personality and serve client access over *NFS*, *SMB*, and *S3*.
- Storage shelves connect through *NVMe-oF* with *RoCE* and provide a redundant backend fabric with no single point of failure.
- Controllers and shelves are decoupled and connected by a redundant cluster storage switch network with VLAN-tagged paths.
- Clients access the cluster over a separate client network, while cluster-internal storage traffic uses the internal switched fabric.

**Key concepts:**
- *Storage Availability Zone (SAZ)* is the shared cluster-wide storage pool; all controller nodes can read/write across SAZ capacity.
- *FlexVolumes*, *FlexGroups*, and *S3 buckets* are the primary data containers exposed to administrators.
- The AFX tenant model is based on *SVMs* and supports multi-tenancy with simplified options for NAS/S3-focused environments.
- Volume movement inside SAZ is metadata-based using *Zero Copy Volume Move* (ZCVM) which supports non-disruptive balancing and HA behavior.

**Naming conventions and terminology:**
- Use *Unified ONTAP* to refer to the ONTAP personality used on AFF/FAS systems; AFX is a different ONTAP personality.
- Use *SAZ* for the shared storage pool and *SVM* for storage virtual machine.
- Hardware platform terms in this repo include *AFX 1K*, *AFX 2K*, and *NX224* shelves.
- AFX is optimized for NAS and object workflows; SAN-specific concepts (for example LUN/NVMe namespace administration) are treated as unsupported/restricted in the AFX-focused content.

### Typical user workflows
**Initial deployment and setup:** Review architecture and requirements → Install hardware and switches (AFX 1K or AFX 2K) → Cable and power on system → Complete ONTAP cluster setup in System Manager → Prepare cluster/SVM administration

**Provision and use data services:** Sign in to System Manager → Configure VLAN/network services for client protocols → Create and configure an SVM → Create data containers (volume or S3 bucket) → Manage volumes/buckets and monitor storage behavior

**Protect and replicate data:** Create cluster peer relationship → (Optional) create replication policy → Create consistency-group replication relationship → Manage snapshots and replication schedules

**API-based validation and automation entry:** Identify cluster management LIF and credentials → Run first REST API call to `/api/cluster` → Confirm ONTAP personality fields → Continue with REST API usage and reference topics
