Para configurar cloud9 con ansible realiza lo siguiente

1. **Instala ansible en la terminal de cloud9 corriendo el siguiente comando**

```bash
sudo yum install ansible 
```


2. **Crear un playbook de Ansible:**
   Crear un archivo YAML con las tareas que deseas ejecutar. Por ejemplo, crea un archivo llamado `mi_playbook.yml` con el siguiente contenido:

   ```yaml
   ---
   - name: Mi Playbook Localhost
     hosts: localhost
     tasks:
       - name: Imprimir mensaje
         debug:
           msg: "¡Hola desde Ansible en localhost!"
   ```

2. **Ejecutar el playbook desde la consola de Cloud9:**
   Abre la consola en Cloud9 y navega al directorio donde guardaste tu playbook. Luego, ejecuta el siguiente comando:

   ```bash
   ansible-playbook mi_playbook.yml
   ```

   Asegúrate de tener Ansible instalado en tu entorno de Cloud9 y que esté configurado para ejecutarse en localhost.

3. **Verificar la salida:**
   Después de ejecutar el playbook, verás la salida en la consola. Deberías ver un mensaje como el siguiente:

   ```bash
   PLAY [Mi Playbook Localhost] **************************************************

   TASK [Gathering Facts] *********************************************************
   ok: [localhost]

   TASK [Imprimir mensaje] ********************************************************
   ok: [localhost] => (item=None) =>
     msg: ¡Hola desde Ansible en localhost!

   PLAY RECAP *********************************************************************
   localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
   ```

   Esto indica que el playbook se ejecutó correctamente, y el mensaje se imprimió en la consola.

4. **Modifica el playbook con el contenido del Archivo AnsibleExample**

```yaml
---
- name: Install Amazon Corretto and Docker
  hosts: your_amazon_linux_server
  become: true  # Run tasks as sudo

  tasks:
    - name: Update package cache
      yum:
        name: '*'
        state: latest

    - name: Install Amazon Corretto 11
      yum:
        name: java-11-amazon-corretto-devel
        state: present

    - name: Add Docker Yum repository
      yum_repository:
        name: docker-ce-stable
        description: Docker CE Stable - $basearch
        baseurl: https://download.docker.com/linux/centos/7/$basearch/stable
        gpgkey: https://download.docker.com/linux/centos/gpg
        enabled: yes

    - name: Install Docker
      yum:
        name:
          - docker-ce
          - docker-ce-cli
          - containerd.io
        state: present

    - name: Start and enable Docker service
      systemd:
        name: docker
        enabled: yes
        state: started
```
5. **Ejecutar el playbook desde la consola de Cloud9:**
   Abre la consola en Cloud9 y navega al directorio donde guardaste tu playbook. Luego, ejecuta el siguiente comando:

   ```bash
   ansible-playbook mi_playbook.yml
   ```