# homelab-infra

Kubernetes HA homelab on VMware vSphere. Manifests and notes used to build it.

## Cluster

| Component | Detail |
|---|---|
| Control plane | 3 nodes (kube1/2/3), stacked etcd |
| Workers | 1 |
| Kubernetes | kubeadm |
| CNI | Flannel |
| Control-plane LB | kube-vip (ARP), VIP 192.168.102.250 |
| Ingress | ingress-nginx 4.14.3 |
| Observability | kube-prometheus-stack 82.10.2, loki-stack 2.10.3 |
| UI | Headlamp 0.40.0 |

## Layout

- `cluster/` - kubeadm and kube-vip configuration
- `apps/` - Helm values for installed components
- `docs/` - operational notes and test results

## Notes

- [Control-plane failover test](docs/failover-test.md) - ~5s API downtime on leader loss
