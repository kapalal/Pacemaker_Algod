Pacemaker Configuration
-------------------------

 
    apt install corosync pacemaker pcs
    systemctl enable pcsd
    systemctl start pcsd
    passwd hacluster
    pcs cluster auth
    vi /etc/hosts
    pcs cluster setup cluster corotest corotest2
    pcs host auth cluster corotest corotest2
    pcs cluster setup cluster corotest corotest2
    pcs host auth cluster corotest corotest2
    pcs cluster setup cluster corotest corotest2 --force
    pcs cluster enable --all
    pcs cluster start --all
    pcs property set stonith-enabled=false
    pcs property set no-quorum-policy=ignore
    crm status
    pcs resource create floating_ip ocf:heartbeat:IPaddr2 ip=192.168.56.12 cidr_netmask=24 op monitor interval=60s
    pcs resource create http_server ocf:heartbeat:nginx configfile="/etc/nginx/nginx.conf" op monitor timeout="20s" interval="60s"
    pcs status resources
    crm configure group cluster1 floating_ip http_server
    crm configure group cluster floating_ip http_server
    pcs status resources
    crm status
