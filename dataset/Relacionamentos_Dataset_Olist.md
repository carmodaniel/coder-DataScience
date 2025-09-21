# Estratégia de Relacionamentos - Dataset Olist

## 🔗 Mapa de Relacionamentos

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              CORE BUSINESS ENTITIES                            │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐            │
│  │   CUSTOMERS     │    │     ORDERS      │    │    PRODUCTS     │            │
│  │                 │    │                 │    │                 │            │
│  │ • customer_id   │◄───┤ • order_id      │    │ • product_id    │            │
│  │ • customer_     │    │ • customer_id   │    │ • category_name │            │
│  │   unique_id     │    │ • status        │    │ • dimensions    │            │
│  │ • zip_code      │    │ • timestamps    │    │ • weight        │            │
│  │ • city/state    │    │ • delivery      │    │                 │            │
│  └─────────────────┘    └─────────────────┘    └─────────────────┘            │
│           │                       │                       ▲                   │
│           │                       │                       │                   │
│           │                       ▼                       │                   │
│           │              ┌─────────────────┐              │                   │
│           │              │  ORDER_ITEMS    │              │                   │
│           │              │                 │              │                   │
│           │              │ • order_id      │──────────────┘                   │
│           │              │ • product_id    │                                  │
│           │              │ • seller_id     │                                  │
│           │              │ • price         │                                  │
│           │              │ • freight_value │                                  │
│           │              └─────────────────┘                                  │
│           │                       │                                           │
│           │                       ▼                                           │
│           │              ┌─────────────────┐                                  │
│           │              │    SELLERS      │                                  │
│           │              │                 │                                  │
│           │              │ • seller_id     │                                  │
│           │              │ • zip_code      │                                  │
│           │              │ • city/state    │                                  │
│           │              └─────────────────┘                                  │
│           │                                                                   │
│           └───────────────────────────────────────────────────────────────────┘
│
├─────────────────────────────────────────────────────────────────────────────────┤
│                              SUPPORTING ENTITIES                               │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐            │
│  │ ORDER_PAYMENTS  │    │ ORDER_REVIEWS   │    │   GEOLOCATION   │            │
│  │                 │    │                 │    │                 │            │
│  │ • order_id      │    │ • order_id      │    │ • zip_code      │            │
│  │ • payment_type  │    │ • review_score  │    │ • lat/lng       │            │
│  │ • installments  │    │ • comments      │    │ • city/state    │            │
│  │ • payment_value │    │ • timestamps    │    │                 │            │
│  └─────────────────┘    └─────────────────┘    └─────────────────┘            │
│           │                       │                       │                   │
│           └───────────────────────┼───────────────────────┼───────────────────┘
│                                   │                       │
│                                   ▼                       ▼
│                          ┌─────────────────┐    ┌─────────────────┐
│                          │     ORDERS      │    │ CUSTOMERS/      │
│                          │   (CENTRAL)     │    │ SELLERS         │
│                          └─────────────────┘    └─────────────────┘
│
├─────────────────────────────────────────────────────────────────────────────────┤
│                              REFERENCE TABLES                                  │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │              PRODUCT_CATEGORY_NAME_TRANSLATION                          │   │
│  │                                                                         │   │
│  │ • product_category_name (PT)                                           │   │
│  │ • product_category_name_english (EN)                                   │   │
│  │                                                                         │   │
│  │ └─► Links to: PRODUCTS.product_category_name                           │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

## 🎯 Estratégia de Relacionamento para Máximo Valor em Análise

### **1. TABELA CENTRAL: ORDERS**
A tabela `orders` é o **hub central** que conecta todos os outros dados:
- **Chave Primária**: `order_id`
- **Função**: Conecta clientes, produtos, vendedores, pagamentos e reviews
- **Valor**: Permite análises de jornada completa do cliente

### **2. RELACIONAMENTOS PRINCIPAIS**

#### **A) CUSTOMER JOURNEY (Jornada do Cliente)**
```
CUSTOMERS → ORDERS → ORDER_ITEMS → PRODUCTS
         ↓         ↓
    GEOLOCATION  ORDER_PAYMENTS
                ORDER_REVIEWS
```

#### **B) SELLER PERFORMANCE (Performance do Vendedor)**
```
SELLERS → ORDER_ITEMS → ORDERS → CUSTOMERS
        ↓             ↓
   GEOLOCATION    ORDER_REVIEWS
```

#### **C) PRODUCT ANALYTICS (Análise de Produtos)**
```
PRODUCTS → ORDER_ITEMS → ORDERS → CUSTOMERS
         ↓             ↓
CATEGORY_TRANSLATION  ORDER_REVIEWS
```

## 📊 Análises de Alto Valor Possíveis

### **1. ANÁLISE DE CUSTOMER LIFETIME VALUE (CLV)**
```sql
-- Exemplo de Query para CLV
SELECT 
    c.customer_unique_id,
    c.customer_state,
    COUNT(DISTINCT o.order_id) as total_orders,
    SUM(oi.price + oi.freight_value) as total_spent,
    AVG(r.review_score) as avg_satisfaction,
    DATEDIFF(MAX(o.order_purchase_timestamp), MIN(o.order_purchase_timestamp)) as customer_lifespan_days
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
LEFT JOIN order_reviews r ON o.order_id = r.order_id
GROUP BY c.customer_unique_id, c.customer_state
```

