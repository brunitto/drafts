# INNER LOOP

## Resumo

Rascunho sobre as atividades de desenvolvimento de software locais e específicas.

Este rascunho é contextualizado para aplicações web.

## Proposta

O _inner loop_ deve ser definido como um conjunto de atividades de desenvolvimento de software. Mais especificante, as atividades mais específicas executadas com mais frequência. Ainda, estas atividades têm alto impacto na produtividade.

A ordem das atividades deve seguir este modelo:

1. Spec: define o contexto, produto (métricas, funcionalidades, fluxos) e engenharia (arquitetura, testes, tecnologias).
2. Testes E2E: definem como o frontend deve funcionar, incluindo as interações do usuário e resultados esperados.
3. Frontend: implementa os adaptadores (componentes, páginas, etc) nas aplicações frontend (WEB, CLI).
4. Testes de Integração: definem como o backend deve funcionar, incluindo as aplicações e serviços.
5. Backend: implementa os adaptadores (repositórios, services, etc) nas aplicações backend (API, worker).
6. Testes Unitários: definem como as entidades e casos de uso devem funcionar.
7. Library: implementa as entidades e casos de uso do sistema (core).

Por exemplo, no desenvolvimento da funcionalidade "Gerenciar Postagens":

1. Spec: `specs/changes/feat-post-management/spec.md`.
2. Testes E2E: `apps/web/test/post-management.spec.ts`: `test('Shoud List Existing Posts')`, `await page.goto('/posts')`, `await expect(page.locator('#postList').toExist()`.
3. Frontend: `apps/web/src/posts/page.ts`: `async function PostsListPage(...)`, `apps/web/src/_components/post-card.ts`: `async function PostCard(...)`.
4. Testes de integração: `apps/api/test/post-list.test.ts`: `test('Should List Posts from the Database')`, `test('Should Not List Draft Posts')`.
5. Backend: `apps/api/src/api/posts/route.ts`: `async function GET(...)`, `apps/worker/src/post-approve.ts`: `async function approvePosts(...)`.
6. Testes Unitários: `libs/core/test/post.test.ts`: `test('Should Create With Valid Arguments')`, `test('Should Not Create with Invalid Email')`; `libs/core/test/post-list.test.ts`: `test('Should List Approved Posts')`.
7. Library: `libs/core/src/domain/entities/post.ts`: `class Post`; `libs/core/src/application/use-cases`: `class PostCreate`; `libs/core/src/application/interfaces/post-repository`: `interface PostRepository`.

**As pessoas e/ou agentes devem seguir essa ordem para garantir uma maior produtividade (quantidade de alterações testadas ao longo do tempo), aplicando SDD e TDD.**
