# Proxy para autenticação Sanctum

Implementação nova, baseada no front e na API disponíveis. Não é uma recuperação dos arquivos originais.

O navegador acessa http://localhost:8080. O Nginx encaminha /api/* e /sanctum/* para a API Laravel; as demais chamadas vão para o Vue/Vite.

1. O front solicita GET /sanctum/csrf-cookie.
2. Laravel devolve os cookies de sessão e XSRF-TOKEN.
3. Axios envia POST /api/login com as credenciais, cookies e X-XSRF-TOKEN.
4. Laravel valida as credenciais e regenera a sessão.
5. GET /api/me e as demais rotas protegidas usam auth:sanctum.
6. POST /api/logout invalida a sessão.

O proxy preserva os cookies e cabeçalhos. A autenticação é feita pelo Laravel. Não há tokens salvos no localStorage nem validação de senha no Nginx.

Configuração destinada ao desenvolvimento local com Docker Compose da raiz. Não use o compose interno da pasta api ao mesmo tempo.
Documentação: https://laravel.com/docs/12.x/sanctum#spa-authentication
