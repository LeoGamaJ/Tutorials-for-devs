### Tutorial Completo: Instalando e Usando o Google Cloud SDK (CLI) no Ubuntu

#### O que é o Google Cloud SDK?

O Google Cloud SDK é um conjunto abrangente de ferramentas para gerenciamento de recursos e aplicações na Google Cloud Platform. A principal ferramenta do SDK é o `gcloud`, uma CLI poderosa que permite criar e gerenciar VMs, orquestrar clusters Kubernetes, gerenciar configurações de rede e muito mais.

#### Pré-requisitos
- Sistema Ubuntu (18.04 ou superior recomendado)
- Acesso de administrador para instalação de pacotes
- Conta Google e projeto no Google Cloud (você pode criar um gratuitamente [aqui](https://cloud.google.com/free))

---

### Passo 1: Configuração do Ambiente

#### Atualize o sistema e instale dependências

Primeiro, vamos garantir que o sistema esteja atualizado e que todas as dependências necessárias estejam instaladas:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install curl apt-transport-https ca-certificates gnupg -y
```

---

### Passo 2: Baixando e Instalando o Google Cloud SDK

#### Método A: Script de Instalação

1. **Baixar e iniciar o script de instalação**:

   Este método usa um script para instalar o SDK e é o mais rápido:
   ```bash
   curl https://sdk.cloud.google.com | bash
   ```

2. **Atualizar o terminal para reconhecer o SDK**:

   Após a instalação, execute este comando para atualizar sua sessão do shell:
   ```bash
   exec -l $SHELL
   ```

#### Método B: Repositório APT (Método Alternativo)

1. **Adicionar o repositório do Google Cloud SDK**:

   ```bash
   echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
   ```

2. **Importar a chave pública do Google Cloud**:

   ```bash
   curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
   ```

3. **Instalar o Google Cloud SDK**:

   ```bash
   sudo apt update
   sudo apt install google-cloud-sdk -y
   ```

---

### Passo 3: Inicialização e Autenticação

1. **Inicializar o SDK**:

   O comando `gcloud init` irá ajudá-lo a configurar sua conta:

   ```bash
   gcloud init
   ```

   - Siga as instruções para autenticar via navegador.
   - Selecione uma conta do Google.
   - Escolha um projeto para trabalhar (você pode criar um novo se necessário).

2. **Configurar versões padrão da API e zona/região**:

   Pense em definir suas configurações padrão para evitar especificá-las em cada comando:

   ```bash
   gcloud config set compute/zone us-central1-a
   gcloud config set compute/region us-central1
   ```

   Esses parâmetros acima são exemplos; selecione a zona e região mais adequadas ao seu projeto.

---

### Passo 4: Comandos Comuns do Google Cloud CLI

#### **Gerenciamento de Máquinas Virtuais (VMs)**

1. **Listar instâncias de VM**:

   ```bash
   gcloud compute instances list
   ```

2. **Criar uma nova VM**:

   ```bash
   gcloud compute instances create my-vm --zone=us-central1-a --machine-type=n1-standard-1 --image-family=debian-10 --image-project=debian-cloud
   ```

3. **Conectar-se a uma VM via SSH**:

   ```bash
   gcloud compute ssh my-vm
   ```

#### **Gerenciamento de Kubernetes com GKE**

1. **Listar clusters**:

   ```bash
   gcloud container clusters list
   ```

2. **Criar um cluster GKE**:

   ```bash
   gcloud container clusters create my-cluster --zone=us-central1-a
   ```

3. **Obter credenciais para um cluster GKE**:

   ```bash
   gcloud container clusters get-credentials my-cluster --zone=us-central1-a
   ```

---

### Passo 5: Configuração Avançada

#### Trabalhando com Configurações

- **Listar configurações ativas**:

   ```bash
   gcloud config list
   ```

- **Criar nova configuração**:

   ```bash
   gcloud config configurations create my-new-config
   gcloud config set project my-project-id
   ```

- **Ativar configuração**:

   ```bash
   gcloud config configurations activate my-new-config
   ```

#### Autenticação de Serviço

Se estiver automatizando processos, é útil usar contas de serviço:

1. **Criar uma conta de serviço**:

   ```bash
   gcloud iam service-accounts create my-service-account
   ```

2. **Conceder permissões à conta de serviço**:

   ```bash
   gcloud projects add-iam-policy-binding [PROJECT_ID] --member="serviceAccount:my-service-account@[PROJECT_ID].iam.gserviceaccount.com" --role="roles/editor"
   ```

3. **Gerar e baixar a chave JSON**:

   ```bash
   gcloud iam service-accounts keys create ~/key.json --iam-account=my-service-account@[PROJECT_ID].iam.gserviceaccount.com
   ```

4. **Autenticar usando a chave da conta de serviço**:

   ```bash
   gcloud auth activate-service-account --key-file=~/key.json
   ```

---

### Passo 6: Manutenção e Atualização

Para garantir que você tenha sempre a última versão com novos recursos e correções de bugs, atualize regularmente:

```bash
gcloud components update
```

---

### Conclusão

Agora você possui um tutorial completo para instalar, configurar e utilizar o Google Cloud SDK no Ubuntu. Com isso, você está pronto para explorar e gerenciar uma vasta gama de recursos da Google Cloud Platform. Para mais opções e ferramentas avançadas, consulte a [documentação oficial do Google Cloud SDK](https://cloud.google.com/sdk/docs).
