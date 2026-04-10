##Modulo formativo ansible, podman, git

Obiettivo: automatizzare grazie ad ansible la creazione di tre container: haproxy, grafana, prometheus

Il container haproxy funge da FE (Proxy/LoadBalancer) per i due container di BE (grafana e prometheus)

Il progetto prevedere l'utilizzo di un ruolo sou_podman, nel quale sono definiti i template da utilizzare come file di configurazine di ogni container, e di task, dove risiede il file in cui sono specificate
le azioni che il comando 'ansible-playbook' andrà ad eseguire.  
