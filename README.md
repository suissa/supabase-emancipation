<h1 align="center">Cogful Coding: supabase emancipation</h1>


![Cogful Coding: supabase emancipation](https://i.imgur.com/MaIgxym.png)




# Primeira etapa: liberdade de backend, sem retrabalho

Nesta primeira etapa, a ideia é não quebrar nada do que você já tem.
Você pode continuar usando Firebase normalmente, enquanto criamos uma réplica em tempo real dos dados.

A diferença é que, a partir daqui, você passa a ter liberdade total de infraestrutura:

seguir só com Firebase,

usar Postgres local,

ou rodar os dois em paralelo, sem mudar seu código de negócio.

Eu vou entregar uma biblioteca compatível com as rotas do supabase, mas implementada sobre Postgres.
Na prática, isso significa: mesmas chamadas, mesmos contratos, outro backend.

Eu criei e testei em uma base de dados pequena e funcionou certinho, mas se a sua for grande sempre verifique o resultado e faça uma lista manual do nome das suas tabelas para validar já no início se ele conseguiu listar todas. Caso não tenha conseguido, crie uma issue aqui falando qual foi a diferença, quero ir melhoranddo a medida que vierem os pedidos para chegar em um solução que funcione para qualquer tamanho de database.

Essa é a sequência dos prompts. Não coloquei tudo em 1 para que você possa validar passo a passo.

- [prompt01](prompt01.md)
- [prompt02](prompt02.md)
- [prompt03](prompt03.md)
- [prompt04](prompt04.md)
- [prompt05](prompt05.md)
- [prompt06](prompt06.md)

Aguardo seu feedback.


<div align="center">
<img src="https://i.imgur.com/yTjCuyT.png" style="300px" alt="o futuro é agêntico" />
</div>


