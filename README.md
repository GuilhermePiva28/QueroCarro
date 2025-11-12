# 🚗 QueroCarro

> Encontre seu veículo ideal com preços da Tabela FIPE

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)](https://reactjs.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)

Uma aplicação web moderna e intuitiva para buscar veículos (carros, motos e caminhões) dentro do seu orçamento, utilizando dados oficiais da Tabela FIPE.

![QueroCarro Banner](logo-header.png)

## 📋 Índice

- [Sobre](#-sobre)
- [Funcionalidades](#-funcionalidades)
- [Demo](#-demo)
- [Tecnologias](#-tecnologias)
- [Como Usar](#-como-usar)
- [Capturas de Tela](#-capturas-de-tela)
- [API](#-api)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)
- [Autor](#-autor)

## 📖 Sobre

O **QueroCarro** é uma Single Page Application (SPA) desenvolvida para facilitar a busca de veículos baseada no orçamento do usuário. A aplicação integra-se com a API da Tabela FIPE para fornecer preços oficiais e atualizados, além de oferecer links diretos para as principais plataformas de venda de veículos do Brasil.

### 🎯 Problema Resolvido

Encontrar um veículo que se encaixe no seu orçamento pode ser trabalhoso. O QueroCarro resolve isso ao:
- Buscar automaticamente veículos dentro da sua faixa de preço (±R$5.000)
- Mostrar todos os anos disponíveis de cada modelo em um único card
- Fornecer links diretos para busca nas principais plataformas de venda

## ✨ Funcionalidades

### 🔍 Busca Inteligente
- **Por orçamento**: Defina seu valor e encontre veículos na faixa ±R$5.000
- **Por tipo**: Escolha entre carros, motos ou caminhões
- **Por marca e modelo**: Busca específica para resultados precisos
- **Por ano**: Filtre por intervalo de anos (de/até)

### 📊 Visualização Completa
- **Agrupamento por modelo**: Todos os anos de um modelo exibidos em um único card
- **Valores FIPE**: Preços oficiais para cada ano/combustível
- **Valor médio**: Cálculo automático da média de preços
- **Badges de combustível**: Identificação visual (Flex, Gasolina, Diesel, etc.)

### 🔗 Links Diretos
Acesso rápido para buscar o veículo em:
- 🔴 **Webmotors**
- 🟣 **OLX**
- 🟠 **iCarros**
- 🟡 **Mercado Livre**

### 🎨 Experiência do Usuário
- Interface responsiva e moderna
- Loading com barra de progresso
- Estados vazios informativos
- Cache de requisições para melhor performance
- Delays automáticos para respeitar rate limits da API

## 🌐 Demo

**Acesse agora:** [https://guilhermepiva28.github.io/QueroCarro/](https://guilhermepiva28.github.io/QueroCarro/)

## 🛠 Tecnologias

| Tecnologia | Descrição |
|-----------|-----------|
| ![React](https://img.shields.io/badge/-React-61DAFB?logo=react&logoColor=white) | Biblioteca JavaScript para interfaces |
| ![Tailwind CSS](https://img.shields.io/badge/-Tailwind%20CSS-38B2AC?logo=tailwind-css&logoColor=white) | Framework CSS utilitário |
| ![Babel](https://img.shields.io/badge/-Babel-F9DC3E?logo=babel&logoColor=black) | Transpilador JSX |
| ![FIPE API](https://img.shields.io/badge/-FIPE%20API-0066CC?logo=api&logoColor=white) | API oficial de preços de veículos |

### Arquitetura
- **Frontend**: React 18 (UMD build via CDN)
- **Estilização**: Tailwind CSS via CDN
- **Build**: Babel Standalone para transpilação in-browser
- **API**: REST API da Tabela FIPE (parallelum.com.br)

## 🚀 Como Usar

### Opção 1: Acesso Online
Acesse diretamente: [https://guilhermepiva28.github.io/QueroCarro/](https://guilhermepiva28.github.io/QueroCarro/)

### Opção 2: Executar Localmente

1. **Clone o repositório**
```bash
git clone https://github.com/GuilhermePiva28/QueroCarro.git
cd QueroCarro
```

2. **Abra o arquivo**
```bash
# Opção 1: Abrir diretamente no navegador
open index.html  # macOS
xdg-open index.html  # Linux
start index.html  # Windows

# Opção 2: Usar servidor local (recomendado)
python3 -m http.server 8000
# Acesse: http://localhost:8000
```

3. **Pronto!** 🎉
O site estará funcionando localmente.

## 📸 Capturas de Tela

### Tela Inicial
![Tela Inicial](docs/screenshot-home.png)

### Resultados da Busca
![Resultados](docs/screenshot-results.png)

### Card de Veículo
![Card](docs/screenshot-card.png)

## 🔌 API

A aplicação utiliza a **API FIPE** para obter dados de veículos:

### Base URL
```
https://parallelum.com.br/fipe/api/v1
```

### Endpoints Principais
```javascript
GET /{tipo}/marcas                              // Lista marcas
GET /{tipo}/marcas/{marca}/modelos              // Lista modelos
GET /{tipo}/marcas/{marca}/modelos/{modelo}/anos // Lista anos
GET /{tipo}/marcas/{marca}/modelos/{modelo}/anos/{ano} // Valor FIPE
```

**Tipos suportados**: `carros`, `motos`, `caminhoes`

### Rate Limiting
- A aplicação implementa cache local e delays (300-400ms) entre requisições
- Respeita os limites da API FIPE para evitar bloqueios

## 🎯 Modos de Busca

### 1. Busca Específica
- Selecione marca + modelo
- Busca todos os anos daquele modelo
- Mais rápida e precisa
- ✅ Recomendada quando você já sabe o que quer

### 2. Busca Ampla
- Não selecione marca/modelo (ou só marca)
- Busca até 15 marcas × 5 modelos × 3 anos
- Pode levar mais tempo
- ✅ Ideal para descobrir opções

## 🤝 Contribuindo

Contribuições são bem-vindas! Siga os passos:

1. Fork o projeto
2. Crie uma branch para sua feature
   ```bash
   git checkout -b feature/MinhaFeature
   ```
3. Commit suas mudanças
   ```bash
   git commit -m '✨ Adiciona MinhaFeature'
   ```
4. Push para a branch
   ```bash
   git push origin feature/MinhaFeature
   ```
5. Abra um Pull Request

### 💡 Ideias para Contribuir
- [ ] Adicionar mais plataformas de venda
- [ ] Implementar comparação entre modelos
- [ ] Adicionar gráficos de depreciação
- [ ] Modo escuro
- [ ] Exportar resultados em PDF
- [ ] Favoritar veículos
- [ ] Histórico de buscas

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👤 Autor

**Guilherme Piva**

- GitHub: [@GuilhermePiva28](https://github.com/GuilhermePiva28)
- Repositório: [QueroCarro](https://github.com/GuilhermePiva28/QueroCarro)

---

## 🙏 Agradecimentos

- [Tabela FIPE](https://veiculos.fipe.org.br/) - Dados oficiais de preços
- [Parallelum](https://parallelum.com.br/fipe) - API REST da FIPE
- [React](https://reactjs.org/) - Framework JavaScript
- [Tailwind CSS](https://tailwindcss.com/) - Framework CSS

---

<div align="center">

**⭐ Se este projeto te ajudou, considere dar uma estrela!**

Desenvolvido com ❤️ por [Guilherme Piva](https://github.com/GuilhermePiva28)

</div>
