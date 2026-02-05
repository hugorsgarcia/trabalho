# Portfólio Profissional

## Sobre o Projeto

Site de portfólio profissional desenvolvido com HTML5, CSS3 e JavaScript. O projeto conta com uma pipeline completa de CI/CD usando GitHub Actions para garantir a qualidade e a publicação automática do código.

## Estrutura do Projeto

```
├── .github/
│   └── workflows/
│       ├── ci.yml          # Pipeline de Integração Contínua (PR)
│       └── cd.yml          # Pipeline de Entrega Contínua (Deploy)
├── images/
│   ├── profile.svg         # Imagem de perfil
│   ├── project1.svg        # Imagem do projeto 1
│   ├── project2.svg        # Imagem do projeto 2
│   └── project3.svg        # Imagem do projeto 3
├── .htmlhintrc             # Configuração do linter HTML
├── index.html              # Página principal do portfólio
├── style.css               # Folha de estilos
├── package.json            # Dependências (HTMLHint)
└── README.md               # Este arquivo
```

## Pipeline de CI (Integração Contínua)

A pipeline de CI é disparada em **Pull Requests para a branch `main`** e realiza as seguintes validações:

| Validação | Descrição |
|-----------|-----------|
| **index.html** | Verifica se o arquivo `index.html` existe na raiz |
| **Linter (HTMLHint)** | Valida o HTML seguindo padrões técnicos |
| **Tamanho de Arquivos** | Bloqueia arquivos individuais maiores que 500KB |
| **Termos Proibidos** | Impede `TODO`, `FIXME`, `senha` e `password` no código |
| **Links e Imagens** | Verifica URLs externas e caminhos locais de imagens |

### Matrix Strategy

O job de linter roda simultaneamente em **duas versões do Node.js** (18 e 20) usando `strategy: matrix`.

## Pipeline de CD (Entrega Contínua)

A pipeline de CD é disparada quando há um **push na branch `main`** (após merge de PR aprovado):

1. Faz checkout do código
2. Configura o GitHub Pages
3. Faz upload dos artefatos
4. Publica automaticamente no GitHub Pages

### Permissões Configuradas

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

## Notificações

As pipelines incluem steps de notificação de **sucesso** e **falha**. Para configurar notificações reais:

- **E-mail:** `dawidd6/action-send-mail@v3`
- **Discord:** `sarisia/actions-status-discord@v1`
- **Slack:** `slackapi/slack-github-action@v1`

## Proteção de Branch

Para ativar a proteção da branch `main` no GitHub:

1. Vá em **Settings** → **Branches** → **Add branch protection rule**
2. Em **Branch name pattern**, digite `main`
3. Marque **Require status checks to pass before merging**
4. Selecione os checks da pipeline de CI (`validacao`)
5. Salve as configurações

Isso impedirá que o botão de **Merge** fique habilitado se a pipeline falhar.

## Como Usar

### Desenvolvimento Local

```bash
# Instalar dependências
npm install

# Executar linter localmente
npm run lint
```

### Fluxo de Trabalho

1. Crie uma branch a partir de `main`
2. Faça suas alterações
3. Abra um Pull Request para `main`
4. A pipeline de CI será executada automaticamente
5. Se todas as validações passarem, faça o merge
6. A pipeline de CD fará o deploy automático no GitHub Pages

## Tecnologias

- HTML5
- CSS3
- JavaScript
- GitHub Actions
- GitHub Pages
- HTMLHint (Linter)
