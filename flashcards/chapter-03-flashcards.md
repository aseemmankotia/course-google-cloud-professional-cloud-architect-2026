## Chapter 3: Networking, Multi-Region HA & Disaster Recovery Design — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | VPC Peering: default max peering connections per VPC network? | 25 peering connections per VPC by default (increasable via quota request). Exam tip: peering is always non-transitive regardless of quota. |
| 2 | Dedicated Interconnect circuit speeds? | 10 Gbps or 100 Gbps per circuit; multiple circuits can be provisioned for more bandwidth/redundancy. Requires colocation at a Google supported facility. |
| 3 | Partner Interconnect bandwidth range? | 50 Mbps up to 50 Gbps. Used when you don't have equipment in a Google colocation facility — a partner extends the connection to Google. |
| 4 | Cloud VPN SLA: HA VPN vs Classic VPN? | HA VPN = 99.99% SLA (two interfaces, redundant peer gateway). Classic VPN = 99.9% SLA and is legacy/deprecated for new designs. |
| 5 | HA VPN per-tunnel throughput capacity? | Up to 3 Gbps per tunnel. Multiple tunnels can be used together for more aggregate bandwidth. |
| 6 | Shared VPC vs VPC Peering — when to use which? | Shared VPC: centralized admin, one team owns subnets/firewall rules, service projects attach. VPC Peering: decentralized, each VPC keeps its own admin, non-transitive, good for connecting independently-managed VPCs (e.g., across orgs). |
| 7 | Global external Application LB vs Regional external Application LB vs Internal Application LB | Global: single anycast IP, routes to nearest healthy region, works with Cloud CDN. Regional external: single-region, internet-facing L7. Internal: L7 routing but VIP only reachable inside the VPC/region. |
| 8 | Multi-region low-latency live streaming — reference architecture | Global external Application LB + Cloud CDN in front of regional backend services/MIGs in each target region, with health checks driving automatic regional failover. |
| 9 | Hybrid + multi-region DNS resolution pattern | Use Cloud DNS forwarding zones for on-prem-to-GCP resolution and Cloud DNS peering zones to let one VPC resolve private zones owned by another (e.g., Shared VPC host project). |
| 10 | gcloud command: enable a project as a Shared VPC host | `gcloud compute shared-vpc enable HOST_PROJECT_ID` then `gcloud compute shared-vpc associated-projects add SERVICE_PROJECT_ID --host-project=HOST_PROJECT_ID` |
| 11 | gcloud command: enable Private Google Access on a subnet | `gcloud compute networks subnets update SUBNET_NAME --region=REGION --enable-private-ip-google-access` |
| 12 | VPC Peering non-transitivity — one-sentence rule | If A peers with B and B peers with C, A CANNOT reach C through B. Each peering relationship must be established explicitly and directly. Exam trap: students assume peering behaves like transitive routing. |
