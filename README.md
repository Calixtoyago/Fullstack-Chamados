# Contrato inicial — API de Chamados

## Recurso
- Nome: `chamados`
- Finalidade: registrar e acompanhar solicitações de suporte.

## Formato de dados
- Requisições e respostas: JSON

## Atributos
| Campo | Tipo | Obrigatório na criação? | Descrição | Exemplo |
|---|---|---|---|---|
| id | número | não | Identificador do chamado | 45 |
| usuario_nome | texto | sim | Identificar o usuário que solicitou o chamado | "Yago_Calixto" |
| titulo | texto | sim | Resumo do problema | "Impressora não funciona" |
| descricao | texto | sim | Detalhamento do problema | "Impressora não está imprimindo corretamente"
| prioridade | texto | sim |  Nível de prioridade | "Alta" |
| status | texto | não | Situação do chamado | "Aberto" |

### Status
| Tipos de status | Descrição |
|---|---|
| Aberto | Chamado ainda não iniciado |
| Em andamento | Chamado iniciado porém ainda não resolvido |
| Pendência | Esperando uma resposta do solicitante do chamado |
| Concluído | Chamado finalizado e concluído |

### Prioridades
| prioridade |
|---|
| Alta |
| Média |
| Baixa |

## Endpoints
| Operação | Método | URI | Finalidade | Status previstos |
|---|---|---|---|---|
| Listar chamados | GET | /chamados | Lista chamados | 200 |
| Buscar um chamado por id | GET | /chamados/{id} | Consulta um chamado | 200, 404 |
| Buscar um chamado por nome de usuário | GET | /chamados{usuario_nome} | Consulta os chamados de um usuário | 200, 404
| Criar um chamado | POST | /chamados | Cria um chamado | 201, 400 |
| Atualizar um chamado | PATCH | /chamados/{id} | Atualiza parcialmente um chamado | 200, 400, 404 |
| Deletar um chamado | DELETE | /chamados/{id} | Remove um chamado | 204, 404 |

## Exemplos
```
POST /chamados
Content-Type: application/json
{
    "usuario_nome": "Yago_Calixto",
    "titulo": "Sistema não inicia",
    "descricao": "O sistema fica carregando e não entra nunca",
    "prioridade": "Alta"
}
HTTP/1.1 201 Created
Content-Type: application/json
Location: /chamados/44
{
    "id": 44,
    "usuario_nome": "Yago_Calixto",
    "titulo": "Sistema não inicia",
    "descricao": "O sistema fica carregando e não entra nunca",
    "prioridade": "Alta",
    "status": "aberto"
}
```

```
GET /chamados/44
HTTP/1.1 200 OK
Content-Type: application/json
Location: /chamados/44
{
    "id": 44,
    "usuario_nome": "Yago_Calixto",
    "titulo": "Sistema não inicia",
    "descricao": "O sistema fica carregando e não entra nunca",
    "prioridade": "Alta",
    "status": "aberto"
}
```

```
GET /chamados/50
HTTP/1.1 404 Not Found
{
    "erro": "Chamado não existe",
    "detalhes": [
        {
        "codigo": 404,
        "campo": id,
        "mensagem": "O id selecionado não corresponde a nenhum chamado existente"
        }
    ]
}
```

```
POST /chamados
Content-Type: application/json
{
    "usuario_nome": "Yago_Calixto",
    "titulo": "Sistema não inicia",
    "prioridade": "Alta"
}
HTTP/1.1 400 Bad Request
{
    "erro": "Dado inválido",
    "detalhes": [
        {
            "codigo": 400,
            "campo": "descrição",
            "mensagem": "A descrição é obrigatória."
        }
    ]
}

```

## Decisões e dúvidas pendentes
- [Registrar decisões tomadas]
- [Registrar dúvidas que precisam de validação]
