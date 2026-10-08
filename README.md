# E-commerce | Sistema de Pedidos

Aplicação de console em **Java** que simula a gestão de pedidos de uma loja
(e-commerce): cadastro de clientes e produtos, montagem de pedidos, pagamento,
controle de estoque e acompanhamento da situação do pedido, com persistência em
banco de dados SQLite.

## Origem e autoria

Este projeto foi desenvolvido inicialmente em grupo para a disciplina de
**Linguagem de Programação II**, com a participação de Iago Diogo Procopio Santana
e seus colegas.

A versão acadêmica está disponível no
[repositório original](https://github.com/RafaelFernandes12/lp2-ecommerce).
Este repositório foi iniciado a partir de uma cópia dessa versão e não contém o
histórico de commits do projeto original.

A partir dessa base, Iago dá continuidade ao projeto com correções, testes e
novas funcionalidades, registrando as mudanças em etapas. A autoria da versão
inicial é compartilhada; as evoluções posteriores serão documentadas no
histórico deste repositório.

## Pré-requisitos

- **Java 17 ou superior**.
- As dependências (`sqlite-jdbc` e `slf4j`) já acompanham o projeto na pasta
  `lib/`, então não é necessário Maven nem acesso à internet.

Verifique sua versão do Java:

```bash
java -version
```

## Como executar

### Linux / macOS

```bash
./run.sh
```

(se necessário: `chmod +x run.sh`)

### Windows

```bat
run.bat
```

### Manualmente (qualquer SO)

```bash
# compilar
javac -d target/classes -cp "lib/*" $(find src -name '*.java')

# executar (Linux/macOS — use ';' no lugar de ':' no Windows)
java -cp "target/classes:lib/*" br.com.loja.Main
```

Ao iniciar, o sistema cria o arquivo de banco `loja.db` na pasta atual (se ainda
não existir) e carrega os dados já salvos. Use o menu do terminal para cadastrar
clientes/produtos e operar os pedidos.

## Estrutura do projeto

```
src/main/java/br/com/loja/
├── Main.java                  # inicializa o banco, carrega dados e abre o menu
├── model/                     # entidades + situação do pedido
│   ├── Pessoa, Cliente, ClienteRegular, ClienteVip
│   ├── Produto, ProdutoFisico, ProdutoDigital
│   ├── Pedido, ItemPedido, SituacaoPedido (enum)
│   └── Pagamento, PagamentoPix, PagamentoCartao
├── exception/                 # exceções personalizadas
├── persistence/               # ConexaoSQLite + ClienteDAO/ProdutoDAO/PedidoDAO
├── service/                   # ClienteService/ProdutoService/PedidoService
└── ui/                        # MenuPrincipal (terminal)
lib/                           # dependências (sqlite-jdbc, slf4j)
```

## Funcionamento

- **Clientes**: tipos Regular e VIP, com regras de desconto próprias (VIP 10%
  sempre; Regular 5% apenas na primeira compra).
- **Produtos**: físicos (frete por peso) e digitais (frete grátis), com controle
  de estoque.
- **Pedidos**: passam pelos estados `ACEITO → PAGO → ENVIADO → ENTREGUE`, com
  `CANCELADO` permitido apenas antes do envio.
- **Pagamentos**: Pix (5% de desconto) ou Cartão (juros quando parcelado).
- **Persistência**: clientes, produtos e pedidos são gravados no SQLite e
  recarregados na inicialização.

## Evolução planejada

A versão atual funciona pelo terminal e simula os pagamentos, sem integração
com serviços de cobrança. As etapas abaixo são planejadas e ainda não foram
implementadas nesta continuidade:

- Corrigir inconsistências no fluxo de pedidos, estoque e persistência.
- Preservar os valores históricos das compras e aprimorar as validações.
- Adicionar testes automatizados para as regras de negócio.
- Evoluir para uma interface web com catálogo, carrinho e checkout simulado.
- Preparar uma demonstração do projeto para o portfólio.

Cada etapa será desenvolvida, verificada e registrada em commits que descrevam
a mudança realizada.
