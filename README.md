# Modulo formativo ansible, podman, git

Obiettivo: automatizzare grazie ad ansible la creazione di tre container: haproxy, grafana, prometheus

Il container haproxy funge da FE (Proxy/LoadBalancer) per i due container di BE (grafana e prometheus)

Il progetto prevedere l'utilizzo di un ruolo sou_podman, nel quale sono definiti i template da utilizzare come file di configurazine di ogni container, e di task, dove risiede il file in cui sono specificate
le azioni che il comando 'ansible-playbook' andrà ad eseguire.

NOTA: allo stato attuale è tutto hardcoded

## Utilizzo del progetto

Per far partire ansible e permettergli di creare quanto scritto nei file si utilizza il comando

```bash
ansible-playbook -i inventory.ini playbook.yaml
```  

inventory.ini contiene l'indirizzo degli host sui quali verranno eseguiti i ruoli, il playbook.yml è invece il file che fa partire l'automazione

## Dove posso modificare i template?

```bash
roles/sou_podman/templates/
```

All'interno di questa cartella sono presenti i template dei file di configurazione (in formato j2) su cui è possibile apportare modifiche in caso lo si volesse 

## Dove posso modificare i task?

```bash
roles/sou_podman/tasks/
```

All'interno di questa cartella è presente il task (in formato yml) su cui è possibile apportare modifiche in caso lo si volesse per modificare le azioni che ansible compie una volta lanciato il comando.
In questo file sono definite le configurazioni dei container (porte, volumi, network)

## Esempio di un task per la creazione di un container

```yml
- name: install Haproxy
  containers.podman.podman_container:
    name: haproxy
    image: docker.io/library/haproxy:latest
    network: test_network
    state: started
    ports:
      - "1936:1936"
      - "8080:8080"
      - "8443:8443" 
      - "8404:8404"
    volumes:
      - "{{ playbook_dir }}/containers_vols/haproxy/haproxy.cfg:/usr/local/etc/haproxy/haproxy.cfg:Z"
      - "{{ playbook_dir }}/containers_vols/haproxy/cert/haproxy_cert.pem:/usr/local/etc/haproxy/certs/haproxy_cert.pem:Z"
```
