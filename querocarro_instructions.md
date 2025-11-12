# 📋 INSTRUÇÕES COMPLETAS PARA CRIAÇÃO DO SITE QUEROCARRO

## 🎯 VISÃO GERAL DO PROJETO

### Descrição
Site responsivo para busca de veículos com integração à API da Tabela FIPE, permitindo que usuários encontrem carros, motos e caminhões dentro de seu orçamento e acessem links diretos para plataformas de venda (Webmotors, OLX, iCarros, Mercado Livre).

### Diferencial Principal
O site oferece duas modalidades de busca:
1. **Busca Específica**: Usuário seleciona marca e modelo exatos
2. **Busca Ampla**: Usuário informa apenas orçamento e tipo, recebendo TODOS os veículos na faixa de preço (±R$ 5.000)

---

## 🛠️ STACK TECNOLÓGICA

### Tecnologias Obrigatórias
- **Framework**: React 18+ com Hooks
- **Estilização**: Tailwind CSS (apenas classes core - sem compilador)
- **Ícones**: lucide-react
- **API**: Tabela FIPE - https://parallelum.com.br/fipe/api/v1/
- **Tipo**: Single Page Application (SPA) - React Artifact

### Bibliotecas React Disponíveis
```javascript
import { useState, useEffect } from 'react';
import { Car, Bike, Truck, Search, ExternalLink, DollarSign, Calendar, Filter, Info } from 'lucide-react';
```

---

## 🎨 DESIGN SYSTEM

### Paleta de Cores

#### Cores Principais
```css
--primary: #3B82F6        /* Azul vibrante - botões primários */
--primary-hover: #2563EB  /* Azul escuro - hover */
--secondary: #10B981      /* Verde - valores, confirmações */
--background: #F9FAFB     /* Cinza muito claro - fundo geral */
--card-bg: #FFFFFF        /* Branco - cards */
```

#### Cores de Texto
```css
--text-primary: #1F2937   /* Cinza escuro - títulos */
--text-secondary: #6B7280 /* Cinza médio - descrições */
--text-muted: #9CA3AF     /* Cinza claro - hints */
```

#### Cores de Borda e Sombras
```css
--border: #E5E7EB         /* Cinza claro */
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05)
--shadow-md: 0 4px 6px rgba(0,0,0,0.1)
--shadow-lg: 0 10px 15px rgba(0,0,0,0.1)
--shadow-xl: 0 20px 25px rgba(0,0,0,0.15)
```

#### Cores das Plataformas
```css
--webmotors: #DC2626     /* Vermelho */
--olx: #7C3AED           /* Roxo */
--icarros: #F97316       /* Laranja */
--mercadolivre: #EAB308  /* Amarelo */
```

#### Cores de Combustível (Badges)
```css
--gasolina: #E5E7EB      /* Cinza */
--flex: #D1FAE5          /* Verde claro */
--diesel: #FEF3C7        /* Amarelo claro */
--eletrico: #DBEAFE      /* Azul claro */
--hibrido: #E9D5FF       /* Roxo claro */
```

### Tipografia

#### Tamanhos de Fonte
```css
text-xs: 0.75rem    /* 12px - labels pequenos */
text-sm: 0.875rem   /* 14px - texto secundário */
text-base: 1rem     /* 16px - texto padrão */
text-lg: 1.125rem   /* 18px - subtítulos */
text-xl: 1.25rem    /* 20px - títulos de seção */
text-2xl: 1.5rem    /* 24px - preços */
text-3xl: 1.875rem  /* 30px - títulos principais */
text-4xl: 2.25rem   /* 36px - logo/hero */
```

#### Pesos de Fonte
```css
font-normal: 400    /* Texto padrão */
font-medium: 500    /* Labels, botões */
font-semibold: 600  /* Subtítulos */
font-bold: 700      /* Títulos, preços */
font-extrabold: 800 /* Logo, destaque máximo */
```

### Espaçamentos

#### Padding/Margin
```css
p-2: 0.5rem    /* 8px */
p-4: 1rem      /* 16px */
p-6: 1.5rem    /* 24px */
p-8: 2rem      /* 32px */
p-12: 3rem     /* 48px */
```

#### Gaps (Grid/Flex)
```css
gap-2: 0.5rem  /* 8px */
gap-4: 1rem    /* 16px */
gap-6: 1.5rem  /* 24px */
gap-8: 2rem    /* 32px */
```

### Bordas e Sombras

#### Border Radius
```css
rounded: 0.25rem      /* 4px - elementos pequenos */
rounded-md: 0.375rem  /* 6px - inputs */
rounded-lg: 0.5rem    /* 8px - botões */
rounded-xl: 0.75rem   /* 12px - cards */
rounded-2xl: 1rem     /* 16px - card principal */
rounded-full: 9999px  /* Circular - badges */
```

#### Box Shadow (Classes Tailwind)
```css
shadow-sm: sombra pequena
shadow-md: sombra média
shadow-lg: sombra grande
shadow-xl: sombra extra grande
shadow-2xl: sombra máxima
```

### Animações e Transições

```css
transition-all duration-300      /* Padrão - transição suave */
hover:scale-105                  /* Hover - crescer 5% */
hover:-translate-y-1             /* Hover - elevar 4px */
hover:shadow-xl                  /* Hover - aumentar sombra */
```

---

## 🏗️ ESTRUTURA DO SITE

### Layout Geral
```
┌─────────────────────────────────────────────────────────┐
│                    HEADER (fixo)                        │
│   Logo QueroCarro + Tagline                            │
│   Gradiente azul                                        │
└─────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────┐
│                   MAIN CONTENT                          │
│  ┌─────────────────────────────────────────────────┐   │
│  │        FILTROS (Card branco)                    │   │
│  │  - Tipo de veículo                              │   │
│  │  - Orçamento (slider)                           │   │
│  │  - Marca (opcional)                             │   │
│  │  - Modelo (opcional)                            │   │
│  │  - Ano (opcional)                               │   │
│  │  - Botão BUSCAR                                 │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │        RESULTADOS (Grid de cards)               │   │
│  │  [Card 1] [Card 2] [Card 3]                     │   │
│  │  [Card 4] [Card 5] [Card 6]                     │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────┐
│                    FOOTER (opcional)                    │
│   Créditos + Links úteis                               │
└─────────────────────────────────────────────────────────┘
```

---

## 📐 COMPONENTES DETALHADOS

### 1. HEADER

#### Especificações Visuais
```jsx
// Classes Tailwind
className="bg-gradient-to-r from-blue-500 to-blue-600 text-white shadow-lg"
```

#### Estrutura
```
┌──────────────────────────────────────────────┐
│  [Logo QueroCarro.png]                       │
│  Encontre seu veículo ideal com preços       │
│  da Tabela FIPE                              │
└──────────────────────────────────────────────┘
```

#### Implementação
```jsx
<header className="bg-gradient-to-r from-blue-500 to-blue-600 text-white shadow-lg">
  <div className="container mx-auto px-4 py-6">
    <div className="flex items-center justify-center gap-4">
      <img 
        src="QueroCarro(1).png" 
        alt="QueroCarro Logo" 
        className="h-12 md:h-16"
      />
    </div>
    <p className="text-center text-sm md:text-base mt-2 opacity-90">
      Encontre seu veículo ideal com preços da Tabela FIPE
    </p>
  </div>
</header>
```

#### Responsividade
- Mobile: Logo h-12 (48px), texto text-sm
- Desktop: Logo h-16 (64px), texto text-base

---

### 2. CARD DE FILTROS

#### Especificações Visuais
```jsx
className="bg-white rounded-2xl shadow-xl p-8 max-w-4xl mx-auto"
```

#### Estrutura Completa
```
┌────────────────────────────────────────────────┐
│  🚗 Que tipo de veículo você procura?          │
│  [🚗 Carros] [🏍️ Motos] [🚚 Caminhões]        │
│                                                 │
│  💰 Qual seu orçamento?                        │
│  [━━━━━━━○━━━] R$ 50.000                      │
│  Buscando entre R$ 45.000 e R$ 55.000         │
│                                                 │
│  🏭 Marca (opcional)                           │
│  [Selecione uma marca... ▼]                    │
│                                                 │
│  🚘 Modelo (opcional)                          │
│  [Todos os modelos ▼]                          │
│                                                 │
│  📅 Ano do veículo (opcional)                  │
│  [De: Todos ▼]  [Até: Todos ▼]                │
│                                                 │
│       [🔍 BUSCAR VEÍCULOS]                     │
└────────────────────────────────────────────────┘
```

