# Control-plane failover test

Goal: measure how long the Kubernetes API is unreachable when the
kube-vip leader is lost.

## How kube-vip elects a leader

kube-vip runs as a static pod on all three control-plane nodes. They
compete for the `plndr-cp-lock` Lease in `kube-system`. The holder adds
the VIP (192.168.102.250) to ens33 and announces it with gratuitous ARP.
Services use a separate lease, `plndr-svcs-lock`.

    kubectl -n kube-system get lease plndr-cp-lock \
      -o jsonpath='{.spec.holderIdentity}'

## Method

Monitor from a node that is not the leader:

    while true; do
      echo "$(date +%T) $(kubectl get --raw /healthz --request-timeout=2s 2>&1 | head -1)"
      sleep 1
    done | tee failover.log

Then reboot the leader (kube2).

## Result

    05:39:25 ok
    05:39:26 Unable to connect to the server: unexpected EOF
    05:39:28 Unable to connect to the server: context deadline exceeded
    05:39:31 ok

Downtime: ~5-6 seconds. The lease moved from kube2 to kube3, which
brought up the VIP. This matches kube-vip's default ~5s lease duration.

`unexpected EOF` is the open connection being cut as kube2 went down.
`context deadline exceeded` is the window where no node held the VIP.

## Notes

- Three control-plane nodes means etcd keeps quorum when one is lost.
  With two, losing one would take the API down until it returned.
- Tuning knobs: `vip_leaseduration`, `vip_renewdeadline`,
  `vip_retryperiod` in the kube-vip manifest.
