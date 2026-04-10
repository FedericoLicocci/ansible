# Modulo formativo ansible, podman, git

Obiettivo: automatizzare grazie ad ansible la creazione di tre container: haproxy, grafana, prometheus

Il container haproxy funge da FE (Proxy/LoadBalancer) per i due container di BE (grafana e prometheus)

Il progetto prevedere l'utilizzo di un ruolo sou_podman, nel quale sono definiti i template da utilizzare come file di configurazine di ogni container, e di task, dove risiede il file in cui sono specificate
le azioni che il comando 'ansible-playbook' andrà ad eseguire.

NOTA: allo stato attuale è tutto hardcoded

# Utilizzo del progetto

Per far partire ansible e permettergli di creare quanto scritto nei file si utilizza il comando

'''
ansible-playbook -i inventory.ini playbook.yaml
'''  

inventory.ini contiene l'indirizzo degli host sui quali verranno eseguiti i ruoli, il playbook.yml è invece il file che fa partire l'automazione