#### 2.A) FILTRO: Tipo de Veículo

**Layout**
```jsx
<div className="space-y-3">
  <label className="flex items-center gap-2 text-lg font-semibold text-gray-800">
    <Filter className="w-5 h-5" />
    Que tipo de veículo você procura?
  </label>
  
  <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
    {/* Botão Carros */}
    <button
      className={`flex items-center justify-center gap-3 p-4 rounded-lg font-semibold 
        transition-all duration-300 ${
          tipoVeiculo === 'carros' 
            ? 'bg-blue-500 text-white shadow-lg scale-105' 
            : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
        }`}
      onClick={() => setTipoVeiculo('carros')}
    >
      <Car className="w-6 h-6" />
      Carros
    </button>
    
    {/* Botão Motos */}
    <button
      className={`flex items-center justify-center gap-3 p-4 rounded-lg font-semibold 
        transition-all duration-300 ${
          tipoVeiculo === 'motos' 
            ? 'bg-blue-500 text-white shadow-lg scale-105' 
            : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
        }`}
      onClick={() => setTipoVeiculo('motos')}
    >
      <Bike className="w-6 h-6" />
      Motos
    </button>
    
    {/* Botão Caminhões */}
    <button
      className={`flex items-center justify-center gap-3 p-4 rounded-lg font-semibold 
        transition-all duration-300 ${
          tipoVeiculo === 'caminhoes' 
            ? 'bg-blue-500 text-white shadow-lg scale-105' 
            : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
        }`}
      onClick={() => setTipoVeiculo('caminhoes')}
    >
      <Truck className="w-6 h-6" />
      Caminhões
    </button>
  </div>
</div>
```

**Estados React**
```javascript
const [tipoVeiculo, setTipoVeiculo] = useState('carros');
```

**Comportamento**
- Ao clicar, atualiza estado e recarrega marcas
- Apenas um tipo selecionado por vez
- Efeito visual de seleção (cor azul + escala)

---

#### 2.B) FILTRO: Orçamento (Slider)

**Layout**
```jsx
<div className="space-y-3">
  <label className="flex items-center gap-2 text-lg font-semibold text-gray-800">
    <DollarSign className="w-5 h-5" />
    Qual seu orçamento?
  </label>
  
  <div className="space-y-2">
    <input
      type="range"
      min="10000"
      max="300000"
      step="5000"
      value={orcamento}
      onChange={(e) => setOrcamento(Number(e.target.value))}
      className="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-blue-500"
    />
    
    <div className="text-center">
      <div className="text-3xl font-bold text-blue-600">
        {formatarPreco(orcamento)}
      </div>
      <div className="text-sm text-gray-500 mt-1">
        Buscando entre {formatarPreco(orcamento - 5000)} e {formatarPreco(orcamento + 5000)}
      </div>
    </div>
  </div>
</div>
```

**Função Auxiliar**
```javascript
function formatarPreco(valor) {
  return new Intl.NumberFormat('pt-BR', {
    style: 'currency',
    currency: 'BRL',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(valor);
}
```

**Estados React**
```javascript
const [orcamento, setOrcamento] = useState(50000);
```

**Comportamento**
- Faixa: R$ 10.000 a R$ 300.000
- Incrementos de R$ 5.000
- Atualização em tempo real
- Exibe faixa de busca (±R$ 5.000)

---

#### 2.C) FILTRO: Marca

**Layout**
```jsx
<div className="space-y-3">
  <label className="flex items-center gap-2 text-base font-semibold text-gray-800">
    🏭 Marca (opcional)
  </label>
  
  <select
    value={marcaSelecionada}
    onChange={(e) => {
      setMarcaSelecionada(e.target.value);
      setModeloSelecionado(''); // Reset modelo
    }}
    className="w-full px-4 py-3 border-2 border-gray-200 rounded-lg 
      focus:border-blue-500 focus:ring-2 focus:ring-blue-200 
      transition-all text-base"
  >
    <option value="">Todas as marcas</option>
    {marcas.map(marca => (
      <option key={marca.codigo} value={marca.codigo}>
        {marca.nome}
      </option>
    ))}
  </select>
</div>
```

**Estados React**
```javascript
const [marcas, setMarcas] = useState([]);
const [marcaSelecionada, setMarcaSelecionada] = useState('');
```

**Comportamento**
- Carrega marcas ao selecionar tipo de veículo
- Opção "Todas as marcas" para busca ampla
- Ao mudar marca, reseta modelo selecionado

---

#### 2.D) FILTRO: Modelo

**Layout**
```jsx
<div className="space-y-3">
  <label className="flex items-center gap-2 text-base font-semibold text-gray-800">
    🚘 Modelo (opcional)
  </label>
  
  <select
    value={modeloSelecionado}
    onChange={(e) => setModeloSelecionado(e.target.value)}
    disabled={!marcaSelecionada}
    className="w-full px-4 py-3 border-2 border-gray-200 rounded-lg 
      focus:border-blue-500 focus:ring-2 focus:ring-blue-200 
      transition-all text-base disabled:bg-gray-100 disabled:cursor-not-allowed"
  >
    <option value="">
      {marcaSelecionada ? 'Todos os modelos' : 'Primeiro selecione uma marca...'}
    </option>
    {modelos.map(modelo => (
      <option key={modelo.codigo} value={modelo.codigo}>
        {modelo.nome}
      </option>
    ))}
  </select>
</div>
```

**Estados React**
```javascript
const [modelos, setModelos] = useState([]);
const [modeloSelecionado, setModeloSelecionado] = useState('');
```

**Comportamento**
- Desabilitado se "Todas as marcas" estiver selecionado
- Carrega modelos ao selecionar marca específica
- Placeholder muda baseado no estado

---

#### 2.E) FILTRO: Faixa de Ano

**Layout**
```jsx
<div className="space-y-3">
  <label className="flex items-center gap-2 text-base font-semibold text-gray-800">
    <Calendar className="w-5 h-5" />
    Ano do veículo (opcional)
  </label>
  
  <div className="grid grid-cols-2 gap-4">
    <div>
      <label className="text-sm text-gray-600 mb-1 block">De:</label>
      <select
        value={anoInicio}
        onChange={(e) => setAnoInicio(e.target.value)}
        className="w-full px-4 py-3 border-2 border-gray-200 rounded-lg 
          focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
      >
        <option value="">Todos</option>
        {gerarAnos().map(ano => (
          <option key={ano} value={ano}>{ano}</option>
        ))}
      </select>
    </div>
    
    <div>
      <label className="text-sm text-gray-600 mb-1 block">Até:</label>
      <select
        value={anoFim}
        onChange={(e) => setAnoFim(e.target.value)}
        className="w-full px-4 py-3 border-2 border-gray-200 rounded-lg 
          focus:border-blue-500 focus:ring-2 focus:ring-blue-200 transition-all"
      >
        <option value="">Todos</option>
        {gerarAnos().map(ano => (
          <option key={ano} value={ano}>{ano}</option>
        ))}
      </select>
    </div>
  </div>
</div>
```

**Função Auxiliar**
```javascript
function gerarAnos() {
  const anoAtual = new Date().getFullYear();
  const anos = [];
  for (let ano = anoAtual; ano >= 1980; ano--) {
    anos.push(ano);
  }
  anos.unshift('0 KM'); // Código 32000 na API
  return anos;
}
```

**Estados React**
```javascript
const [anoInicio, setAnoInicio] = useState('');
const [anoFim, setAnoFim] = useState('');
```

---

#### 2.F) BOTÃO DE BUSCA

**Layout**
```jsx
<button
  onClick={buscarVeiculos}
  disabled={loading || !tipoVeiculo}
  className="w-full md:w-auto px-8 py-4 bg-blue-500 text-white font-bold 
    text-lg rounded-lg shadow-lg hover:bg-blue-600 hover:shadow-xl 
    hover:scale-105 transition-all duration-300 disabled:opacity-50 
    disabled:cursor-not-allowed disabled:hover:scale-100 
    flex items-center justify-center gap-3 mx-auto"
>
  {loading ? (
    <>
      <div className="animate-spin rounded-full h-5 w-5 border-2 border-white border-t-transparent" />
      BUSCANDO...
    </>
  ) : (
    <>
      <Search className="w-6 h-6" />
      BUSCAR VEÍCULOS
    </>
  )}
</button>
```

**Estados React**
```javascript
const [loading, setLoading] = useState(false);
```

**Comportamento**
- Desabilitado durante carregamento
- Desabilitado se tipo não selecionado
- Animação de loading (spinner)
- Efeito hover apenas quando habilitado