### **2. ANÁLISE GEOGRÁFICA DE PERFORMANCE**
```sql
-- Performance por Região
SELECT 
    c.customer_state,
    g.geolocation_lat,
    g.geolocation_lng,
    COUNT(DISTINCT o.order_id) as total_orders,
    SUM(oi.price) as total_revenue,
    AVG(r.review_score) as avg_satisfaction
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN geolocation g ON c.customer_zip_code_prefix = g.geolocation_zip_code_prefix
LEFT JOIN order_reviews r ON o.order_id = r.order_id
GROUP BY c.customer_state, g.geolocation_lat, g.geolocation_lng
```

### **3. ANÁLISE DE PRODUTOS E CATEGORIAS**
```sql
-- Top Categorias com Performance
SELECT 
    pct.product_category_name_english,
    COUNT(DISTINCT oi.order_id) as total_orders,
    SUM(oi.price) as total_revenue,
    AVG(oi.price) as avg_price,
    AVG(r.review_score) as avg_rating,
    COUNT(DISTINCT s.seller_id) as unique_sellers
FROM products p
JOIN product_category_name_translation pct ON p.product_category_name = pct.product_category_name
JOIN order_items oi ON p.product_id = oi.product_id
JOIN orders o ON oi.order_id = o.order_id
JOIN sellers s ON oi.seller_id = s.seller_id
LEFT JOIN order_reviews r ON o.order_id = r.order_id
GROUP BY pct.product_category_name_english
ORDER BY total_revenue DESC
```

## 🔄 Estratégias de Join para Diferentes Análises

### **1. INNER JOIN (Dados Completos)**
- Use quando precisar de dados completos de todas as tabelas
- Ideal para análises de performance e métricas de negócio
- Exemplo: Análise de receita por vendedor

### **2. LEFT JOIN (Dados com Tolerância a Faltantes)**
- Use quando alguns dados podem estar ausentes
- Ideal para análises de satisfação (nem todos os pedidos têm review)
- Exemplo: Análise de CLV incluindo clientes sem reviews

### **3. FULL OUTER JOIN (Análise Completa)**
- Use para análises de cobertura e qualidade de dados
- Ideal para identificar gaps nos dados
- Exemplo: Verificar quais produtos nunca foram vendidos

## 📈 Métricas de Negócio que Podem Ser Calculadas

### **Métricas de Vendas:**
- Receita total por período/região/categoria
- Ticket médio por cliente/vendedor/categoria
- Taxa de conversão por região
- Sazonalidade de vendas

### **Métricas de Cliente:**
- Customer Lifetime Value (CLV)
- Taxa de retenção de clientes
- Frequência de compra
- Tempo médio entre compras

### **Métricas de Produto:**
- Produtos mais vendidos por categoria
- Margem de lucro por produto
- Velocidade de venda
- Performance por categoria

### **Métricas de Vendedor:**
- Performance por vendedor
- Concentração de vendas
- Satisfação média dos clientes por vendedor
- Crescimento de vendas por vendedor

### **Métricas Geográficas:**
- Densidade de vendas por região
- Crescimento por mercado
- Correlação geográfica com satisfação
- Identificação de mercados emergentes

## 🛠️ Implementação Prática

### **1. Criação de Views para Análises Frequentes**
```sql
-- View: Customer Analytics
CREATE VIEW customer_analytics AS
SELECT 
    c.customer_unique_id,
    c.customer_state,
    COUNT(DISTINCT o.order_id) as total_orders,
    SUM(oi.price + oi.freight_value) as total_spent,
    AVG(r.review_score) as avg_satisfaction
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
LEFT JOIN order_reviews r ON o.order_id = r.order_id
GROUP BY c.customer_unique_id, c.customer_state;
```

### **2. Índices Recomendados**
```sql
-- Índices para performance
CREATE INDEX idx_orders_customer_id ON orders(customer_id);
CREATE INDEX idx_order_items_order_id ON order_items(order_id);
CREATE INDEX idx_order_items_product_id ON order_items(product_id);
CREATE INDEX idx_order_items_seller_id ON order_items(seller_id);
CREATE INDEX idx_geolocation_zip ON geolocation(geolocation_zip_code_prefix);
```

### **3. Estrutura de Dados para Análise**
```python
# Exemplo em Python/Pandas
import pandas as pd

# Carregar dados
orders = pd.read_csv('olist_orders_dataset.csv')
customers = pd.read_csv('olist_customers_dataset.csv')
order_items = pd.read_csv('olist_order_items_dataset.csv')
products = pd.read_csv('olist_products_dataset.csv')
sellers = pd.read_csv('olist_sellers_dataset.csv')
reviews = pd.read_csv('olist_order_reviews_dataset.csv')
payments = pd.read_csv('olist_order_payments_dataset.csv')
geolocation = pd.read_csv('olist_geolocation_dataset.csv')
category_translation = pd.read_csv('product_category_name_translation.csv')

# Criar dataset unificado para análise
df_analysis = (orders
    .merge(customers, on='customer_id', how='left')
    .merge(order_items, on='order_id', how='left')
    .merge(products, on='product_id', how='left')
    .merge(sellers, on='seller_id', how='left')
    .merge(reviews, on='order_id', how='left')
    .merge(payments, on='order_id', how='left')
    .merge(category_translation, on='product_category_name', how='left')
)
```

## 🎯 Próximos Passos Recomendados

1. **Implementar os relacionamentos** usando as queries SQL fornecidas
2. **Criar views materializadas** para análises frequentes
3. **Desenvolver dashboards** baseados nas métricas identificadas
4. **Implementar alertas** para métricas críticas de negócio
5. **Documentar** todos os relacionamentos e métricas calculadas

---

**Data de Criação**: Dezembro 2024  
**Versão**: 1.0  
**Foco**: Maximizar valor em análise de dados através de relacionamentos estratégicos
