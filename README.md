# coderouse-datadcience

Este projeto analisa o ciclo completo de pedidos do e‑commerce brasileiro (2016–2018) utilizando o dataset público da Olist, com ~100 mil pedidos e 9 tabelas relacionais em CSV que cobrem pedidos, itens, pagamentos, avaliações, clientes, vendedores, produtos, geolocalização e tradução de categorias. O objetivo é explorar logística, satisfação do cliente, receitas e comportamento de compra, além de construir métricas e modelos preditivos úteis para decisões de negócio.

## Tabelas principais
- olist_orders_dataset: status e linha do tempo dos pedidos, permitindo medir prazos e SLAs.

  - olist_order_items_dataset: itens por pedido (preço, frete, produto, vendedor).
  
  - olist_order_payments_dataset: meios de pagamento, parcelas e valores.
  
  - olist_order_reviews_dataset: notas e textos de avaliação pós‑compra.
  
  - olist_customers_dataset: identificação e localização de clientes.
  
  - olist_sellers_dataset: cadastro e localização de vendedores.
  
  - olist_products_dataset: catálogo, categorias e atributos físicos.
  
  - olist_geolocation_dataset: latitude/longitude por prefixo de CEP.
  
  - product_category_name_translation: tradução de categorias para inglês.

Principais perguntas de negócio
Logística: quais fatores explicam atrasos e variações de prazo entre estados, categorias e distâncias?

Satisfação: como atrasos e frete afetam o review_score e a reputação?

Receita e mix: quais categorias e sellers puxam faturamento e ticket médio?

Clientes: qual a taxa de recompra por UF e coortes sazonais?

Pagamentos: qual o impacto do tipo de pagamento e parcelamento em conversão e satisfação?

Métricas e modelos
Métricas: lead time de entrega, atraso vs. estimativa, ticket médio, participação do frete, taxa de cancelamento, NPS‑like por review_score.
