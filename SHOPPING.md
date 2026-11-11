# Carrinho e pedidos

O carrinho é salvo no banco por usuário autenticado. Na loja, use **Adicionar ao carrinho**; em **Carrinho**, altere as quantidades, remova itens e confira o total em ouros. **Finalizar pedido** registra a compra, esvazia o carrinho e abre o histórico em **Meu perfil**. Este fluxo registra pedidos; não processa pagamentos.

Os pedidos guardam nome, preço unitário, quantidade e subtotal da compra. Alterações ou exclusões posteriores no catálogo não alteram o histórico. O servidor calcula os valores, limita cada quantidade a 999 e restringe o acesso aos dados do próprio usuário.

## Preparação

O Compose da raiz usa as pastas `stardew-api` e `teste`. Com o ambiente Docker disponível:

```sh
docker compose up -d --build
docker compose exec php php artisan migrate
```

Para uma instalação nova sem catálogo, execute também:

```sh
docker compose exec php php artisan db:seed
```

## Verificação

Com PHP, dependências Composer e SQLite de teste disponíveis, execute em `stardew-api`:

```sh
php artisan test --filter=ShoppingTest
```

Em `teste`, com Node e dependências disponíveis:

```sh
npm ci
npm run build
```

Verifique no navegador: adicionar duas sementes, atualizar a página, sair e entrar novamente; o carrinho deve permanecer. Finalize o pedido e confira os itens e o total no perfil. Entre com outra conta para conferir que seus dados não aparecem nela.
