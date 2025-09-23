# Mini Projeto de Análise de Dados - E-commerce Olist

## 📊 Visão Geral do Projeto

Este projeto consiste na análise exploratória e insights de um dataset real de e-commerce brasileiro da Olist, uma das maiores plataformas de marketplace do Brasil. O dataset contém informações sobre pedidos, clientes, produtos, vendedores e avaliações, oferecendo uma oportunidade única de realizar análises de negócio e comportamento do consumidor.

## 🎯 Objetivos do Projeto

### Objetivos Principais:
- **Análise de Performance de Vendas**: Identificar tendências de vendas, sazonalidade e padrões de compra
- **Análise de Satisfação do Cliente**: Avaliar reviews e identificar fatores que impactam a satisfação
- **Análise Geográfica**: Mapear distribuição de vendas e identificar mercados-chave
- **Análise de Produtos**: Identificar categorias mais vendidas e oportunidades de crescimento
- **Análise de Vendedores**: Avaliar performance dos vendedores e identificar top performers

### Objetivos de Negócio:
- Identificar oportunidades de crescimento
- Otimizar estratégias de marketing
- Melhorar experiência do cliente
- Aumentar retenção e lifetime value

## 📁 Estrutura do Dataset

O dataset é composto por **9 arquivos CSV** interconectados:

### 1. **olist_orders_dataset.csv** (99.442 registros)
- **Chave**: `order_id`
- **Campos**: ID do pedido, status, timestamps de compra, aprovação, entrega
- **Período**: 2016-2018
- **Status possíveis**: delivered, shipped, canceled, invoiced, processing, unavailable

### 2. **olist_customers_dataset.csv** (99.442 registros)
- **Chave**: `customer_id`
- **Campos**: ID único do cliente, localização (CEP, cidade, estado)
- **Cobertura**: Todo o território brasileiro

### 3. **olist_products_dataset.csv** (32.952 registros)
- **Chave**: `product_id`
- **Campos**: Categoria, nome, dimensões, peso, quantidade de fotos
- **Categorias**: 73 categorias diferentes (perfumaria, eletrônicos, casa, etc.)

### 4. **olist_order_items_dataset.csv** (112.651 registros)
- **Chave**: `order_id` + `product_id`
- **Campos**: Itens por pedido, preço, frete, vendedor
- **Relaciona**: Pedidos com produtos e vendedores

### 5. **olist_order_payments_dataset.csv** (103.887 registros)
- **Chave**: `order_id`
- **Campos**: Método de pagamento, parcelas, valor
- **Métodos**: credit_card, boleto, voucher, debit_card

### 6. **olist_order_reviews_dataset.csv** (104.165 registros)
- **Chave**: `review_id`
- **Campos**: Avaliações (1-5 estrelas), comentários, timestamps
- **Período**: 2016-2018

### 7. **olist_sellers_dataset.csv** (3.096 registros)
- **Chave**: `seller_id`
- **Campos**: Localização dos vendedores (CEP, cidade, estado)
- **Cobertura**: Vendedores de todo o Brasil

### 8. **olist_geolocation_dataset.csv** (1.000.164 registros)
- **Chave**: `geolocation_zip_code_prefix`
- **Campos**: Coordenadas geográficas (lat/lng) por CEP
- **Uso**: Análises de geolocalização e mapas

### 9. **product_category_name_translation.csv** (72 registros)
- **Chave**: `product_category_name`
- **Campos**: Tradução das categorias para inglês
- **Uso**: Padronização e internacionalização

## 🔍 Análises Propostas

### 1. **Análise Temporal**
- Evolução das vendas ao longo do tempo
- Sazonalidade e padrões mensais/sazonais
- Análise de tendências de crescimento
- Correlação entre eventos e vendas

### 2. **Análise de Performance de Vendas**
- Receita total e ticket médio
- Análise por categoria de produto
- Top produtos e categorias
- Análise de conversão e abandono

### 3. **Análise Geográfica**
- Distribuição de vendas por região/estado
- Análise de densidade de clientes
- Identificação de mercados emergentes
- Correlação geográfica com performance

