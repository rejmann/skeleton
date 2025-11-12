# Skeleton Project

Um skeleton (template) de projeto PHP moderno usando Symfony 7.3 com Docker, ferramentas de qualidade de código e ambiente de desenvolvimento completo.

## 📋 Visão Geral

Este projeto é um template base para desenvolvimento de aplicações web usando Symfony Framework. Inclui configuração completa de ambiente de desenvolvimento com Docker, ferramentas de análise de código, testes automatizados e estrutura organizacional otimizada.

## 🛠 Stack Tecnológica

### Framework & Runtime
- **PHP 8.2+** - Linguagem principal
- **Symfony 7.3** - Framework web
- **MySQL 8.0** - Banco de dados
- **Redis** - Cache e filas
- **Nginx** - Servidor web
- **Docker & Docker Compose** - Containerização

### Dependências Principais
- **Doctrine ORM** - Mapeamento objeto-relacional
- **Twig** - Template engine
- **Symfony Security** - Autenticação e autorização
- **Symfony Mailer** - Envio de emails
- **Symfony Messenger** - Sistema de filas
- **Monolog** - Sistema de logs

### Ferramentas de Desenvolvimento
- **PHPUnit** - Testes unitários
- **PHPStan** - Análise estática de código
- **PHP-CS-Fixer** - Formatação de código
- **PHPMD** - Detector de bagunça de código
- **Doctrine Fixtures** - Dados de teste
- **Symfony Web Profiler** - Debug e profiling

## 🚀 Instalação e Configuração

### Pré-requisitos
- Docker e Docker Compose
- Make (opcional, mas recomendado)
- Git

### 1. Clone o projeto
```bash
git clone <repository-url>
cd skeleton
```

### 2. Configuração inicial
```bash
# Instala arquivo de ambiente e hooks do git
make setup
```

Este comando irá:
- Copiar `.env.dist` para `.env`
- Instalar hooks do git para pre-commit
- Subir os containers Docker
- Instalar dependências do Composer
- Executar migrações do banco
- Configurar permissões
- Adicionar entrada no `/etc/hosts`

### 3. Acesso à aplicação
Após a instalação, a aplicação estará disponível em:
- **Web**: http://skeleton.test:8080 ou http://localhost:8080
- **MySQL**: localhost:3310
- **Redis**: localhost:6379

## 🐳 Docker Services

O projeto utiliza os seguintes serviços Docker:

### app
- Container principal da aplicação PHP-FPM
- Base: PHP 8.2-FPM com extensões necessárias

### worker
- Container para processamento de filas/workers
- Executa jobs assíncronos via Symfony Messenger

### nginx
- Servidor web
- Proxy reverso para a aplicação PHP

### mysql
- Banco de dados MySQL 8.0
- Dados persistidos em volume Docker

### redis
- Cache e sistema de filas
- Usado pelo Symfony Lock e Messenger

## 📁 Estrutura do Projeto

```
skeleton/
├── src/
│   ├── App/           # Código da aplicação principal
│   └── Skeleton/      # Módulos/domínios específicos
├── config/            # Configurações do Symfony
├── templates/         # Templates Twig
├── tests/            # Testes automatizados
├── migrations/       # Migrações do banco de dados
├── public/           # Assets públicos
├── devops/           # Configurações Docker
├── bin/              # Scripts executáveis
└── cli/              # Scripts CLI customizados
```

## 🔧 Comandos Disponíveis (Make)

### Configuração e Infraestrutura
```bash
make setup              # Configuração inicial completa
make up                 # Iniciar ambiente de desenvolvimento
make docker-up          # Apenas subir containers
make composer-install   # Instalar dependências PHP
make fix-permissions    # Corrigir permissões de arquivos
```

### Banco de Dados
```bash
make migrate            # Executar migrações
make doctrine-diff      # Gerar migração baseada em mudanças nas entidades
make empty-migration    # Criar migração vazia
make migrations-check   # Verificar status das migrações
```

### Qualidade de Código
```bash
make check              # Executar todas as verificações
make phpstan            # Análise estática com PHPStan
make phpmd              # Detecção de problemas com PHPMD
make php-cs-fixer       # Corrigir formatação do código
make php-cs-fixer-check # Verificar formatação sem corrigir
make auto-fix           # Corrigir problemas automaticamente
```

### Testes
```bash
make tests              # Executar todos os testes
```

## 🧪 Scripts CLI Customizados

O projeto inclui vários scripts personalizados na pasta `cli/`:

- `cli/console` - Wrapper para comandos Symfony
- `cli/composer` - Wrapper para Composer
- `cli/tests` - Executar testes
- `cli/phpstan` - Análise estática
- `cli/phpmd` - Detector de problemas
- `cli/php-cs-fixer` - Formatação de código
- `cli/run-at-container` - Executar comandos dentro do container

## 🔒 Qualidade e Padronização

### Pre-commit Hook
O projeto inclui um hook de pre-commit que executa:
- Verificação de sintaxe PHP
- PHPStan (análise estática)
- PHPMD (detecção de problemas)
- PHP-CS-Fixer (formatação)

### Configurações de Qualidade
- **phpstan.neon** - Configuração do PHPStan
- **phpmd.xml** - Regras do PHPMD
- **phpunit.dist.xml** - Configuração dos testes
- **.php-cs-fixer.dist.php** - Regras de formatação

## 🌐 Variáveis de Ambiente

As principais variáveis estão no arquivo `.env`:

```env
APP_ENV=dev                    # Ambiente (dev/prod)
APP_SECRET=<secret>            # Chave secreta do Symfony
APP_DOMAIN=skeleton.test       # Domínio da aplicação
APP_PORT=8080                  # Porta da aplicação
DATABASE_URL=mysql://...       # URL do banco de dados
REDIS_URL=redis://redis        # URL do Redis
MAILER_DSN=null://null         # Configuração do mailer
```

## 🚀 Deploy e Produção

### Workers e Crons
```bash
# Iniciar workers supervisor (executar como root)
make start-crons
```

### Considerações para Produção
- Configurar `APP_ENV=prod`
- Definir `APP_SECRET` seguro
- Configurar `MAILER_DSN` apropriado
- Configurar volumes persistentes para uploads
- Configurar backup do banco de dados
- Configurar monitoramento e logs

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

### Padrões de Código
- Seguir PSR-12 para formatação
- Utilizar PHPStan nível máximo
- Manter cobertura de testes
- Documentar classes e métodos públicos

## 📝 Licença

Este projeto é proprietário. Todos os direitos reservados.

## 🆘 Troubleshooting

### Problemas Comuns

**Erro de permissões:**
```bash
make fix-permissions
```

**Containers não sobem:**
```bash
docker compose down
docker compose up -d --remove-orphans
```

**Banco de dados não conecta:**
- Verificar se o MySQL está healthy: `docker compose ps`
- Verificar logs: `docker compose logs mysql`

**Site não carrega:**
- Verificar se foi adicionado ao `/etc/hosts`: `127.0.0.1 skeleton.test`
- Verificar se a porta 8080 está livre

### Comandos Úteis de Debug

```bash
# Ver logs dos containers
docker compose logs -f

# Executar bash no container da aplicação
docker compose exec app bash

# Ver status dos serviços
docker compose ps

# Limpar cache do Symfony
cli/console cache:clear
```

## 📚 Documentação Adicional

- [Symfony Documentation](https://symfony.com/doc)
- [Doctrine ORM](https://www.doctrine-project.org/projects/orm.html)
- [PHPUnit](https://phpunit.de/documentation.html)
- [PHPStan](https://phpstan.org/user-guide/getting-started)