---

### 3. SEÇÃO DE RESULTADOS

#### Estrutura do Container
```jsx
{buscaRealizada && (
  <div className="mt-12">
    <div className="max-w-6xl mx-auto px-4">
      {/* Cabeçalho dos Resultados */}
      <div className="mb-8 text-center">
        <h2 className="text-3xl font-bold text-gray-800 mb-2">
          {modeloSelecionado 
            ? '📊 Resultados Específicos' 
            : '📊 Veículos na sua Faixa de Orçamento'
          }
        </h2>
        <p className="text-gray-600">
          {resultados.length > 0 
            ? `✅ ${resultados.length} veículos encontrados` 
            : '😕 Nenhum veículo encontrado'
          }
        </p>
      </div>

      {/* Grid de Resultados */}
      {resultados.length > 0 ? (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {resultados.map((veiculo, index) => (
            <ResultadoCard key={index} veiculo={veiculo} />
          ))}
        </div>
      ) : (
        <EmptyState />
      )}
    </div>
  </div>
)}
```

---

### 4. CARD DE RESULTADO (Componente Individual)

#### Especificações Visuais
```jsx
className="bg-white rounded-xl shadow-md hover:shadow-xl hover:-translate-y-1 
  transition-all duration-300 p-6 border border-gray-100"
```

#### Estrutura Completa
```
┌────────────────────────────────┐
│  🚗 [Ícone tipo veículo]       │
│                                 │
│  Ford Ka SE 1.0 Flex           │
│  (text-xl font-bold)           │
│                                 │
│  2018 • Gasolina               │
│  (text-gray-600)               │
│                                 │
│  ─────────────────             │
│                                 │
│  Valor FIPE                    │
│  R$ 48.500                     │
│  (text-2xl text-green-600)     │
│                                 │
│  Código: 003128-3              │
│  (text-xs text-gray-400)       │
│                                 │
│  ── Buscar em: ──              │
│                                 │
│  [Webmotors] [OLX]             │
│  [iCarros]   [Merc. Livre]     │
└────────────────────────────────┘
```

#### Implementação Completa
```jsx
function ResultadoCard({ veiculo }) {
  const valorNumerico = converterPrecoFipe(veiculo.Valor);
  
  return (
    <div className="bg-white rounded-xl shadow-md hover:shadow-xl 
      hover:-translate-y-1 transition-all duration-300 p-6 
      border border-gray-100">
      
      {/* Ícone do Tipo */}
      <div className="flex justify-center mb-4">
        <div className="bg-blue-50 p-3 rounded-full">
          <Car className="w-8 h-8 text-blue-500" />
        </div>
      </div>

      {/* Título - Modelo */}
      <h3 className="text-xl font-bold text-gray-800 mb-2 text-center">
        {veiculo.Modelo}
      </h3>

      {/* Ano e Combustível */}
      <div className="flex items-center justify-center gap-2 mb-4">
        <span className="text-gray-600">{veiculo.AnoModelo}</span>
        <span className="text-gray-400">•</span>
        <span className={`px-2 py-1 rounded-full text-xs font-medium ${
          getBadgeCombustivel(veiculo.Combustivel)
        }`}>
          {veiculo.Combustivel}
        </span>
      </div>

      {/* Divider */}
      <div className="border-t border-gray-200 my-4" />

      {/* Preço FIPE */}
      <div className="text-center mb-4">
        <div className="text-sm text-gray-500 mb-1">Valor FIPE</div>
        <div className="text-2xl font-bold text-green-600">
          {veiculo.Valor}
        </div>
        <div className="text-xs text-gray-400 mt-1">
          Código: {veiculo.CodigoFipe}
        </div>
      </div>

      {/* Divider */}
      <div className="border-t border-gray-200 my-4" />

      {/* Botões das Plataformas */}
      <div className="space-y-3">
        <div className="text-center text-sm font-semibold text-gray-600 mb-2">
          Buscar em:
        </div>
        
        <div className="grid grid-cols-2 gap-2">
          <BotaoPlataforma 
            nome="Webmotors"
            cor="bg-red-500 hover:bg-red-600"
            url={gerarURL('webmotors', veiculo.Marca, veiculo.Modelo, valorNumerico)}
          />
          
          <BotaoPlataforma 
            nome="OLX"
            cor="bg-purple-500 hover:bg-purple-600"
            url={gerarURL('olx', veiculo.Marca, veiculo.Modelo, valorNumerico)}
          />
          
          <BotaoPlataforma 
            nome="iCarros"
            cor="bg-orange-500 hover:bg-orange-600"
            url={gerarURL('icarros', veiculo.Marca, veiculo.Modelo, valorNumerico)}
          />
          
          <BotaoPlataforma 
            nome="Merc. Livre"
            cor="bg-yellow-500 hover:bg-yellow-600"
            url={gerarURL('mercadolivre', veiculo.Marca, veiculo.Modelo, valorNumerico)}
          />
        </div>
      </div>
    </div>
  );
}
```

#### Funções Auxiliares do Card

**Badge de Combustível**
```javascript
function getBadgeCombustivel(combustivel) {
  const badges = {
    'Gasolina': 'bg-gray-200 text-gray-700',
    'Flex': 'bg-green-200 text-green-700',
    'Diesel': 'bg-yellow-200 text-yellow-700',
    'Elétrico': 'bg-blue-200 text-blue-700',
    'Híbrido': 'bg-purple-200 text-purple-700',
    'Álcool': 'bg-green-200 text-green-700'
  };
  return badges[combustivel] || 'bg-gray-200 text-gray-700';
}
```

---

### 5. BOTÃO DE PLATAFORMA (Componente Reutilizável)

```jsx
function BotaoPlataforma({ nome, cor, url }) {
  return (
    <a
      href={url}
      target="_blank"
      rel="noopener noreferrer"
      className={`${cor} text-white px-3 py-2 rounded-lg text-xs md:text-sm 
        font-medium transition-all duration-300 flex items-center 
        justify-center gap-2 hover:scale-105 shadow-sm hover:shadow-md`}
    >
      <span>{nome}</span>
      <ExternalLink className="w-3 h-3" />
    </a>
  );
}
```

---

### 6. ESTADOS DE INTERFACE

#### Loading Spinner
```jsx
function LoadingSpinner() {
  return (
    <div className="flex flex-col items-center justify-center py-12">
      <div className="animate-spin rounded-full h-16 w-16 border-4 border-blue-500 border-t-transparent" />
      <p className="mt-4 text-gray-600 font-medium">🔍 Buscando veículos...</p>
      <p className="text-sm text-gray-500 mt-2">Isso pode levar alguns segundos</p>
    </div>
  );
}
```

#### Empty State (Sem Resultados)
```jsx
function EmptyState() {
  return (
    <div className="text-center py-12 px-4">
      <div className="text-6xl mb-4">😕</div>
      <h3 className="text-2xl font-bold text-gray-800 mb-2">
        Nenhum veículo encontrado
      </h3>
      <p className="text-gray-600 mb-6">
        Não encontramos veículos nessa faixa de preço.
        <br />
        Tente aumentar o orçamento ou ajustar os filtros!
      </p>
      <div className="bg-blue-50 border border-blue-200 rounded-lg p-4 max-w-md mx-auto">
        <p className="text-sm text-blue-800">
          💡 <strong>Dica:</strong> Deixe marca e modelo em branco para ver 
          TODOS os veículos disponíveis na sua faixa de orçamento!
        </p>
      </div>
    </div>
  );
}
```

#### Estado Inicial (Antes de Buscar)
```jsx
function EstadoInicial() {
  return (
    <div className="text-center py-12 px-4">
      <div className="text-6xl mb-4">🎯</div>
      <h3 className="text-2xl font-bold text-gray-800 mb-2">
        Pronto para encontrar seu veículo ideal?
      </h3>
      <p className="text-gray-600 mb-6">
        Selecione o tipo de veículo e seu orçamento acima.
      </p>
      <div className="bg-gradient-to-r from-blue-50 to-purple-50 border border-blue-200 
        rounded-lg p-6 max-w-lg mx-auto">
        <p className="text-sm text-gray-700 mb-3">
          <strong>📍 Como funciona:</strong>
        </p>
        <ul className="text-left text-sm text-gray-600 space-y-2">
          <li>✓ Busca específica: Selecione marca e modelo exatos</li>
          <li>✓ Busca ampla: Deixe marca/modelo em branco</li>
          <li>✓ Comparamos com a Tabela FIPE oficial</li>
          <li>✓ Links diretos para anúncios reais</li>
        </ul>
      </div>
    </div>
  );
}
```

