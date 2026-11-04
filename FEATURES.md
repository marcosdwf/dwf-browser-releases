# DWF Browser — Funcionalidades

Navegador desktop (Windows) dedicado ao sistema **DWF Sistemas**. Fork do Navega,
construído em Tauri v2 / WebView2. Abre direto na tela de login do DWF e mantém o
usuário dentro do sistema, sem a distração de um navegador comum.

> Este documento é a base do manual em PDF. Cada seção marcada com 📷 indica um
> ponto onde entra um print no manual.

---

## 1. Navegação focada no DWF

### Página inicial fixa 📷
- O navegador abre sempre em `https://app.dwfsistemas.com/login`.
- O botão **Início** (casinha), **nova guia** (Ctrl+T) e **nova janela** levam
  sempre à tela de login do DWF.
- A página inicial **não é editável** — não há como trocar por outro site.

### Barra de endereço somente leitura 📷
- Mostra o endereço atual e permite **selecionar e copiar** o link.
- **Não é digitável**: não dá para navegar para outro site pela barra.
- Links clicados **dentro** do sistema DWF funcionam normalmente — nada é
  bloqueado no back-end, para não travar nenhuma página legítima do sistema.

### Identificação para o sistema
- Cada guia se identifica como DWF Browser: `navigator.userAgent` e o cabeçalho
  `User-Agent` terminam em `dwf_browser/<versão>` (ex.: `dwf_browser/1.7.0`).
- Assim o sistema DWF consegue saber qual navegador e versão estão em uso.

### Sem favoritos
- A barra de favoritos, o botão de estrela e o menu de favoritos ficam
  desativados, para uma interface enxuta voltada só ao DWF.

---

## 2. Login automático no DWF

### Cofre de credenciais 📷
- Em **Menu ▸ Configurações ▸ Credenciais** é possível salvar usuário e senha.
- O campo **Domínio** já vem travado em `app.dwfsistemas.com`.
- A senha é **criptografada com DPAPI** (proteção de dados do Windows, vinculada
  à conta do usuário) e nunca é exibida novamente depois de salva.

### Auto-login
- Com a credencial marcada como **padrão** e **login automático**, ao abrir a tela
  de login o navegador preenche usuário e senha e entra sozinho.
- Funciona também quando o sistema desloga e volta à tela de login (por logoff
  manual ou automático) — ele reentra.
- Compatível com o login por **F2** do DWF.

### Pop-up "Salvar login do DWF" 📷
- Se você abrir a tela de login **sem** uma credencial salva e ficar ~1 segundo
  na tela, aparece um **pop-up** para digitar usuário e senha e ativar o
  auto-login na hora.
- Só aparece na **tela de login** (`/login`), nunca nas demais páginas do sistema.
- Opções no pop-up:
  - **Fazer login automático ao abrir o sistema** (marcado por padrão).
  - **Não perguntar novamente** — desliga o aviso de vez.
- Botões **Salvar** e **Agora não** (ou **×**/Esc para fechar).

### Controle do aviso nas Configurações 📷
- Em **Configurações ▸ Credenciais** há o toggle **"Não solicitar para salvar
  senha"**, que desliga o pop-up. Pode ser reativado a qualquer momento.

### Excluir credencial
- Ao excluir a credencial salva, o auto-login é **interrompido imediatamente** nas
  abas do DWF — não continua reentrando.

---

## 3. Guias e janelas

- **Guias reais** (várias páginas do DWF abertas ao mesmo tempo).
- **Múltiplas janelas** e **destacar guia** (arrastar a guia para fora cria uma
  nova janela) — útil para trabalhar com duas telas do sistema lado a lado.
- Barra de guias que também serve de barra de título (minimizar/maximizar/fechar).
- Atalhos: `Ctrl+T` nova guia, `Ctrl+W` fechar guia, `Ctrl+Tab` alternar,
  `Alt+←/→` voltar/avançar, `F5` recarregar, `F11` tela cheia.

---

## 4. Ferramentas de apoio

### Zoom por guia 📷
- Aumentar/diminuir zoom por página (`Ctrl+ +/−/0`) ou `Ctrl+scroll`.

### Lupa (lente de aumento) 📷
- Lente que segue o cursor, para ampliar trechos da tela.

### Monitor de desempenho 📷
- Janela com **RAM, CPU e rede** do navegador, mais a lista por processo.

### Controle de volume
- Ajuste de volume do aplicativo direto na barra de ferramentas.

---

## 5. Manutenção e privacidade

### Limpeza de dados 📷
- Limpar cookies, armazenamento local, cache e IndexedDB — de **um site**, por
  **tipo** ou **tudo** (estilo Chrome).

### Notificações nativas do Windows
- Sites do DWF podem notificar pela **Central de Notificações do Windows**, com
  controle de permissão por site.

### Regras por domínio (avançado)
- Automações opcionais por site: **auto-atualização** periódica, **manter ativo**
  (keep-alive) e **limpeza periódica** de dados.

---

## 6. Atualizações automáticas

- O DWF Browser verifica novas versões automaticamente e pode **baixar e instalar
  sozinho** a atualização.
- As versões são publicadas no repositório público de releases
  (`marcosdwf/dwf-browser-releases`).
- O rodapé do menu mostra a versão instalada e, quando há atualização, um atalho
  **"Atualizar para X"**.

---

## Requisitos

- Windows 10/11.
- Runtime do **WebView2** (já presente na maioria dos Windows atuais; o instalador
  cuida disso quando necessário).
- Instalação por usuário (não exige administrador).
