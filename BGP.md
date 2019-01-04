```
router bgp [AS]
 bgp router-id [LOOPBACK_IP]
 bgp log-neighbor-changes
 network [NETWORK]
 network [NETWORK] mask [MASK]
 network [NETWORK] mask [MASK]
 timers bgp 20 60
 neighbor [PEER_IP] remote-as [EXTERNAL_AS]
 neighbor [PEER_IP] description EBGP_TO_[PROVIDER_NAME]
 neighbor [PEER_IP] soft-reconfiguration inbound
 neighbor [PEER_IP] route-map RM_[NAME]_IN in
 neighbor [PEER_IP] route-map RM_[NAME]_OUT out
 neighbor [PEER_IP] remote-as [INTERNAL_AS]
 neighbor [PEER_IP] description iBGP to [DEVICE_NAME]
 neighbor [PEER_IP] next-hop-self
!
route-map RM_[NAME]_IN permit 10
 match ip address prefix-list PFX_DEFAULT_ROUTE
 set local-preference 150
!
 route-map RM_[NAME]_OUT permit 10
 match ip address prefix-list PFX_[PROVIDER_NAME]_OUT
 set as-path prepend 65200
!
ip prefix-list PFX_DEFAULT_ROUTE seq 10 permit 0.0.0.0/0
ip prefix-list PFX_[PROVIDER_NAME]_OUT seq 10 permit 159.52.0.0/16
```
