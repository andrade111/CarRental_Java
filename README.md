# 🚘 Car Rental System (Locadora de Veículos)

> **Sistema em Java para gestão e processamento de aluguel de veículos, projetado para demonstrar boas práticas de Orientação a Objetos, desacoplamento através de Interfaces e Injeção de Dependência.**

![Java](https://img.shields.io/badge/Java-11%2B-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Paradigma](https://img.shields.io/badge/Paradigma-POO%20%2F%20Interfaces-informational?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)

---

### 💡 Sobre o Projeto

O **CarRental_Java** é uma solução voltada para o cálculo e faturamento de aluguéis de veículos. A aplicação recebe as datas de retirada e retorno, calcula a duração da locação e aplica regras dinâmicas de tarifação (por hora ou por dia), emitindo a fatura final com os devidos impostos aplicados.

O principal diferencial técnico do projeto é o **desacoplamento da camada de serviço de impostos**, utilizando a interface `TaxService` para permitir que diferentes regras tributárias sejam injetadas sem alterar a regra de negócio principal (`RentalService`).

---

### 🛠️ Arquitetura & Fluxo de Processamento

```text
  ┌──────────────────┐
  │  Dados de Entrada│ (Veículo, Data Retirada, Data Retorno, Valor/Hora, Valor/Dia)
  └─────────┬────────┘
            │
            ▼
  ┌──────────────────┐      Interface      ┌──────────────────┐
  │  RentalService   ├────────────────────>│   TaxService     │
  └─────────┬────────┘      (Desacoplado)  └────────┬─────────┘
            │                                       │ (Implementação: BrazilTaxService)
            ▼                                       ▼
  ┌──────────────────┐                     ┌──────────────────┐
  │ Generates Invoice│<────────────────────┤ Cálculo Imposto  │
  └──────────────────┘                     └──────────────────┘
```

---

### ⚙️ Regras de Tarifação & Impostos

| Condição de Locação | Regra de Cobrança |
| :--- | :--- |
| **Até 12 Horas** | Cobrado por **hora exata** (arredondado para cima). Ex: 4h 10min = 5h cobradas. |
| **Acima de 12 Horas** | Cobrado por **diária completa**. Ex: 18h = 1 dia cobrado. |
| **Imposto (Brasil)** | • **20%** para pagamentos básicos até R$ 100,00.<br>• **15%** para pagamentos básicos acima de R$ 100,00. |

---

### 🧩 Padrões de Projeto & POO Aplicados

- 🔌 **Inversão de Controle & Injeção de Dependência:** O serviço `RentalService` não instancia diretamente o serviço de imposto. Em vez disso, recebe uma implementação de `TaxService` via construtor.
- 📦 **Composição de Objetos:** A classe `CarRental` é composta por um `Vehicle` e uma `Invoice` (quando gerada).
- 🗓️ **Manipulação de Datas:** Utilização da API moderna de datas do Java (`LocalDateTime` e `Duration`).

---

<details>
<summary>📁 <b>Clique para visualizar a estrutura de diretórios do repositório</b></summary>

```text
CarRental_Java/
├── src/
│   ├── application/
│   │   └── Program.java           # Ponto de entrada (Interação CLI)
│   └── model/
│       ├── entities/
│       │   ├── CarRental.java     # Modelo de dados da locação
│       │   ├── Invoice.java       # Fatura final (Pagamento Básico + Imposto)
│       │   └── Vehicle.java       # Modelo do veículo (Modelo/Placa)
│       └── services/
│           ├── TaxService.java       # Interface para o cálculo de imposto
│           ├── BrazilTaxService.java # Implementação concreta da regra fiscal
│           └── RentalService.java    # Orquestrador das regras de negócio
├── .gitignore
├── LICENSE                        # Licença MIT
└── README.md                      # Documentação do projeto
```

</details>

---

<details>
<summary>🚀 <b>Clique para ver como executar o projeto localmente</b></summary>

### 📌 Pré-requisitos
- **Java JDK 11** ou superior instalado.

### 🔧 Passos

1. **Clonar o repositório:**
   ```bash
   git clone [https://github.com/andrade111/CarRental_Java.git](https://github.com/andrade111/CarRental_Java.git)
   ```

2. **Acessar a pasta do projeto:**
   ```bash
   cd CarRental_Java
   ```

3. **Compilar o projeto:**
   ```bash
   javac -d bin src/application/Program.java src/model/entities/*.java src/model/services/*.java
   ```

4. **Executar a aplicação:**
   ```bash
   java -cp bin application.Program
   ```

</details>

---

<sub>Desenvolvido por **[Gabriel Andrade](https://github.com/andrade111)** • Licença MIT</sub>
