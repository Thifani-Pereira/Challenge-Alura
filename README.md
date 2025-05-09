# Challenge-Alura

Tem por objetivo analisar o faturamento de uma loja e decidir quais devem permanecer abertas e quais devem encerrar suas atividades.
O material disponivel são 4 planilhas csv fornecidas diretamente pela Alura, sem sofrer alterações.
Foi utiizado a biblioteca  pandas e o matplot para fazer os graficos.
Para calcular o faturamento apliquei calculo simples de Preço ( produto) + Frete, soma total pois são os unicos dados em valores que tem

loja["Total"] = loja["Preço"] + loja["Frete"]
faturamento_total = loja["Total"].sum()

Depois apliquei o groupby para visualizar o faturamento pelo local de compra e classiqifuqei em ordem ascendente
faturamento_estado = loja.groupby("Local da compra")["Total"].sum().sort_values(ascending=False)
print(faturamento_estado)

Em vendas por categoria utilizei novamente o groupby e classificaçao ascendente
faturamento_categoria = loja.groupby("Categoria do Produto")["Total"].sum().sort_values(ascending=False)
print(faturamento_categoria)

As lojas tem avaliações,utilize o groupby para o Local de compra e valiação.mean para fazer a media de cada uma,
media_avaliacao_estado = loja.groupby("Local da compra")["Avaliação da compra"].mean().sort_values(ascending=False)
print(media_avaliacao_estado)

Produtos mais e menos vendidos
produtos_mais_vendidos = loja["Produto"].value_counts().head(10)
print(produtos_mais_vendidos)

produtos_menos_vendidos = loja["Produto"].value_counts(ascending=True).head(10)
print(produtos_menos_vendidos)

Frete Medio por loja 
frete_medio_por_loja = loja.groupby("Local da compra")["Frete"].mean().sort_values(ascending=False)
print(frete_medio_por_loja)

##Graficos
****Barra
import matplotlib.pyplot as plt

frete_medio_por_loja.plot(kind="bar", figsize=(10, 6), color="mediumseagreen")
plt.ylabel("Frete Médio (R$)")
plt.xlabel("Estado")
plt.title("Frete Médio por Loja (Estado)")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

***Pizza
import matplotlib.pyplot as plt

# Top 10 produtos mais vendidos
produtos_mais_vendidos = loja["Produto"].value_counts().head(10)

# Gráfico de pizza
plt.figure(figsize=(8, 8))
plt.pie(produtos_mais_vendidos, labels=produtos_mais_vendidos.index, autopct="%1.1f%%", startangle=140)
plt.title("Top 10 Produtos Mais Vendidos")
plt.axis("equal")  # Deixa o gráfico em formato de círculo
plt.tight_layout()
plt.show()

****Horizontal

import matplotlib.pyplot as plt

# Calcular o faturamento (Preço + Frete)
loja["Total"] = loja["Preço"] + loja["Frete"]

# Agrupar por estado e somar o total
faturamento_por_loja = loja.groupby("Local da compra")["Total"].sum().sort_values(ascending=False)

# Gráfico de barras
plt.figure(figsize=(10, 6))
faturamento_por_loja.plot(kind="barh", color="cornflowerblue")
plt.ylabel("Faturamento Total (R$)")
plt.xlabel("Loja (Estado)")
plt.title("Faturamento por Loja (Estado)")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

Analise 
Inserir uma coluna agrupando Faturamento , frete , Avaliação e criar uma pontuação baseada em pesos para melhor visualização. As lojas com pontuação baixa e frete alto serão recomendadas para fechamento.

As lojas com pontuação alta serão recomendadas para manter.

