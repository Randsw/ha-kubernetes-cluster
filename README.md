

To set single mode mode

inventrories/ml-k8s-single/group_vars/k8s_cluster.yml

enable_metallb: false
kubernetes_allow_pods_on_control_node: true

inventrories/ml-k8s-single/host_vars/control-node-1.yml
haproxy_server: false # if not HA config set it to false

execute

ansible-playbook -i inventories/ml-k8s-single/hosts-single.yml --ask-vault-pass deploy-cluster.yml -v