#### Barra de Progresso (Para Busca Ampla)
```jsx
function BarraProgresso({ atual, total, mensagem }) {
  const porcentagem = total > 0 ? (atual / total) * 100 : 0;
  
  return (
    <div className="max-w-md mx-auto py-8">
      <p className="text-center text-gray-700 font-medium mb-4">{mensagem}</p>
      
      <div className="w-full bg-gray-200 rounded-full h-3 overflow-hidden">
        <div 
          className="bg-blue-500 h-full transition-all duration-300 rounded-full"
          style={{ width: `${porcentagem}%` }}
        />
      </div>
      
      <p className="text-center text-sm text-gray-500 mt-2">
        {atual} de {total} marcas analisadas
      </p>
    </div>
  );
}
```

---

## 🔌 INTEGRAÇÃO COM API FIPE

### Endpoints da API

```javascript
const BASE_URL = 'https://parallelum.com.br/fipe/api/v1';

// Estrutura de endpoints por tipo
const ENDPOINTS = {
  carros: {
    marcas: `${BASE_URL}/carros/marcas`,
    modelos: (codigoMarca) => `${BASE_URL}/carros/marcas/${codigoMarca}/modelos`,
    anos: (codigoMarca, codigoModelo) => 
      `${BASE_URL}/carros/marcas/${codigoMarca}/modelos/${codigoModelo}/anos`,
    valor: (codigoMarca, codigoModelo, codigoAno) => 
      `${BASE_URL}/carros/marcas/${codigoMarca}/modelos/${codigoModelo}/anos/${codigoAno}`
  },
  motos: {
    marcas: `${BASE_URL}/motos/marcas`,
    modelos: (codigoMarca) => `${BASE_URL}/motos/marcas/${codigoMarca}/modelos`,
    anos: (codigoMarca, codigoModelo) => 
      `${BASE_URL}/motos/marcas/${codigoMarca}/modelos/${codigoModelo}/anos`,
    valor: (codigoMarca, codigoModelo, codigoAno) => 
      `${BASE_URL}/motos/marcas/${codigoMarca}/modelos/${codigoModelo}/anos/${codigoAno}`
  },
  caminhoes: {
    marcas: `${BASE_URL}/caminhoes/marcas`,
    modelos: (codigoMarca) => `${BASE_URL}/caminhoes/marcas/${codigoMarca}/modelos`,
    anos: (codigoMarca, codigoModelo) => 
      `${BASE_URL}/caminhoes/marcas/${codigoMarca}/modelos/${codigoModelo}/anos`,
    valor: (codigoMarca, codigoModelo, codigoAno) => 
      `${BASE_URL}/caminhoes/marcas/${codigoMarca}/modelos/${codigoModelo}/anos/${codigoAno}`
  }
};
```

### Funções de API

#### Buscar Marcas
```javascript
async function buscarMarcas(tipo) {
  try {
    const response = await fetch(ENDPOINTS[tipo].marcas);
    const data = await response.json();
    return data; // [{codigo: "1", nome: "Fiat"}, ...]
  } catch (error) {
    console.error('Erro ao buscar marcas:', error);
    return [];
  }
}
```

#### Buscar Modelos
```javascript
async function buscarModelos(tipo, codigoMarca) {
  try {
    const response = await fetch(ENDPOINTS[tipo].modelos(codigoMarca));
    const data = await response.json();
    return data.modelos; // [{codigo: "1", nome: "UNO"}, ...]
  } catch (error) {
    console.error('Erro ao buscar modelos:', error);
    return [];
  }
}
```

#### Buscar Anos
```javascript
async function buscarAnos(tipo, codigoMarca, codigoModelo) {
  try {
    const response = await fetch(ENDPOINTS[tipo].anos(codigoMarca, codigoModelo));
    const data = await response.json();
    return data; // [{codigo: "2020-1", nome: "2020 Gasolina"}, ...]
  } catch (error) {
    console.error('Erro ao buscar anos:', error);
    return [];
  }
}
```

#### Buscar Valor FIPE
```javascript
async function buscarValorFipe(tipo, codigoMarca, codigoModelo, codigoAno) {
  try {
    const response = await fetch(
      ENDPOINTS[tipo].valor(codigoMarca, codigoModelo, codigoAno)
    );
    const data = await response.json();
    /* Retorna:
    {
      Valor: "R$ 48.500,00",
      Marca: "Fiat",
      Modelo: "UNO VIVACE 1.0 Fire Flex 8V 5p",
      AnoModelo: 2020,
      Combustivel: "Gasolina",
      CodigoFipe: "001004-1",
      MesReferencia: "novembro de 2024",
      TipoVeiculo: 1,
      SiglaCombustivel: "G"
    }
    */
    return data;
  } catch (error) {
    console.error('Erro ao buscar valor:', error);
    return null;
  }
}
```

---

## 🧠 LÓGICA DE BUSCA

### Estados React Necessários

```javascript
// Estados de filtro
const [tipoVeiculo, setTipoVeiculo] = useState('carros');
const [orcamento, setOrcamento] = useState(50000);
const [marcas, setMarcas] = useState([]);
const [marcaSelecionada, setMarcaSelecionada] = useState('');
const [modelos, setModelos] = useState([]);
const [modeloSelecionado, setModeloSelecionado] = useState('');
const [anoInicio, setAnoInicio] = useState('');
const [anoFim, setAnoFim] = useState('');

// Estados de resultado
const [resultados, setResultados] = useState([]);
const [loading, setLoading] = useState(false);
const [buscaRealizada, setBuscaRealizada] = useState(false);

// Estados de progresso (para busca ampla)
const [progresso, setProgresso] = useState({
  atual: 0,
  total: 0,
  mensagem: ''
});
```

### useEffect - Carregar Marcas ao Mudar Tipo

```javascript
useEffect(() => {
  async function carregarMarcas() {
    const marcasData = await buscarMarcas(tipoVeiculo);
    setMarcas(marcasData);
    setMarcaSelecionada(''); // Reset
    setModelos([]);
    setModeloSelecionado('');
  }
  
  if (tipoVeiculo) {
    carregarMarcas();
  }
}, [tipoVeiculo]);
```

### useEffect - Carregar Modelos ao Selecionar Marca

```javascript
useEffect(() => {
  async function carregarModelos() {
    if (marcaSelecionada) {
      const modelosData = await buscarModelos(tipoVeiculo, marcaSelecionada);
      setModelos(modelosData);
      setModeloSelecionado(''); // Reset
    } else {
      setModelos([]);
      setModeloSelecionado('');
    }
  }
  
  carregarModelos();
}, [marcaSelecionada, tipoVeiculo]);
```

---

### FUNÇÃO PRINCIPAL DE BUSCA

```javascript
async function buscarVeiculos() {
  setLoading(true);
  setBuscaRealizada(true);
  setResultados([]);
  
  try {
    let resultadosEncontrados = [];
    
    // Verificar tipo de busca
    if (modeloSelecionado) {
      // BUSCA ESPECÍFICA
      resultadosEncontrados = await buscaEspecifica();
    } else {
      // BUSCA AMPLA
      resultadosEncontrados = await buscaAmpla();
    }
    
    setResultados(resultadosEncontrados);
    
  } catch (error) {
    console.error('Erro na busca:', error);
    alert('Erro ao buscar veículos. Tente novamente.');
  } finally {
    setLoading(false);
    setProgresso({ atual: 0, total: 0, mensagem: '' });
  }
}
```

---

### MODALIDADE 1: Busca Específica

```javascript
async function buscaEspecifica() {
  const resultados = [];
  const precoMin = orcamento - 5000;
  const precoMax = orcamento + 5000;
  
  // 1. Buscar anos disponíveis do modelo
  const anosDisponiveis = await buscarAnos(
    tipoVeiculo, 
    marcaSelecionada, 
    modeloSelecionado
  );
  
  // 2. Filtrar anos pela faixa selecionada (se especificado)
  let anosFiltrados = anosDisponiveis;
  
  if (anoInicio || anoFim) {
    anosFiltrados = anosDisponiveis.filter(ano => {
      const anoNum = parseInt(ano.codigo.split('-')[0]);
      const inicio = anoInicio ? parseInt(anoInicio) : 1900;
      const fim = anoFim ? parseInt(anoFim) : 2100;
      return anoNum >= inicio && anoNum <= fim;
    });
  }
  
  // 3. Para cada ano, buscar valor e verificar se está na faixa
  for (const ano of anosFiltrados) {
    try {
      const veiculo = await buscarValorFipe(
        tipoVeiculo,
        marcaSelecionada,
        modeloSelecionado,
        ano.codigo
      );
      
      if (veiculo) {
        const valorNumerico = converterPrecoFipe(veiculo.Valor);
        
        // Verificar se está na faixa de preço
        if (valorNumerico >= precoMin && valorNumerico <= precoMax) {
          resultados.push(veiculo);
        }
      }
    } catch (error) {
      console.error(`Erro ao buscar ano ${ano.nome}:`, error);
    }
  }
  
  // 4. Ordenar por valor (crescente)
  resultados.sort((a, b) => {
    const valorA = converterPrecoFipe(a.Valor);
    const valorB = converterPrecoFipe(b.Valor);
    return valorA - valorB;
  });
  
  return resultados;
}
```