### 4. **Análise de Satisfação do Cliente**
- Distribuição de avaliações
- Correlação entre tempo de entrega e satisfação
- Análise de comentários (NLP)
- Identificação de problemas recorrentes

### 5. **Análise de Vendedores**
- Performance por vendedor
- Análise de concentração de vendas
- Identificação de vendedores-chave
- Análise de churn de vendedores

### 6. **Análise de Pagamentos**
- Preferências de método de pagamento
- Análise de parcelamento
- Correlação entre método de pagamento e valor
- Análise de inadimplência

## 🛠️ Ferramentas e Tecnologias Recomendadas

### **Linguagens de Programação:**
- **Python** (pandas, numpy, matplotlib, seaborn, plotly)
- **R** (dplyr, ggplot2, shiny)
- **SQL** (para consultas complexas)

### **Ferramentas de Visualização:**
- **Jupyter Notebooks** (análise exploratória)
- **Tableau/Power BI** (dashboards interativos)
- **Plotly/Dash** (visualizações web)
- **Matplotlib/Seaborn** (gráficos estáticos)

### **Ferramentas de Análise:**
- **Pandas** (manipulação de dados)
- **Scikit-learn** (machine learning)
- **Statsmodels** (análise estatística)
- **Folium** (mapas interativos)

## 📈 Métricas de Sucesso

### **Métricas de Negócio:**
- Aumento de 15% no ticket médio
- Redução de 20% no tempo de entrega
- Melhoria de 10% na satisfação do cliente
- Identificação de 5 novas oportunidades de mercado

### **Métricas Técnicas:**
- 95% de precisão nas previsões de vendas
- Tempo de processamento < 5 minutos
- Dashboards atualizados em tempo real
- Documentação completa do processo

## 🚀 Próximos Passos

### **Fase 1: Preparação e Limpeza (1-2 semanas)**
1. Carregamento e exploração inicial dos dados
2. Limpeza e tratamento de dados faltantes
3. Criação de variáveis derivadas
4. Validação da qualidade dos dados

### **Fase 2: Análise Exploratória (2-3 semanas)**
1. Análise univariada de todas as variáveis
2. Análise bivariada e correlações
3. Identificação de padrões e outliers
4. Criação de visualizações exploratórias

### **Fase 3: Análise Avançada (3-4 semanas)**
1. Análises de segmentação de clientes
2. Modelos preditivos de vendas
3. Análise de churn e retenção
4. Otimização de preços e promoções

### **Fase 4: Implementação e Monitoramento (2-3 semanas)**
1. Criação de dashboards interativos
2. Implementação de alertas automáticos
3. Documentação e treinamento
4. Monitoramento contínuo

## 📊 Exemplos de Insights Esperados

### **Insights de Vendas:**
- "Vendas aumentam 40% em novembro devido à Black Friday"
- "Categoria 'eletrônicos' representa 25% da receita total"
- "Ticket médio em SP é 30% maior que a média nacional"

### **Insights de Cliente:**
- "Clientes que compram parcelado têm 20% mais chance de recompra"
- "Tempo de entrega > 10 dias reduz satisfação em 35%"
- "Reviews negativas concentram-se em produtos de baixo preço"

### **Insights Geográficos:**
- "Sudeste concentra 60% das vendas"
- "Norte e Nordeste são mercados em crescimento"
- "Cidades com >100k habitantes têm 3x mais conversão"

## 🎓 Competências Desenvolvidas

Este projeto permite desenvolver habilidades em:
- **Análise de Dados**: Manipulação, limpeza e transformação
- **Visualização**: Criação de gráficos e dashboards
- **Estatística**: Análise descritiva e inferencial
- **Machine Learning**: Modelos preditivos e clustering
- **Storytelling**: Comunicação de insights de negócio
- **Programação**: Python/R e SQL

## 📚 Recursos Adicionais

### **Documentação:**
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/)
- [Seaborn Examples](https://seaborn.pydata.org/examples/)

### **Datasets Relacionados:**
- [Brazilian E-commerce Public Dataset](https://www.kaggle.com/olistbr/brazilian-ecommerce)
- [Olist Business Intelligence](https://olist.com/)


