# 🧱 Bootstrap Kubernetes – Cluster Setup Inicial

Este repositório configura os recursos essenciais de **bootstrap** no cluster Kubernetes utilizado pelo sistema de autoatendimento da lanchonete (Tech Challenge – Fase 4 – FIAP). Ele prepara o cluster com componentes fundamentais como **Ingress Controller**, **segredos externos da AWS** e integração com **GitHub Actions** para deploys automatizados.

## 📦 Visão Geral

O bootstrap deste cluster é necessário **antes do deploy da infraestrutura de microsserviços**, pois ele provisiona:

- 🎛️ Ingress Controller (NGINX)
- 🔐 External Secrets (via AWS Secrets Manager)
- 🤖 Integração com GitHub Actions (via `aws-creds-secret.yaml`)
- 🗂️ ClusterSecretStore para sincronização segura de segredos
- ⚙️ Workflows de automação (`.github/workflows/*.yml`)

> Este projeto é complementar ao repositório:
> - [TC4-terraform-infra-k8s-microservices](https://github.com/limalucas99/TC4-terraform-infra-k8s-microservices)

---

## 🛠️ Tecnologias Utilizadas

- Kubernetes (EKS)
- Helm (opcional)
- External Secrets Operator
- AWS Secrets Manager
- GitHub Actions
- Ingress NGINX

---

## 🧩 Pré-requisitos

- Cluster Kubernetes já provisionado (ex: via Terraform)
- `kubectl` instalado e configurado para o cluster
- Acesso a um repositório GitHub com permissões de CI/CD
- Permissões de acesso à AWS (EKS + Secrets Manager)

---

## 🚀 Como Utilizar

### 1. Aplicar Ingress Controller

```bash
kubectl apply -f ingress/ingress.yml
```

### 2. Criar Segredos de Acesso à AWS

```bash
kubectl apply -f templates/aws-creds-secret.yaml
```

Esse recurso é consumido pelos workflows GitHub Actions para autenticação na AWS.

### 3. Configurar External Secrets Operator

```bash
kubectl apply -f external-secrets/cluster-secret-store.yaml
```

Esse recurso conecta o cluster ao AWS Secrets Manager para disponibilizar segredos como variáveis em pods.

---

## ⚙️ Workflows Automatizados

Os workflows `.github/workflows/*.yml` realizam:

- Deploy contínuo de segredos
- Validação da configuração do cluster
- Atualização automática dos componentes de bootstrap

> Esses pipelines são ativados com push na `main` ou por meio de PRs.

---

## 📄 Licença

Projeto acadêmico para fins educacionais na pós-graduação em Software Architecture da FIAP.
