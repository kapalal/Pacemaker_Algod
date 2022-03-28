Pacemaker Configuration
-------------------------
Goal
- creare cluster via ansible
- creare ofc resource che gestitica servizi systemd e virtual ip del cluster
- creare configurazione Active-PAssive (in caso di standby del nodo1 virtual ip passa 
a nodo 2 e servizio viene spento su nodo 1 e attivato su nodo2 )

Link Utili

https://www.adminscout.net/en/os/Ubuntu/osv/20.04/conf/configuration-of-a-cluster-corosync-and-pacemaker-on-an-ubuntu-20-04-server/e1bfcf0dec05488e6be06e1701d489e5.html

http://www.linux-ha.org/doc/dev-guides/ra-dev-guide.html

https://ubuntu.com/server/docs/ubuntu-ha-pacemaker-resource-agents

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_high_availability_clusters/assembly_overview-of-high-availability-configuring-and-managing-high-availability-clusters#the_cluster_and_pacemaker_configuration_files

https://www.golinuxcloud.com/understanding-resource-group-constraints-cluster-examples/

Comandi installazione
 
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
