# Nossa Corretora · Portal (front)

Portal interno da Nossa Corretora para as vendas de planos de saúde
**CDL Mossoró × Unimed**: Pipeline comercial, Implantação em 5 etapas
(Cadastro → Pessoas → Conferência → Implantação → Ativado), clientes,
CDLs, repasses, comissões, usuários e integrações.

No ar em **https://portal.nossaapp.com.br** (Cloudflare Pages).
Cada envio para a branch `main` publica sozinho, em cerca de 1 minuto.

## Repositórios do sistema

| Repositório | O que é | Onde fica no ar |
|---|---|---|
| `portal` (este) | Portal e páginas públicas do cliente | Cloudflare Pages · portal.nossaapp.com.br |
| `saude` | Simulador de planos para o cliente | GitHub Pages · simulador.nossaapp.com.br |
| `nossa-backend` | Funções do Supabase, SQL e script do Google | Supabase |

## Arquivos

| Arquivo | Quem usa | Para quê |
|---|---|---|
| `index.html` | equipe (login) | o portal inteiro |
| `formulario-cliente.html` | cliente (link por vida) | endereço, questionário de saúde e assinatura da ficha de inclusão |
| `documentos-cliente.html` | cliente (link da empresa ou do titular) | envio dos documentos |
| `unimed-conferencia.html` | atendente da Unimed (link com validade) | conferir e baixar todos os arquivos da implantação |
| `termos-de-uso.html` | público | termos de uso e participação |
| `modelos/` | portal | modelos oficiais em PDF (Proposta PME III e ficha de inclusão) preenchidos pelo sistema |
| `CNAME` | GitHub Pages (antigo) | domínio; não é usado pelo Cloudflare |

As páginas não têm etapa de build: são HTML com o JavaScript dentro.
Bibliotecas externas (planilha e PDF) vêm do cdnjs.

## Onde ficam os dados

Tudo fica no **Supabase** (login, banco criptografado, arquivos e funções).
O código do servidor está no repositório `nossa-backend`. A chave que aparece
no `index.html` é a chave **pública** do Supabase, feita para ficar no
navegador; a chave de serviço e as das integrações ficam só nos segredos do
Supabase.

## Papéis de acesso

- **Administrador**: tudo.
- **Atendente**: faz a implantação inteira; não apaga, não cria usuários e não vê comissões.
- **Vendedor parceiro**: só Pipeline e as vendas dele (o servidor entrega só os dados dele).

## Integrações

- **Autentique**: assinatura eletrônica (contrato de associação, fichas de inclusão, Proposta PME III).
- **Google (Gmail)**: e-mail da implantação para a Unimed.
- **SunChat**: o Pipeline comercial espelhado no pipeline da SunChat.