---

### MODALIDADE 2: Busca Ampla

```javascript
async function buscaAmpla() {
  const resultados = [];
  const precoMin = orcamento - 5000;
  const precoMax = orcamento + 5000;
  
  // 1. Determinar marcas a buscar
  let marcasParaBuscar = [];
  
  if (marcaSelecionada) {
    // Se marca foi selecionada, buscar apenas nela
    const marca = marcas.find(m => m.codigo === marcaSelecionada);
    marcasParaBuscar = [marca];
  } else {
    // Se não, buscar em TODAS as marcas (limitar a 20 para performance)
    marcasParaBuscar = marcas.slice(0, 20);
  }
  
  setProgresso({
    atual: 0,
    total: marcasParaBuscar.length,
    mensagem: 'Iniciando busca...'
  });
  
  // 2. Para cada marca
  for (let i = 0; i < marcasParaBuscar.length; i++) {
    const marca = marcasParaBuscar[i];
    
    setProgresso({
      atual: i + 1,
      total: marcasParaBuscar.length,
      mensagem: `Buscando na marca ${marca.nome}...`
    });
    
    try {
      // 3. Buscar modelos da marca (limitar a 15 para performance)
      const modelosDaMarca = await buscarModelos(tipoVeiculo, marca.codigo);
      const modelosLimitados = modelosDaMarca.slice(0, 15);
      
      // 4. Para cada modelo
      for (const modelo of modelosLimitados) {
        try {
          // 5. Buscar anos disponíveis
          const anosDoModelo = await buscarAnos(
            tipoVeiculo,
            marca.codigo,
            modelo.codigo
          );
          
          if (anosDoModelo.length === 0) continue;
          
          // 6. Pegar apenas o ano mais recente (para performance)
          const anoMaisRecente = anosDoModelo[0];
          
          // 7. Buscar valor FIPE
          const veiculo = await buscarValorFipe(
            tipoVeiculo,
            marca.codigo,
            modelo.codigo,
            anoMaisRecente.codigo
          );
          
          if (veiculo) {
            const valorNumerico = converterPrecoFipe(veiculo.Valor);
            
            // 8. Se valor estiver na faixa, adicionar
            if (valorNumerico >= precoMin && valorNumerico <= precoMax) {
              resultados.push(veiculo);
              
              // Limitar a 50 resultados para não sobrecarregar
              if (resultados.length >= 50) {
                return ordenarResultados(resultados);
              }
            }
          }
        } catch (error) {
          // Ignorar erros individuais de modelo
          console.error(`Erro no modelo ${modelo.nome}:`, error);
        }
      }
    } catch (error) {
      console.error(`Erro na marca ${marca.nome}:`, error);
    }
  }
  
  return ordenarResultados(resultados);
}

function ordenarResultados(resultados) {
  return resultados.sort((a, b) => {
    const valorA = converterPrecoFipe(a.Valor);
    const valorB = converterPrecoFipe(b.Valor);
    return valorA - valorB;
  });
}
```

---

## 🛠️ FUNÇÕES AUXILIARES

### Converter Preço FIPE para Número

```javascript
function converterPrecoFipe(valorString) {
  // "R$ 48.500,00" → 48500
  if (!valorString) return 0;
  
  return parseFloat(
    valorString
      .replace('R, '')
      .replace(/\s/g, '')      // Remove espaços
      .replace(/\./g, '')      // Remove pontos (milhares)
      .replace(',', '.')       // Substitui vírgula por ponto
  );
}
```

### Formatar Preço para Exibição

```javascript
function formatarPreco(valor) {
  return new Intl.NumberFormat('pt-BR', {
    style: 'currency',
    currency: 'BRL',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(valor);
}
```

### Normalizar String para URL

```javascript
function normalizarParaURL(str) {
  return str
    .toLowerCase()
    .normalize('NFD')                    // Decompõe caracteres acentuados
    .replace(/[\u0300-\u036f]/g, '')    // Remove acentos
    .replace(/\s+/g, '-')                // Substitui espaços por hífen
    .replace(/[^\w-]/g, '')              // Remove caracteres especiais
    .replace(/-+/g, '-')                 // Remove hífens duplicados
    .replace(/^-|-$/g, '');              // Remove hífens do início/fim
}
```

### Gerar URLs das Plataformas

```javascript
function gerarURL(plataforma, marca, modelo, orcamento) {
  const marcaSlug = normalizarParaURL(marca);
  const modeloSlug = normalizarParaURL(modelo);
  const precoMax = orcamento + 5000;
  
  const urls = {
    webmotors: `https://www.webmotors.com.br/comprar/${marcaSlug}/${modeloSlug}?precoate=${precoMax}`,
    
    olx: `https://www.olx.com.br/autos-e-pecas/carros-vans-e-utilitarios?q=${encodeURIComponent(marca + ' ' + modelo)}&pe=${precoMax}`,
    
    icarros: `https://www.icarros.com.br/comprar/${marcaSlug}-${modeloSlug}.html`,
    
    mercadolivre: `https://carros.mercadolivre.com.br/${marcaSlug}-${modeloSlug}`
  };
  
  return urls[plataforma] || '#';
}
```

---

## 📱 RESPONSIVIDADE

### Breakpoints Tailwind

```javascript
// sm: 640px   - Smartphones grandes
// md: 768px   - Tablets
// lg: 1024px  - Laptops
// xl: 1280px  - Desktops
// 2xl: 1536px - Telas grandes
```

### Grid Responsivo de Resultados

```jsx
// Mobile: 1 coluna
// Tablet: 2 colunas
// Desktop: 3 colunas

<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {/* Cards aqui */}
</div>
```

### Filtros Responsivos

```jsx
// Mobile: Empilhados verticalmente
// Desktop: Lado a lado

<div className="grid grid-cols-1 md:grid-cols-3 gap-4">
  {/* Botões de tipo */}
</div>

<div className="grid grid-cols-2 gap-4">
  {/* Ano início/fim */}
</div>
```

### Padding Responsivo

```jsx
// Mobile: padding menor
// Desktop: padding maior

<div className="px-4 md:px-6 lg:px-8">
  <div className="py-6 md:py-8 lg:py-12">
    {/* Conteúdo */}
  </div>
</div>
```

### Logo Responsivo

```jsx
<img 
  src="QueroCarro(1).png" 
  alt="QueroCarro Logo" 
  className="h-12 md:h-16 lg:h-20"
/>
```

---

## ⚡ OTIMIZAÇÕES DE PERFORMANCE

### 1. Debounce no Slider de Orçamento

```javascript
import { useState, useEffect } from 'react';

function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
}

// Uso:
const [orcamentoTemp, setOrcamentoTemp] = useState(50000);
const orcamento = useDebounce(orcamentoTemp, 500); // 500ms de delay
```

### 2. Cache de Requisições

```javascript
const cache = {};

async function buscarComCache(url) {
  if (cache[url]) {
    return cache[url];
  }
  
  const response = await fetch(url);
  const data = await response.json();
  cache[url] = data;
  
  return data;
}
```

### 3. Abort Controller (Cancelar Requisições)

```javascript
let abortController = null;

async function buscarVeiculos() {
  // Cancelar busca anterior se existir
  if (abortController) {
    abortController.abort();
  }
  
  abortController = new AbortController();
  
  try {
    const response = await fetch(url, {
      signal: abortController.signal
    });
    // ...
  } catch (error) {
    if (error.name === 'AbortError') {
      console.log('Busca cancelada');
      return;
    }
    throw error;
  }
}
```

### 4. Lazy Loading de Resultados

```javascript
const [resultadosVisiveis, setResultadosVisiveis] = useState(12);

function carregarMais() {
  setResultadosVisiveis(prev => prev + 12);
}

