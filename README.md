# 🏙️ SmartCitySecurity

Um sistema integrado de segurança urbana que oferece ferramentas avançadas para monitoramento de crimes, gerenciamento de emergências, vigilância por câmeras e alocação de recursos policiais em tempo real.

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades Principais](#funcionalidades-principais)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração do Banco de Dados](#configuração-do-banco-de-dados)
- [Como Usar](#como-usar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [API Endpoints](#api-endpoints)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

## 🎯 Sobre o Projeto

**SmartCitySecurity** é uma aplicação web desenvolvida em ASP.NET Core que funciona como um sistema centralizado para gerenciamento de segurança pública. O projeto integra dados de habitantes, registro de crimes, emergências, sistemas de vigilância e recursos policiais em uma única plataforma.

### Objetivo
Fornecer às autoridades de segurança pública uma ferramenta robusta e intuitiva para:
- Monitorar incidentes criminais
- Gerenciar emergências urbanas
- Controlar sistemas de vigilância
- Otimizar a alocação de recursos policiais

## ✨ Funcionalidades Principais

### 1. **Gerenciamento de Habitantes**
- Cadastro completo com dados pessoais (nome, CPF, endereço, telefone)
- Registro de histórico criminal
- Observações e notas sobre residentes

### 2. **Registro de Crimes**
- Documentação detalhada de incidentes
- Classificação por tipo e gravidade
- Rastreamento de armas utilizadas
- Status do caso (aberto, fechado, investigando)

### 3. **Gerenciamento de Emergências**
- Registro de emergências com tipo, local e descrição
- Relacionamento com habitantes afetados
- Vinculação com sistemas de vigilância
- Rastreamento de status

### 4. **Sistemas de Vigilância**
- Cadastro de câmeras e sistemas de monitoramento
- Rastreamento de manutenção
- Registro de incidentes capturados
- Monitoramento de resolução de vídeo

### 5. **Recursos Policiais**
- Gestão de veículos, equipamentos e pessoal
- Acompanhamento de disponibilidade em tempo real
- Controle de capacidade e delegacias
- Histórico de manutenção
- API REST para integração com sistemas externos

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Descrição |
|------------|--------|-----------|
| **.NET** | 8.0 | Framework principal |
| **ASP.NET Core** | 8.0 | Framework web |
| **Entity Framework Core** | 8.0.6 | ORM para acesso a dados |
| **Oracle Database** | - | Banco de dados relacional |
| **C#** | 12.0 | Linguagem de programação |
| **HTML5** | - | Markup para interfaces |
| **CSS3** | - | Estilização |
| **JavaScript** | - | Interatividade do cliente |
| **Docker** | - | Containerização |

### Padrões e Arquitetura

- **Padrão MVC**: Controllers, Models, Views
- **Padrão Repository**: Abstração de acesso a dados
- **Padrão Service**: Lógica de negócio centralizada
- **Dependency Injection**: Injeção de dependências nativa do ASP.NET Core
- **RESTful API**: Endpoints para integração externa

## 📦 Pré-requisitos

Certifique-se de ter instalado:

- **.NET 8.0 SDK** ou superior - [Download](https://dotnet.microsoft.com/download)
- **Visual Studio 2022** ou **Visual Studio Code**
- **Oracle Database** (versão recomendada: 21c ou superior)
- **Git** para clonar o repositório
- **Docker** (opcional, para containerização)

## 🚀 Instalação

### 1. Clonar o Repositório

```bash
git clone https://github.com/saram0rais/SmartCitySecurity.git
cd SmartCitySecurity
```

### 2. Restaurar Dependências

```bash
dotnet restore
```

### 3. Configurar a String de Conexão

Abra o arquivo `appsettings.json` (ou crie-o se não existir) e configure a conexão com o Oracle:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Data Source=SEU_SERVIDOR;User Id=SEU_USUARIO;Password=SUA_SENHA;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information"
    }
  }
}
```

### 4. Aplicar Migrations

```bash
dotnet ef database update
```

### 5. Compilar o Projeto

```bash
dotnet build
```

### 6. Executar a Aplicação

```bash
dotnet run
```

A aplicação estará disponível em:
- HTTP: `http://localhost:5095`
- HTTPS: `https://localhost:7118`

## 🗄️ Configuração do Banco de Dados

### Tabelas Principais

O projeto implementa as seguintes entidades:

| Tabela | Descrição |
|--------|-----------|
| **HABITANTE** | Dados de residentes da cidade |
| **CRIME** | Registros de atos criminosos |
| **EMERGENCIA** | Registro de emergências urbanas |
| **SISTEMA_VIGILANCIA** | Câmeras e sistemas de monitoramento |
| **RECURSOS_POLICIAIS** | Veículos, equipamentos e pessoal |

### Índices Otimizados

```
IDX_ENDERECO_CPF - Busca por endereço e CPF
IDX_NOME_TIPO - Busca de crimes por nome e tipo
IDX_TIPO_DATA - Busca de emergências por tipo e data
IDX_NOME_LOCAL - Busca de sistemas por nome e localização
IDX_RECURSO_DISPONIBILIDADE - Busca de recursos por disponibilidade
```

## 📖 Como Usar

### Via Interface Web

1. Acesse a aplicação em `http://localhost:5095`
2. Navegue até as seções desejadas (Home, Modelos, etc.)
3. Insira, atualize ou visualize dados conforme necessário

### Via API REST

A aplicação expõe uma API RESTful para gerenciamento de recursos policiais:

```bash
# GET - Listar todos os recursos
GET /api/recursospoliciais

# GET - Obter recurso específico
GET /api/recursospoliciais/{id}

# POST - Criar novo recurso
POST /api/recursospoliciais
Content-Type: application/json

{
  "recurso": "Viatura Patrulha",
  "tipoRecurso": "Veículo",
  "disponibilidade": true,
  "localizacaoRecurso": "Centro",
  "nomeAgentes": "João Silva, Maria Santos",
  "delegacias": "Delegacia Central",
  "capacidade": 4,
  "aquisicao": "2024-01-15",
  "ultimaManutencao": "2024-05-01",
  "responsavelManutencao": "Carlos Oliveira"
}

# PUT - Atualizar recurso
PUT /api/recursospoliciais/{id}
Content-Type: application/json

# PUT - Atualizar status de disponibilidade
PUT /api/recursospoliciais/atualizar-status

# DELETE - Deletar recurso
DELETE /api/recursospoliciais/{id}
```

## 📁 Estrutura do Projeto

```
SmartCitySecurity/
├── Controllers/
│   ├── HomeController.cs          # Controlador principal
│   ├── ModeloController.cs        # Controlador de modelos
│   ├── PolicialController.cs      # Controlador de policiais
│   └── RecursosPoliciaisController.cs  # API REST para recursos
├── Models/
│   ├── Habitante.cs              # Entidade de habitante
│   ├── ModeloCrime.cs            # Entidade de crime
│   ├── ModeloEmergencia.cs       # Entidade de emergência
│   ├── ModeloSistemaVigilancia.cs # Entidade de vigilância
│   ├── RecursosPoliciais.cs      # Entidade de recursos
│   └── ErrorViewModel.cs         # Modelo de erro
├── Data/
│   ├── Contexts/
│   │   └── DatabaseContext.cs    # DbContext do Entity Framework
│   └── Repository/
│       ├── IRecursoPolicialRepository.cs  # Interface do repositório
│       └── RecursoPolicialRepository.cs   # Implementação
├── Services/
│   ├── IRecursoService.cs        # Interface de serviço
│   └── RecursoService.cs         # Implementação de serviço
├── Migrations/                    # Histórico de migrações
├── Views/                         # Views MVC
├── Properties/
│   └── launchSettings.json       # Configurações de execução
├── Dockerfile                     # Containerização
└── README.md                      # Este arquivo
```

## 🔌 API Endpoints

### RecursosPoliciais Controller
- `GET /api/recursospoliciais` - Listar todos os recursos
- `GET /api/recursospoliciais/{id}` - Obter recurso por ID
- `POST /api/recursospoliciais` - Criar novo recurso
- `PUT /api/recursospoliciais/{id}` - Atualizar recurso
- `DELETE /api/recursospoliciais/{id}` - Deletar recurso
- `PUT /api/recursospoliciais/atualizar-status` - Atualizar status de disponibilidade

### Controllers MVC
- `GET /` - Home page
- `GET /privacy` - Página de privacidade
- `GET /modelo` - Página de modelos
- `GET /error` - Página de erro

## 🔄 Fluxo de Dados

```
Usuário → Views (MVC) → Controllers → Services → Repository → Database
           ↓                                                        ↑
        API Client ────────────────────────────────────────────────
```

## 🔐 Segurança

- Validação de entrada em todos os endpoints
- Consultas parametrizadas para prevenção de SQL Injection
- Relacionamentos com integridade referencial
- Constraint de chaves estrangeiras

## 📊 Funcionalidade de Monitoramento de Disponibilidade

O método `AtualizarStatusDisponibilidade()` verifica automaticamente a disponibilidade dos recursos baseado na manutenção:

```csharp
// Recursos sem manutenção há mais de 24 horas são marcados como indisponíveis
if (DateTime.UtcNow - recurso.UltimaManutencao > TimeSpan.FromHours(24))
{
    recurso.Disponibilidade = false;
}
```

## 🐳 Docker

Para executar a aplicação em container:

```bash
docker build -t smartcitysecurity .
docker run -p 8080:8080 -p 8081:8081 smartcitysecurity
```

## 📝 Exemplo de Uso Completo

```csharp
// Criar um novo recurso
var novoRecurso = new RecursosPoliciais
{
    Recurso = "Viatura Motocicleta",
    TipoRecurso = "Veículo",
    Disponibilidade = true,
    LocalizacaoRecurso = "Zona Norte",
    NomeAgentes = "Pedro Costa",
    Delegacias = "Delegacia Zona Norte",
    Capacidade = 1,
    Aquisicao = DateTime.Now,
    UltimaManutencao = DateTime.Now,
    ReponsavelManutencao = "João Técnico"
};

await _recursoService.CriarRecurso(novoRecurso);
```

## 🚧 Status do Projeto

- ✅ Estrutura base implementada
- ✅ Models e migrações configuradas
- ✅ Repository Pattern
- ✅ Service Layer
- ✅ API REST básica
- 🔄 Interfaces avançadas em desenvolvimento
- 📋 Testes unitários (planejado)

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📞 Contato e Suporte

Para dúvidas ou sugestões sobre o projeto:
- 📧 GitHub: [@saram0rais](https://github.com/saram0rais)
- 📁 Repositório: [SmartCitySecurity](https://github.com/saram0rais/SmartCitySecurity)

## 📄 Licença

Este projeto está disponível sob a Licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

## 📚 Referências e Documentação

- [Microsoft .NET Documentation](https://docs.microsoft.com/dotnet/)
- [ASP.NET Core](https://docs.microsoft.com/aspnet/core/)
- [Entity Framework Core](https://docs.microsoft.com/ef/core/)
- [Oracle Database](https://www.oracle.com/database/)

---

**Desenvolvido por:** [saram0rais](https://github.com/saram0rais)  
**Última atualização:** 2026-05-08  
**Versão:** 1.0.0
