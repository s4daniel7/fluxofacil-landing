# 💸 Fluxo Fácil

**Plataforma SaaS de gestão financeira e controle de fluxo de caixa para pequenos negócios — simples, segura e pronta para escalar.**

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Backend-000000?style=flat&logo=flask&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?style=flat&logo=postgresql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Em%20Produção-success?style=flat)
![License](https://img.shields.io/badge/License-Privado-lightgrey?style=flat)

---

## 📌 Sobre o projeto

**Fluxo Fácil** é uma plataforma SaaS que centraliza a gestão financeira de pequenos negócios: entradas, saídas, vendas, estoque e visão consolidada do caixa em tempo real, em um único sistema.

### O problema

Grande parte dos pequenos empreendedores ainda controla as finanças do negócio em papel, planilhas soltas ou sistemas complexos demais para o dia a dia. Isso gera falta de visibilidade sobre o dinheiro real disponível, decisões tomadas às cegas e retrabalho constante de conciliação manual.

### A solução

O Fluxo Fácil resolve isso com uma interface simples e mobile-first, que qualquer dono de negócio consegue operar sem treinamento — registrando movimentações financeiras e estoque em segundos, com o dashboard atualizando indicadores automaticamente.

### Para quem foi criado

Pequenos negócios (comércio, prestação de serviço, food service) que precisam de controle financeiro real, sem a complexidade — ou o custo — de um ERP tradicional.

### Visão futura

Evoluir de ferramenta de controle financeiro para uma suíte SaaS completa de gestão para pequenos negócios, com sistema de planos, relatórios avançados e integrações de pagamento nativas (ver [Roadmap](#-roadmap)).

---

## 🎬 Demonstração

> 🔗 Link da aplicação em produção: *(adicionar aqui)*

<table>
<tr>
<td width="50%">

**Login**
<img src="screenshots/login.png" alt="Tela de login do Fluxo Fácil" width="100%">

</td>
<td width="50%">

**Painel de Controle**
<img src="screenshots/dashboard.png" alt="Dashboard com indicadores financeiros" width="100%">

</td>
</tr>
<tr>
<td width="50%">

**Entradas**
<img src="screenshots/entradas.png" alt="Tela de registro de entradas" width="100%">

</td>
<td width="50%">

**Saídas**
<img src="screenshots/saidas.png" alt="Tela de registro de saídas" width="100%">

</td>
</tr>
<tr>
<td width="50%">

**Despesas**
<img src="screenshots/despesas.png" alt="Tela de controle de despesas com contas a pagar" width="100%">

</td>
<td width="50%">

**Produtos / Estoque**
<img src="screenshots/produtos.png" alt="Tela de gestão de produtos e estoque" width="100%">

</td>
</tr>
<tr>
<td width="50%">

**Planos de Clientes**
<img src="screenshots/planos.png" alt="Tela de gestão de assinaturas e mensalidades" width="100%">

</td>
<td width="50%">

**Fechamento Mensal**
<img src="screenshots/relatoriomensal.png" alt="Relatório consolidado mensal" width="100%">

</td>
</tr>
</table>

---

## ⚙️ Principais funcionalidades

### 📊 Dashboard
- Visão financeira geral consolidada, com corte por unidade/filial
- Entradas, saídas e lucro do dia
- Insights automáticos sobre a saúde financeira do período (ex.: comparação de lucro com o dia anterior)
- Fechamento do dia com faturamento total e desempenho vs. média semanal
- Gráfico de faturamento diário ao longo do mês

### 💰 Gestão financeira
- Registro rápido de entradas e saídas, com atalhos configuráveis para lançamentos recorrentes
- Controle de vendas vinculado a produtos do estoque
- Despesas com vencimento, recorrência configurável e status de pagamento (contas a pagar)
- Múltiplos métodos de pagamento (dinheiro, Pix, etc.)
- Exportação de histórico para CSV
- Fechamento mensal consolidado, com histórico de entradas e saídas do período

### 📦 Estoque
- Cadastro de produtos com custo unitário e preço de venda
- Controle de quantidade em tempo real, por filial
- Baixa automática vinculada a vendas
- Busca rápida de produtos cadastrados

### 👥 Planos e assinaturas
- Cadastro de clientes com plano recorrente (mensalidade)
- Controle de ciclo de cobrança, próximo vencimento e último pagamento
- Ativação/desativação de plano por cliente

### 🔐 Segurança
- Proteção contra CSRF (Flask-WTF)
- Validação de dados de entrada
- Controle de acesso por empresa
- Isolamento de dados entre tenants (multi-tenancy)

### ⚡ Performance
- Otimização de queries SQL
- Correção de problemas N+1
- Paginação de resultados
- Índices estratégicos no banco de dados
- Cache para reduzir carga em consultas frequentes

### 📱 Experiência do usuário
- Interface responsiva, mobile-first
- PWA instalável, com Service Worker
- Feedback visual em ações do usuário
- Modais personalizados e melhorias de usabilidade

---

## 🏗️ Arquitetura do sistema

O Fluxo Fácil segue um padrão **MVC adaptado**, com organização modular por **Flask Blueprints** — cada domínio de negócio (autenticação, dashboard, financeiro, estoque) vive isolado em seu próprio módulo, com rotas, lógica e templates próprios.

A separação de responsabilidades é reforçada por um modelo de **multi-tenancy** baseado em `empresa_id` e `filial_id`: todas as consultas ao banco são filtradas por esses identificadores, garantindo isolamento de dados entre diferentes empresas e filiais na mesma instância da aplicação.

```
FluxoFacil/
│
├── app/
│   ├── auth/            # Autenticação e controle de acesso
│   ├── dashboard/        # Visão financeira consolidada
│   ├── financeiro/       # Entradas, saídas, vendas, despesas
│   ├── estoque/          # Produtos, quantidade, baixa automática
│   └── models/           # Modelos SQLAlchemy (empresa, filial, usuário, etc.)
│
├── templates/             # Views Jinja2
├── static/                 # CSS, JS, ícones, service worker (PWA)
├── migrations/             # Migrações de banco de dados
├── requirements.txt
└── run.py
```

> Estrutura de referência — reflete a organização real do projeto por Blueprints.

---

## 🛠️ Tecnologias utilizadas

| Camada | Tecnologias |
|---|---|
| **Backend** | Python, Flask, Flask Blueprints, SQLAlchemy ORM, Flask-WTF, Jinja2 |
| **Banco de dados** | PostgreSQL, Supabase |
| **Frontend** | HTML5, CSS3, JavaScript, design responsivo, mobile-first |
| **Infraestrutura** | Render, deploy automático via GitHub, PWA com Service Worker |
| **Segurança** | CSRF Protection, variáveis de ambiente, validação de dados |

---

## 🚀 Como executar localmente

```bash
# 1. Clone o repositório
git clone https://github.com/s4daniel7/fluxofacil.git
cd fluxofacil

# 2. Crie e ative um ambiente virtual
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Configure as variáveis de ambiente
cp .env.example .env
# edite o .env com suas credenciais (banco de dados, secret key, etc.)

# 5. Execute as migrações do banco
flask db upgrade

# 6. Inicie a aplicação
flask run
```

A aplicação estará disponível em `http://localhost:5000`.

---

## 🗄️ Banco de dados

O projeto utiliza **PostgreSQL**, hospedado via **Supabase**, com o schema versionado por migrações (Flask-Migrate/Alembic).

```bash
DATABASE_URL=postgresql://usuario:senha@host:porta/nome_do_banco
```

Todas as tabelas de domínio de negócio incluem `empresa_id` (e, quando aplicável, `filial_id`) como chave de particionamento lógico, garantindo que os dados de uma empresa nunca sejam expostos a outra dentro da mesma base.

---

## 🔒 Segurança

Segurança é tratada como requisito de produto, não item opcional:

- **CSRF Protection** ativa em todos os formulários via Flask-WTF
- **Validação de dados** de entrada em todas as rotas que recebem input do usuário
- **Isolamento multi-tenant** — toda query é escopada por `empresa_id`/`filial_id`, prevenindo vazamento de dados entre clientes
- **Variáveis de ambiente** para credenciais e chaves sensíveis, nunca versionadas no repositório
- **Controle de acesso** por empresa, restringindo o que cada usuário pode ver e alterar

---

## 🗺️ Roadmap

- [ ] Recuperação de senha
- [ ] Sistema de planos (freemium → pago)
- [ ] Dashboard avançado com mais indicadores
- [ ] Relatórios financeiros em PDF
- [ ] Emissão de NF-e / NFS-e
- [ ] Conciliação automática via PIX
- [ ] Aplicativo mobile nativo
- [ ] Integração com gateways de pagamento
- [ ] Camada de IA para insights financeiros

---

## 📚 Aprendizados técnicos

Este projeto foi construído — e continua evoluindo — como um exercício real de engenharia de software, não como tutorial. Ele demonstra, na prática:

- **Backend estruturado**: organização por Blueprints, separação clara de responsabilidades e modelagem de dados para um domínio financeiro real.
- **Arquitetura SaaS multi-tenant**: implementação de isolamento de dados entre clientes usando `empresa_id`/`filial_id`, um dos maiores desafios de qualquer produto B2B.
- **Banco de dados em produção**: modelagem relacional, migrações versionadas, otimização de queries (correção de N+1, índices, paginação).
- **Segurança aplicada**: proteção CSRF, validação de dados e gestão segura de variáveis de ambiente — não apenas em teoria, mas rodando com clientes reais.
- **Deploy e operação**: pipeline de deploy automático via GitHub para o Render, com banco gerenciado no Supabase.
- **Experiência do usuário**: interface mobile-first, PWA instalável e componentes de UI pensados para uso rápido em campo, não apenas em desktop.

---

## 👨‍💻 Autor

**Desenvolvido por Daniel Martins**

Estudante de Ciência da Computação — Universidade Católica de Brasília (UCB)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-s4daniel-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/s4daniel/)
[![GitHub](https://img.shields.io/badge/GitHub-s4daniel7-181717?style=flat&logo=github&logoColor=white)](https://github.com/s4daniel7)

*Portfólio: (adicionar link aqui)*

---

## 📄 Licença

Este projeto é privado/proprietário. *(ajuste esta seção caso decida abrir parte do código sob licença open source, como MIT.)*