// No JSX:
{resultados.slice(0, resultadosVisiveis).map(veiculo => (
  <ResultadoCard key={veiculo.CodigoFipe} veiculo={veiculo} />
))}

{resultados.length > resultadosVisiveis && (
  <button onClick={carregarMais} className="...">
    Carregar Mais
  </button>
)}
```

---

## ♿ ACESSIBILIDADE

### Labels e ARIA

```jsx
// Labels descritivos
<label htmlFor="marca-select" className="...">
  🏭 Marca (opcional)
</label>
<select id="marca-select" aria-label="Selecione a marca do veículo">
  ...
</select>

// ARIA labels para ícones
<button aria-label="Buscar veículos">
  <Search aria-hidden="true" />
</button>

// ARIA live para atualizações dinâmicas
<div aria-live="polite" aria-atomic="true">
  {resultados.length} veículos encontrados
</div>
```

### Contraste de Cores

Todas as combinações devem passar WCAG AA:
- Texto primário (#1F2937) no branco: ✅ 12.63:1
- Texto secundário (#6B7280) no branco: ✅ 4.61:1
- Botão azul (#3B82F6) com texto branco: ✅ 4.56:1

### Focus Visible

```jsx
className="focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
```

### Navegação por Teclado

- Todos os elementos interativos devem ser acessíveis via Tab
- Enter/Space devem ativar botões
- Escape deve fechar modais (se houver)

---

## 🐛 TRATAMENTO DE ERROS

### Try-Catch em Todas as Requisições

```javascript
async function buscarDados() {
  try {
    const response = await fetch(url);
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const data = await response.json();
    return data;
    
  } catch (error) {
    console.error('Erro ao buscar dados:', error);
    
    // Mostrar mensagem amigável ao usuário
    mostrarErro('Não foi possível carregar os dados. Tente novamente.');
    
    return null;
  }
}
```

### Componente de Erro

```jsx
function ErroMensagem({ mensagem, onTentarNovamente }) {
  return (
    <div className="bg-red-50 border border-red-200 rounded-lg p-6 max-w-md mx-auto">
      <div className="flex items-center gap-3 mb-4">
        <div className="text-3xl">❌</div>
        <h3 className="text-lg font-bold text-red-800">Ops! Algo deu errado</h3>
      </div>
      
      <p className="text-red-700 mb-4">{mensagem}</p>
      
      <button
        onClick={onTentarNovamente}
        className="w-full bg-red-500 hover:bg-red-600 text-white font-medium 
          py-2 px-4 rounded-lg transition-colors"
      >
        Tentar Novamente
      </button>
    </div>
  );
}
```

### Timeout para Busca Ampla

```javascript
async function buscaAmplaComTimeout() {
  const TIMEOUT = 30000; // 30 segundos
  
  const timeoutPromise = new Promise((_, reject) => {
    setTimeout(() => reject(new Error('Timeout')), TIMEOUT);
  });
  
  try {
    const resultado = await Promise.race([
      buscaAmpla(),
      timeoutPromise
    ]);
    return resultado;
  } catch (error) {
    if (error.message === 'Timeout') {
      alert('A busca está demorando muito. Tente filtros mais específicos.');
    }
    throw error;
  }
}
```

---

## 📝 ESTRUTURA FINAL DO CÓDIGO

```jsx
import React, { useState, useEffect } from 'react';
import { Car, Bike, Truck, Search, ExternalLink, DollarSign, Calendar, Filter } from 'lucide-react';

export default function QueroCarro() {
  // ===== ESTADOS =====
  const [tipoVeiculo, setTipoVeiculo] = useState('carros');
  const [orcamento, setOrcamento] = useState(50000);
  const [marcas, setMarcas] = useState([]);
  const [marcaSelecionada, setMarcaSelecionada] = useState('');
  const [modelos, setModelos] = useState([]);
  const [modeloSelecionado, setModeloSelecionado] = useState('');
  const [anoInicio, setAnoInicio] = useState('');
  const [anoFim, setAnoFim] = useState('');
  const [resultados, setResultados] = useState([]);
  const [loading, setLoading] = useState(false);
  const [buscaRealizada, setBuscaRealizada] = useState(false);
  const [progresso, setProgresso] = useState({ atual: 0, total: 0, mensagem: '' });

  // ===== EFFECTS =====
  useEffect(() => {
    // Carregar marcas ao mudar tipo
  }, [tipoVeiculo]);

  useEffect(() => {
    // Carregar modelos ao selecionar marca
  }, [marcaSelecionada]);

  // ===== FUNÇÕES DE API =====
  async function buscarMarcas(tipo) { /* ... */ }
  async function buscarModelos(tipo, codigoMarca) { /* ... */ }
  async function buscarAnos(tipo, codigoMarca, codigoModelo) { /* ... */ }
  async function buscarValorFipe(tipo, codigoMarca, codigoModelo, codigoAno) { /* ... */ }

  // ===== FUNÇÕES DE BUSCA =====
  async function buscarVeiculos() { /* ... */ }
  async function buscaEspecifica() { /* ... */ }
  async function buscaAmpla() { /* ... */ }

  // ===== FUNÇÕES AUXILIARES =====
  function converterPrecoFipe(valorString) { /* ... */ }
  function formatarPreco(valor) { /* ... */ }
  function normalizarParaURL(str) { /* ... */ }
  function gerarURL(plataforma, marca, modelo, orcamento) { /* ... */ }
  function getBadgeCombustivel(combustivel) { /* ... */ }
  function gerarAnos() { /* ... */ }

  // ===== RENDER =====
  return (
    <div className="min-h-screen bg-gray-50">
      {/* HEADER */}
      <Header />

      {/* MAIN CONTENT */}
      <main className="container mx-auto px-4 py-8">
        {/* CARD DE FILTROS */}
        <CardFiltros />

        {/* RESULTADOS */}
        {loading && <LoadingSpinner progresso={progresso} />}
        {!loading && buscaRealizada && <SecaoResultados />}
        {!loading && !buscaRealizada && <EstadoInicial />}
      </main>

      {/* FOOTER (opcional) */}
      <Footer />
    </div>
  );
}

// ===== COMPONENTES AUXILIARES =====
function Header() { /* ... */ }
function CardFiltros() { /* ... */ }
function ResultadoCard({ veiculo }) { /* ... */ }
function BotaoPlataforma({ nome, cor, url }) { /* ... */ }
function LoadingSpinner({ progresso }) { /* ... */ }
function EstadoInicial() { /* ... */ }
function EmptyState() { /* ... */ }
function ErroMensagem({ mensagem, onTentarNovamente }) { /* ... */ }
```

---

## 🎬 ANIMAÇÕES E MICRO-INTERAÇÕES

### Fade-in com Stagger (Entrada Progressiva dos Cards)

```jsx
// Adicionar delay progressivo aos cards
{resultados.map((veiculo, index) => (
  <div
    key={index}
    style={{ animationDelay: `${index * 0.1}s` }}
    className="animate-fade-in"
  >
    <ResultadoCard veiculo={veiculo} />
  </div>
))}

// CSS customizado (adicionar no início do componente)
<style>{`
  @keyframes fade-in {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .animate-fade-in {
    animation: fade-in 0.5s ease-out forwards;
    opacity: 0;
  }
`}</style>
```

### Skeleton Loading (Efeito Shimmer)

```jsx
function SkeletonCard() {
  return (
    <div className="bg-white rounded-xl shadow-md p-6 animate-pulse">
      {/* Ícone placeholder */}
      <div className="flex justify-center mb-4">
        <div className="bg-gray-200 w-16 h-16 rounded-full" />
      </div>
      
      {/* Título placeholder */}
      <div className="space-y-2 mb-4">
        <div className="h-4 bg-gray-200 rounded w-3/4 mx-auto" />
        <div className="h-4 bg-gray-200 rounded w-1/2 mx-auto" />
      </div>
      
      {/* Preço placeholder */}
      <div className="h-8 bg-gray-200 rounded w-2/3 mx-auto mb-4" />
      
      {/* Botões placeholder */}
      <div className="grid grid-cols-2 gap-2">
        <div className="h-10 bg-gray-200 rounded" />
        <div className="h-10 bg-gray-200 rounded" />
        <div className="h-10 bg-gray-200 rounded" />
        <div className="h-10 bg-gray-200 rounded" />
      </div>
    </div>
  );
}

