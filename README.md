# Nexus Agent

Agente de voz local do Nexus. Responde por comando de voz, integra com o painel em [usenexus.online](https://usenexus.online) e executa tarefas no seu computador.

---

## Requisitos

- Windows 10 ou superior
- Python 3.11 ou 3.12 → [Download](https://www.python.org/downloads/)
  - Durante a instalação: marque **"Add Python to PATH"**
- Microfone

---

## Instalação

1. **Baixe** este repositório (botão verde `Code` → `Download ZIP`)
2. **Extraia** o ZIP em uma pasta de sua preferência
3. **Execute** o `setup.bat` (duplo clique)
   - Instala as dependências automaticamente
   - Baixa o modelo de reconhecimento de voz (~50MB)

---

## Pareamento

Após a instalação, você precisa vincular o agente à sua conta Nexus:

1. Acesse [usenexus.online](https://usenexus.online) e faça login
2. Vá em **Parear agente** → clique em **Gerar código**
3. No terminal, execute:
   ```
   .venv\Scripts\python -m agent.main
   ```
4. Cole o código de 8 caracteres quando solicitado
5. O agente salva as credenciais e já sobe automaticamente

---

## Uso

Após pareado, inicie o agente:

```
.venv\Scripts\python -m agent.main
```

- Diga **"Olá Nexus"** para ativar
- Faça seu pedido normalmente
- O agente responde por áudio e executa a ação

---

## Problemas comuns

**Python não encontrado**
→ Reinstale o Python marcando "Add Python to PATH"

**Microfone não detectado**
→ Verifique se o microfone está como dispositivo padrão no Windows (Configurações → Som)

**Código de pareamento expirou**
→ Gere um novo código no painel (válido por 10 minutos)

**Agente não responde após longo tempo offline**
→ Repita o pareamento — o token expira após 30 dias sem uso
