# Guia Completo da CLI do Shodan para Kali Linux

[![Status](https://img.shields.io/badge/status-ready-brightgreen.svg)](https://shodan.io)
[![License](https://img.shields.io/badge/license-educational-lightgrey.svg)]

Um tutorial prático e direto ao ponto para dominar a interface de linha de comando (CLI) do **Shodan** no **Kali Linux**. Focado em instalação otimizada, comandos essenciais, buscas avançadas e integração com ferramentas do Kali. Ideal para profissionais de OSINT e cibersegurança.

---

## 📖 Tabela de Conteúdos
- [Por que usar a CLI do Shodan no Kali?](#-por-que-usar-a-cli-do-shodan-no-kali)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#-instalação-e-configuração)
  - [1. Instale a CLI do Shodan](#1-instea-a-cli-do-shodan)
  - [2. Configure sua Chave de API](#2-configure-sua-chave-de-api)
  - [3. Verifique a Instalação](#3-verifique-a-instalação)
- [Guia de Comandos Essenciais](#-guia-de-comandos-essenciais)
  - [Comandos de Informação](#comandos-de-informação)
  - [Pesquisa e Contagem (search e count)](#pesquisa-e-contagem-search-e-count)
  - [Análise de Alvos (host)](#análise-de-alvos-host)
  - [Estatísticas de Busca (stats)](#estatísticas-de-busca-stats)
  - [Scanner de Rede (scan)](#scanner-de-rede-scan)
- [Filtros de Busca Avançados](#-filtros-de-busca-avançados)
- [Dicas e Truques](#-dicas-e-truques)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)

---

## 🤔 Por que usar a CLI do Shodan no Kali?
Kali é a distro padrão pra pentest. A CLI do Shodan permite:
- **Automação:** scripts em Bash/Python para buscas em massa.  
- **Integração:** junte saída do Shodan com Nmap, Metasploit, Recon-ng.  
- **Eficiência:** tudo no terminal, rápido e sem navegador.

---

## ✅ Pré-requisitos
- Kali Linux atualizado.  
- Conta Shodan e **chave de API** (pega em `https://shodan.io` → sua conta).

---

## 🛠️ Instalação e Configuração

### 1. Instale a CLI do Shodan
Abra o terminal:
```bash
sudo pip install shodan
```

> Dica rápida: prefira `pip` associado ao Python 3 do sistema (`python3 -m pip`) se houver múltiplas versões do Python.

### 2. Configure sua Chave de API
Substitua `SUA_CHAVE_DE_API_AQUI` pela sua chave:
```bash
shodan init SUA_CHAVE_DE_API_AQUI
```
Saída esperada: `Successfully initialized.`

### 3. Verifique a Instalação
```bash
shodan myip
```
Retorna seu IP público.

---

## 🚀 Guia de Comandos Essenciais

### Comandos de Informação
- `shodan info` — informações da conta (créditos, limites).
```bash
shodan info
```
- `shodan myip` — mostra seu IP público.
```bash
shodan myip
```

### Pesquisa e Contagem (search e count)
- `shodan count [filtros]` — conta resultados rápido.
```bash
# Contar quantos servidores Apache existem no Brasil
shodan count apache country:BR
```
- `shodan search [filtros]` — busca e retorna IPs/banners.
```bash
# Buscar webcams no Brasil e salvar IPs
shodan search webcamxp country:BR --fields ip_str > webcams.txt
```

### Análise de Alvos (host)
- `shodan host [IP]` — resumo de um alvo (portas, serviços, CVEs, geolocalização).
```bash
shodan host 8.8.8.8
```

### Estatísticas de Busca (stats)
- `shodan stats [filtros]` — estatísticas agrupadas.
```bash
# Top 10 organizações com mais nginx
shodan stats --facets org:10 nginx

# Top 5 portas em servidores com RDP (3389)
shodan stats --facets port:5 port:3389
```

### Scanner de Rede (scan)
- Submeter scan (requer créditos):
```bash
shodan scan submit 8.8.8.8
```
- Ver status do scan:
```bash
shodan scan status ID_DO_SCAN
```

---

## 🔍 Filtros de Busca Avançados

| Filtro         | Descrição                                | Exemplo                         |
|----------------|------------------------------------------|---------------------------------|
| `port`         | Porta específica aberta                  | `port:3389`                     |
| `org`          | Organização / provedor                    | `org:"Google LLC"`              |
| `country`      | País (código ISO 2 letras)               | `country:JP`                    |
| `city`         | Cidade                                   | `city:"Tokyo"`                  |
| `os`           | Sistema operacional                      | `os:"windows server 2019"`      |
| `product`      | Produto de software                      | `product:"microsoft iis"`       |
| `vuln`         | CVE específica                           | `vuln:CVE-2020-0796`            |
| `hostname`     | Texto no hostname                        | `hostname:.gov.br`              |
| `has_screenshot` | Dispositivos com screenshot            | `has_screenshot:true port:5900` |

Exemplo combinando filtros:
```bash
shodan search apache country:BR port:80 org:"Empresa X" --fields ip_str,port,org --limit 50
```

---

## 💡 Dicas e Truques
- **Salvar saída:** use `>` para gravar em arquivo.  
- **Campos customizados:** `--fields` para escolher colunas (ex.: `ip_str,port,org,hostname`).  
```bash
shodan search microsoft-iis --fields ip_str,port,org
```
- **Pipeline para Nmap:** passe IPs direto com `xargs`.
```bash
# Escanear 100 primeiros IPs com porta 22 no Brasil
shodan search port:22 country:BR --fields ip_str --limit 100 | xargs -I{} nmap -sV {}
```
- **Limites e ética:** scans podem requerer créditos e devem seguir regras legais/ética do seu contexto.

---

## 🤝 Contribuindo
Quer melhorar esse guia? Abra um PR com:
- `README.md` atualizado (este arquivo).
- Exemplos adicionais (scripts, automações).
- Testes mínimos ou instruções de uso.

Modelo de PR:
1. Fork.
2. Crie branch `feature/seu-topico`.
3. Commit e push.
4. Abra PR com descrição objetiva.

---

## 📜 Licença
Conteúdo para fins educacionais. Não é uma licença de software.

