# Projeto Back-End

**Grupo**: Pedro Santos, Gabriel Melo, Bernardo Brandao, Iago Viana, Gabriel Maccachero

## Sobre

O VerificaEstagio e uma API Django para cadastro e verificacao de contratos de estagio. O sistema registra alunos, empresas, instituicoes, estagios, contratos, analises, pendencias, relatorios de conformidade e pareceres institucionais.

## Tecnologias

- Python
- Django
- Django REST Framework
- drf-spectacular
- SQLite
- MkDocs

## Como Rodar

```powershell
python -m pip install -r requirements.txt
$env:DJANGO_DEBUG = "True"
python manage.py migrate
python populate_data.py   # opcional: dados de exemplo
python manage.py runserver
```

O banco (`db.sqlite3`) e os arquivos enviados (`media/`) não ficam no repositório. O `migrate` cria um banco vazio na primeira execução.

## Configuração

As configurações sensíveis vêm de variáveis de ambiente, nunca do código:

| Variável | Para que serve | Padrão |
|---|---|---|
| `DJANGO_DEBUG` | `True` liga o modo de desenvolvimento | `False` |
| `DJANGO_SECRET_KEY` | Chave secreta do Django. Obrigatória com `DJANGO_DEBUG` desligado | Gerada a cada execução no modo de desenvolvimento |
| `DJANGO_ALLOWED_HOSTS` | Domínios aceitos, separados por vírgula | `localhost,127.0.0.1` |

Para gerar uma chave:

```powershell
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Em produção, defina `DJANGO_SECRET_KEY` e `DJANGO_ALLOWED_HOSTS`, deixe `DJANGO_DEBUG` desligado e use um banco como o PostgreSQL no lugar do SQLite.

## Endpoints Principais

- `GET /api/docs/`: Swagger UI
- `GET /api/redoc/`: ReDoc
- `GET /api/schema/`: schema OpenAPI
- `POST /api/auth/register/`: cadastro de usuario Django
- `POST /api/auth/login/`: login por sessao
- `POST /api/auth/logout/`: logout
- `/api/usuarios/`
- `/api/empresas/`
- `/api/instituicoes/`
- `/api/estagios/`
- `/api/contratos/`
- `/api/contratos/{id}/upload-pdf/`
- `/api/contratos/{id}/analisar/`
- `/api/analises/`
- `/api/pendencias/`
- `/api/relatorios/`
- `/api/pareceres/`

## Filtros

Alguns endpoints aceitam filtros via query string:

```text
/api/contratos/?status=RECEBIDO
/api/contratos/?usuario=1&empresa=2
/api/contratos/?data_inicio=2026-01-01&data_fim=2026-12-31
/api/estagios/?tipo_estagio=OBRIGATORIO&curso=Direito
/api/pendencias/?severidade=ERRO&resolvida=false
```

## Testes

```powershell
$env:DJANGO_DEBUG = "True"
python manage.py check
python manage.py test
```