// Usar durante carregamento
{loading && (
  <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    {[...Array(6)].map((_, i) => (
      <SkeletonCard key={i} />
    ))}
  </div>
)}
```

### Contador Animado de Resultados

```jsx
function ContadorAnimado({ valor }) {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    let start = 0;
    const duration = 1000; // 1 segundo
    const increment = valor / (duration / 16); // 60 FPS
    
    const timer = setInterval(() => {
      start += increment;
      if (start >= valor) {
        setCount(valor);
        clearInterval(timer);
      } else {
        setCount(Math.floor(start));
      }
    }, 16);
    
    return () => clearInterval(timer);
  }, [valor]);
  
  return <span>{count}</span>;
}

// Uso:
<p className="text-gray-600">
  ✅ <ContadorAnimado valor={resultados.length} /> veículos encontrados
</p>
```

### Scroll Suave para Resultados

```jsx
function buscarVeiculos() {
  // ... lógica de busca
  
  // Após buscar, scroll suave para resultados
  setTimeout(() => {
    document.getElementById('resultados')?.scrollIntoView({ 
      behavior: 'smooth',
      block: 'start'
    });
  }, 300);
}

// No JSX dos resultados
<div id="resultados" className="mt-12">
  {/* Resultados aqui */}
</div>
```

---

## 🔔 TOAST NOTIFICATIONS (Opcional)

```jsx
function Toast({ mensagem, tipo, onClose }) {
  const cores = {
    sucesso: 'bg-green-500',
    erro: 'bg-red-500',
    info: 'bg-blue-500',
    aviso: 'bg-yellow-500'
  };
  
  useEffect(() => {
    const timer = setTimeout(onClose, 4000);
    return () => clearTimeout(timer);
  }, [onClose]);
  
  return (
    <div className={`fixed bottom-4 right-4 ${cores[tipo]} text-white px-6 py-4 
      rounded-lg shadow-xl animate-slide-up z-50 max-w-md`}>
      <div className="flex items-center gap-3">
        <span>{mensagem}</span>
        <button 
          onClick={onClose}
          className="ml-auto hover:bg-white/20 p-1 rounded"
        >
          ✕
        </button>
      </div>
    </div>
  );
}

// Estado para toast
const [toast, setToast] = useState(null);

// Função para mostrar toast
function mostrarToast(mensagem, tipo = 'info') {
  setToast({ mensagem, tipo });
}

// No JSX principal
{toast && (
  <Toast 
    mensagem={toast.mensagem}
    tipo={toast.tipo}
    onClose={() => setToast(null)}
  />
)}

// Uso
mostrarToast('Busca concluída com sucesso!', 'sucesso');
mostrarToast('Erro ao buscar veículos', 'erro');
```

---

## 📊 ESTATÍSTICAS E INFORMAÇÕES EXTRAS (Opcional)

### Card de Estatísticas

```jsx
function CardEstatisticas({ resultados }) {
  const precoMedio = resultados.reduce((acc, v) => 
    acc + converterPrecoFipe(v.Valor), 0
  ) / resultados.length;
  
  const precoMin = Math.min(...resultados.map(v => converterPrecoFipe(v.Valor)));
  const precoMax = Math.max(...resultados.map(v => converterPrecoFipe(v.Valor)));
  
  return (
    <div className="bg-gradient-to-r from-blue-50 to-purple-50 rounded-xl p-6 mb-8">
      <h3 className="text-lg font-bold text-gray-800 mb-4">📊 Estatísticas</h3>
      
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div className="bg-white rounded-lg p-4 text-center">
          <div className="text-sm text-gray-600 mb-1">Preço Médio</div>
          <div className="text-xl font-bold text-blue-600">
            {formatarPreco(precoMedio)}
          </div>
        </div>
        
        <div className="bg-white rounded-lg p-4 text-center">
          <div className="text-sm text-gray-600 mb-1">Mais Barato</div>
          <div className="text-xl font-bold text-green-600">
            {formatarPreco(precoMin)}
          </div>
        </div>
        
        <div className="bg-white rounded-lg p-4 text-center">
          <div className="text-sm text-gray-600 mb-1">Mais Caro</div>
          <div className="text-xl font-bold text-orange-600">
            {formatarPreco(precoMax)}
          </div>
        </div>
      </div>
    </div>
  );
}
```

### Filtro de Ordenação

```jsx
const [ordenacao, setOrdenacao] = useState('preco-crescente');

function ordenarResultados(resultados) {
  const copia = [...resultados];
  
  switch (ordenacao) {
    case 'preco-crescente':
      return copia.sort((a, b) => 
        converterPrecoFipe(a.Valor) - converterPrecoFipe(b.Valor)
      );
      
    case 'preco-decrescente':
      return copia.sort((a, b) => 
        converterPrecoFipe(b.Valor) - converterPrecoFipe(a.Valor)
      );
      
    case 'ano-recente':
      return copia.sort((a, b) => b.AnoModelo - a.AnoModelo);
      
    case 'ano-antigo':
      return copia.sort((a, b) => a.AnoModelo - b.AnoModelo);
      
    default:
      return copia;
  }
}

// Select de ordenação
<div className="flex items-center gap-3 mb-6">
  <label className="text-sm font-medium text-gray-700">
    Ordenar por:
  </label>
  <select
    value={ordenacao}
    onChange={(e) => setOrdenacao(e.target.value)}
    className="px-4 py-2 border-2 border-gray-200 rounded-lg 
      focus:border-blue-500 transition-all"
  >
    <option value="preco-crescente">Menor Preço</option>
    <option value="preco-decrescente">Maior Preço</option>
    <option value="ano-recente">Mais Novo</option>
    <option value="ano-antigo">Mais Antigo</option>
  </select>
</div>
```

---

## 💾 PERSISTÊNCIA LOCAL (Histórico)

### Salvar Histórico de Buscas

```jsx
// Salvar busca no localStorage
function salvarHistorico(busca) {
  try {
    const historico = JSON.parse(localStorage.getItem('querocarro_historico') || '[]');
    historico.unshift({
      ...busca,
      timestamp: new Date().toISOString()
    });
    
    // Manter apenas últimas 10 buscas
    const historicoLimitado = historico.slice(0, 10);
    localStorage.setItem('querocarro_historico', JSON.stringify(historicoLimitado));
  } catch (error) {
    console.error('Erro ao salvar histórico:', error);
  }
}

// Carregar histórico
function carregarHistorico() {
  try {
    return JSON.parse(localStorage.getItem('querocarro_historico') || '[]');
  } catch (error) {
    console.error('Erro ao carregar histórico:', error);
    return [];
  }
}

// Aplicar busca do histórico
function aplicarBuscaHistorico(busca) {
  setTipoVeiculo(busca.tipo);
  setOrcamento(busca.orcamento);
  setMarcaSelecionada(busca.marca);
  setModeloSelecionado(busca.modelo);
  // ... outros campos
}
```

### Dropdown de Histórico

```jsx
function DropdownHistorico() {
  const [mostrar, setMostrar] = useState(false);
  const historico = carregarHistorico();
  
  if (historico.length === 0) return null;
  
  return (
    <div className="relative">
      <button
        onClick={() => setMostrar(!mostrar)}
        className="flex items-center gap-2 px-4 py-2 bg-white border-2 
          border-gray-200 rounded-lg hover:border-blue-500 transition-all"
      >
        <Clock className="w-4 h-4" />
        Buscas Recentes
      </button>
      
      {mostrar && (
        <div className="absolute top-full mt-2 w-80 bg-white rounded-lg 
          shadow-xl border border-gray-200 z-50 max-h-96 overflow-y-auto">
          {historico.map((busca, index) => (
            <button
              key={index}
              onClick={() => {
                aplicarBuscaHistorico(busca);
                setMostrar(false);
              }}
              className="w-full text-left px-4 py-3 hover:bg-gray-50 
                border-b border-gray-100 last:border-b-0"
            >
              <div className="font-medium text-gray-800">
                {busca.marca} {busca.modelo || 'Todos'}
              </div>
              <div className="text-sm text-gray-500">
                {formatarPreco(busca.orcamento)} • {busca.tipo}
              </div>
              <div className="text-xs text-gray-400 mt-1">
                {new Date(busca.timestamp).toLocaleDateString('pt-BR')}
              </div>
            </button>
          ))}
        </div>
      )}
    </div>
  );
}
```

---

## 🎁 FEATURES EXTRAS PREMIUM

### Comparador de Veículos

```jsx
const [veiculosParaComparar, setVeiculosParaComparar] = useState([]);

function adicionarParaComparacao(veiculo) {
  if (veiculosParaComparar.length >= 3) {
    mostrarToast('Você pode comparar até 3 veículos', 'aviso');
    return;
  }
  setVeiculosParaComparar([...veiculosParaComparar, veiculo]);
}

