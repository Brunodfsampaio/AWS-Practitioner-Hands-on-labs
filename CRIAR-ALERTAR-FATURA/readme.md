# Criar Alertas de Forma Prática e Rápida - Evitando 'Surpresas' na AWS

## 1º Passo

Acesse a Console da AWS e procure por "Budgets":

![IMG1](https://github.com/user-attachments/assets/1429451f-3074-469a-be3f-8e5f85d90e2f)

---

## 2º Passo

Vai abrir a parte de "Orçamentos". No lado direito, clique na opção **Criar um Orçamento**:

![IMG2](https://github.com/user-attachments/assets/fa52d06d-12c4-41f1-af6d-d539bf0e77bc)

---

## 3º Passo

Esse passo é bastante autoexplicativo. Vai aparecer a opção **Padrão** já configurada. Quem for iniciante pode escolher, por exemplo, "Orçamento de gasto zero", onde caso ultrapasse os 0,01 dólares, você já será notificado. No caso do exemplo, vou escolher a opção **Personalizada (2º)**:

![IMG3](https://github.com/user-attachments/assets/d0ed8b31-08ea-4c1c-a33b-639aa503012f)

![IMG4](https://github.com/user-attachments/assets/b0f53b25-3afd-476f-9d5f-b29a29c9889c)

---

Na opção **Personalizada**, você poderá configurar o escopo do orçamento, seja para uso geral ou específico (criando filtros como, por exemplo, apenas uso de **EC2**, **S3**, **DynamoDB**, etc.). 

No caso, vou escolher a **primeira opção**.

Além disso, há a opção **"Agregar custos por"**, com as seguintes opções:

### Opções de Agregação:

1. **Custos Não Combinados**:
   - São os custos totais dos serviços que você está usando na AWS, sem nenhum tipo de agrupamento ou ajustes. Refletem os custos brutos, ou seja, sem deduções ou amortizações.

2. **Custos Amortizados**:
   - Quando você compra algo de forma antecipada ou sob contrato de longo prazo (por exemplo, instâncias reservadas), esses custos são distribuídos ao longo do tempo. A amortização refere-se a distribuir o custo ao longo de um período, em vez de reconhecê-lo de uma vez.

3. **Custos Combinados**:
   - A soma dos custos diretos e amortizados. Essa opção pode ser útil para ver o impacto total no seu orçamento, levando em consideração tanto os custos imediatos quanto os futuros.

4. **Custos Líquidos Não Combinados**:
   - Refere-se ao valor líquido dos custos não combinados, ou seja, após ajustes como descontos ou créditos. Esse é o custo "real" que você está pagando, sem agrupamentos ou amortizações.

5. **Custos Líquidos Amortizados**:
   - O custo líquido depois de descontos ou créditos, já amortizado ao longo do tempo.

### Resumão:

- **Não combinados**: custo bruto, sem ajustes.
- **Amortizados**: custo ajustado por longo prazo (parcelamento do pagamento).
- **Combinados**: soma de custos diretos e amortizados.
- **Líquidos não combinados**: custo bruto após descontos ou créditos.
- **Líquidos amortizados**: custo líquido, considerando ajustes e parcelamento.

---

## 4º Passo

Defina alertas personalizados antes de atingir 100% do valor estipulado:

![IMG6](https://github.com/user-attachments/assets/919bd0bf-1934-4ed3-8c70-40d925dd0b74)

![IMG7](https://github.com/user-attachments/assets/a905a255-1827-4fb8-aa44-d112a000d228)

![IMG8](https://github.com/user-attachments/assets/9220bb3b-4d1e-42d3-98aa-531526b3c903)

---

## 5º Passo

Revise tudo o que foi configurado e, depois, clique em **Criar Orçamento**:

![IMG9](https://github.com/user-attachments/assets/1a783c4c-978f-47d2-903d-c19c6ce2812d)

---

![IMG10](https://github.com/user-attachments/assets/0857bbda-01da-477b-b620-9aa6f0fcd46e)
