# coderouse-datscience

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

## Por que olhar para esses dados
Toda compra online passa por etapas: escolher o produto, pagar, enviar, entregar e avaliar a experiência. Entender como isso funciona na prática ajuda a vender melhor, atrasar menos e deixar quem compra mais satisfeito. Com os gráficos, dá para enxergar onde estão as boas oportunidades e os pontos de atenção do negócio.

### O que cada gráfico ajuda a responder
- **Top 10 categorias por receita**.   
O que mostra: as categorias que mais geram dinheiro somando preço e frete.
Por que importa: aponta onde concentrar esforços de marketing, negociar com fornecedores e revisar o portfólio.
Como ler: barras maiores = mais receita. Vale checar se essas categorias também têm boa margem e poucas reclamações.

- **Tempo de entrega por estado (UF)**.
O que mostra: quantos dias em média um pedido leva para chegar em cada estado.
Por que importa: diferenças entre estados revelam gargalos de logística, como distância ou rota.
Como ler: a linha do meio (mediana) é o “padrão” do estado; caixas altas e pontos muito fora indicam variação grande e possíveis atrasos.

- **Atraso x satisfação**.
O que mostra: a nota média de avaliação quando o pedido chega no prazo versus quando atrasa.
Por que importa: comprova com dados que atraso derruba a satisfação e, no fim, a reputação.
Como ler: se a barra de “Atrasado” for bem menor, diminuir atrasos deve ser prioridade.

- **Peso do frete no total por categoria**.
O que mostra: qual parte do valor pago é frete, por categoria.
Por que importa: quando o frete pesa muito, a compra fica menos atrativa; talvez valha repensar embalagem, rotas ou promoções de frete.
Como ler: categorias com proporção alta pedem teste de frete grátis em valor mínimo, kits de produtos ou ajustes de logística.

- **Receita por mês**.
O que mostra: a evolução da receita ao longo do tempo.
Por que importa: ajuda a identificar sazonalidade (ex.: fim de ano), quedas inesperadas e efeitos de campanhas.
Como ler: procure picos e vales; conecte-os a ações reais (promoções, mudanças de frete, catálogo) para repetir o que funcionou.