function TabelaComparacao() {
  return (
    <div className="bg-white rounded-xl shadow-lg p-6 mb-8">
      <h3 className="text-xl font-bold mb-4">🔄 Comparar Veículos</h3>
      
      <div className="grid grid-cols-3 gap-4">
        {veiculosParaComparar.map((veiculo, index) => (
          <div key={index} className="border border-gray-200 rounded-lg p-4">
            <h4 className="font-bold text-gray-800 mb-2">{veiculo.Modelo}</h4>
            <div className="space-y-2 text-sm">
              <div className="flex justify-between">
                <span className="text-gray-600">Ano:</span>
                <span className="font-medium">{veiculo.AnoModelo}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Combustível:</span>
                <span className="font-medium">{veiculo.Combustivel}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Valor FIPE:</span>
                <span className="font-bold text-green-600">{veiculo.Valor}</span>
              </div>
            </div>
            <button
              onClick={() => setVeiculosParaComparar(
                veiculosParaComparar.filter((_, i) => i !== index)
              )}
              className="w-full mt-3 text-red-500 text-sm hover:text-red-600"
            >
              Remover
            </button>
          </div>
        ))}
      </div>
    </div>
  );
}
```

### Botão "Compartilhar Busca"

```jsx
function compartilharBusca() {
  const url = `${window.location.origin}?tipo=${tipoVeiculo}&orcamento=${orcamento}&marca=${marcaSelecionada}&modelo=${modeloSelecionado}`;
  
  if (navigator.share) {
    navigator.share({
      title: 'QueroCarro - Minha Busca',
      text: `Veja os veículos que encontrei no QueroCarro!`,
      url: url
    });
  } else {
    navigator.clipboard.writeText(url);
    mostrarToast('Link copiado para a área de transferência!', 'sucesso');
  }
}

// Botão
<button
  onClick={compartilharBusca}
  className="flex items-center gap-2 px-4 py-2 bg-gray-100 
    hover:bg-gray-200 rounded-lg transition-colors"
>
  <Share2 className="w-4 h-4" />
  Compartilhar
</button>
```

---

## 🧪 VALIDAÇÕES E TESTES

### Validação de Formulário

```javascript
function validarFiltros() {
  const erros = [];
  
  if (!tipoVeiculo) {
    erros.push('Selecione o tipo de veículo');
  }
  
  if (orcamento < 10000 || orcamento > 300000) {
    erros.push('Orçamento deve estar entre R$ 10.000 e R$ 300.000');
  }
  
  if (anoInicio && anoFim && parseInt(anoInicio) > parseInt(anoFim)) {
    erros.push('Ano inicial não pode ser maior que ano final');
  }
  
  return erros;
}

function buscarVeiculos() {
  const erros = validarFiltros();
  
  if (erros.length > 0) {
    mostrarToast(erros[0], 'erro');
    return;
  }
  
  // Continuar com busca...
}
```

### Casos de Teste

```javascript
// TESTE 1: Busca específica
// Tipo: Carros
// Marca: Fiat
// Modelo: Uno
// Orçamento: R$ 30.000
// Esperado: Lista de Fiat Uno entre R$ 25k e R$ 35k

// TESTE 2: Busca ampla
// Tipo: Carros
// Marca: Todas
// Modelo: -
// Orçamento: R$ 50.000
// Esperado: Lista de vários modelos entre R$ 45k e R$ 55k

// TESTE 3: Sem resultados
// Tipo: Carros
// Marca: Ferrari
// Orçamento: R$ 30.000
// Esperado: Mensagem "Nenhum veículo encontrado"

// TESTE 4: Erro de API
// Simular erro na requisição
// Esperado: Mensagem de erro amigável

// TESTE 5: Responsividade
// Testar em mobile (375px), tablet (768px), desktop (1920px)
// Esperado: Layout adaptado para cada tamanho
```

---

## 📚 DOCUMENTAÇÃO ADICIONAL

### Estrutura de Pastas Sugerida (se expandir)

```
querocarro/
├── src/
│   ├── components/
│   │   ├── Header.jsx
│   │   ├── CardFiltros.jsx
│   │   ├── ResultadoCard.jsx
│   │   ├── BotaoPlataforma.jsx
│   │   ├── LoadingSpinner.jsx
│   │   └── Toast.jsx
│   ├── hooks/
│   │   ├── useDebounce.js
│   │   └── useFipeAPI.js
│   ├── utils/
│   │   ├── formatters.js
│   │   ├── validators.js
│   │   └── urlGenerator.js
│   ├── constants/
│   │   └── api.js
│   └── App.jsx
├── public/
│   └── QueroCarro(1).png
└── package.json
```

### Variáveis de Ambiente (.env)

```bash
# Se futuramente usar backend próprio
VITE_API_BASE_URL=https://parallelum.com.br/fipe/api/v1
VITE_CACHE_DURATION=3600000
VITE_MAX_RESULTS=50
```

### Package.json Sugerido

```json
{
  "name": "querocarro",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "lucide-react": "^0.263.1"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.0.0",
    "autoprefixer": "^10.4.14",
    "postcss": "^8.4.24",
    "tailwindcss": "^3.3.2",
    "vite": "^4.3.9"
  }
}
```

---

## ✅ CHECKLIST FINAL DE IMPLEMENTAÇÃO

### Obrigatório (MVP)
- [ ] Header com logo QueroCarro(1).png
- [ ] Filtro de tipo de veículo (botões)
- [ ] Slider de orçamento com faixa ±R$ 5.000
- [ ] Select de marca (opcional, com "Todas")
- [ ] Select de modelo (opcional, com "Todos")
- [ ] Select de faixa de ano (opcional)
- [ ] Botão de busca com loading
- [ ] Integração com API FIPE
- [ ] Busca específica (marca + modelo)
- [ ] Busca ampla (todas as marcas/modelos)
- [ ] Grid responsivo de resultados
- [ ] Card de veículo com todas informações
- [ ] 4 botões de plataforma (Webmotors, OLX, iCarros, Mercado Livre)
- [ ] URLs geradas corretamente
- [ ] Estados de loading, vazio e erro
- [ ] Responsividade mobile/tablet/desktop
- [ ] Acessibilidade básica (labels, ARIA)

### Recomendado
- [ ] Barra de progresso para busca ampla
- [ ] Skeleton loading durante busca
- [ ] Animações de entrada dos cards
- [ ] Toast notifications
- [ ] Histórico de buscas (localStorage)
- [ ] Ordenação de resultados
- [ ] Estatísticas (preço médio, min, max)
- [ ] Contador animado de resultados
- [ ] Scroll suave para resultados
- [ ] Cache de requisições

### Opcional (Premium)
- [ ] Comparador de veículos (até 3)
- [ ] Botão compartilhar busca
- [ ] Filtros avançados salvos
- [ ] Modo escuro (dark mode)
- [ ] Gráfico de evolução de preços
- [ ] Alertas de preço por email
- [ ] Integração com mais plataformas

---

## 🚀 PRÓXIMOS PASSOS APÓS CRIAÇÃO

1. **Testar em Diferentes Dispositivos**
   - Chrome DevTools (responsividade)
   - Dispositivos reais (iOS, Android)
   - Diferentes navegadores

2. **Otimizar Performance**
   - Lighthouse audit
   - Reduzir tamanho de bundle
   - Lazy loading de imagens

3. **SEO (se publicar)**
   - Meta tags adequadas
   - Open Graph para redes sociais
   - Sitemap e robots.txt

4. **Deploy**
   - Vercel (recomendado)
   - Netlify
   - GitHub Pages

5. **Melhorias Futuras**
   - Backend próprio para cache
   - Banco de dados de histórico de preços
   - Sistema de usuários e favoritos
   - Integração com APIs oficiais

---

## 📞 SUPORTE E RECURSOS

### Documentação Oficial
- React: https://react.dev
- Tailwind CSS: https://tailwindcss.com/docs
- Lucide Icons: https://lucide.dev
- API FIPE: https://deividfortuna.github.io/fipe/

### Comunidades
- Stack Overflow
- Reddit r/reactjs
- Discord do React Brasil

---

## 🎓 CONCLUSÃO

Este documento fornece TODAS as informações necessárias para criar o site QueroCarro completo e funcional. Siga as especificações de design, implemente as duas modalidades de busca (específica e ampla), e garanta uma experiência de usuário fluida e responsiva.

**Boa sorte com a implementação! 🚗💨**