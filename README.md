# Shodan-Cheatsheet
Alguns Filtros para Shodan

# Guia Completo da CLI do Shodan para Kali Linux

![Kali + Shodan](https://i.imgur.com/gAYa7d9.png)

> Um tutorial prático e direto ao ponto para dominar a interface de linha de comando (CLI) do Shodan no Kali Linux. Explore a internet de dispositivos conectados diretamente do seu terminal.

Este guia é focado em usuários do Kali Linux e aborda desde a instalação otimizada até comandos avançados de busca e análise, essenciais para profissionais de OSINT e cibersegurança.

---

## 📖 Tabela de Conteúdos

1.  [Por que usar a CLI do Shodan no Kali?](#-por-que-usar-a-cli-do-shodan-no-kali)
2.  [Pré-requisitos](#-pré-requisitos)
3.  [Instalação e Configuração](#-instalação-e-configuração)
4.  [Guia de Comandos Essenciais](#-guia-de-comandos-essenciais)
    * [Comandos de Informação](#comandos-de-informação)
    * [Pesquisa e Contagem (`search` e `count`)](#pesquisa-e-contagem-search-e-count)
    * [Análise de Alvos (`host`)](#análise-de-alvos-host)
    * [Estatísticas de Busca (`stats`)](#estatísticas-de-busca-stats)
    * [Scanner de Rede (`scan`)](#scanner-de-rede-scan)
5.  [Filtros de Busca Avançados](#-filtros-de-busca-avançados)
6.  [Dicas e Truques](#-dicas-e-truques)
7.  [Licença](#-licença)

---

## 🤔 Por que usar a CLI do Shodan no Kali?

O Kali Linux é a distribuição padrão para pentest e análise de segurança. A CLI do Shodan se integra perfeitamente a esse ambiente, permitindo:
* **Automação:** Crie scripts em Bash ou Python para automatizar buscas e coletar dados em massa.
* **Integração:** Combine a saída do Shodan com outras ferramentas do Kali, como Nmap, Metasploit ou Recon-ng.
* **Eficiência:** Obtenha resultados rápidos sem a necessidade de um navegador, mantendo seu fluxo de trabalho no terminal.

---

## ✅ Pré-requisitos

* **Kali Linux:** Este guia assume que você está usando uma versão atualizada do Kali.
* **Conta Shodan e Chave de API:** Você precisa da sua chave de API, que pode ser encontrada na página da sua conta em [shodan.io](https://account.shodan.io).

---

## 🛠️ Instalação e Configuração

O Kali Linux já vem com Python e `pip` pré-instalados, o que simplifica o processo.

### 1. Instale a CLI do Shodan

Abra seu terminal e execute o comando:
```bash
sudo pip install shodan
