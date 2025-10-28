# Desafio-de-Ciberseguran-a-Simula-o-e-Defesa-Contra-Ransomware-e-Keylogger-com-Python
Breve resumo sobre o projeto (implementação, documentação e aprendizado sobre as ameaças e, principalmente, as defesas).
# 🛡️ Projeto Final DIO: Simulação de Malware e Estratégias de Defesa com Python

## 🌟 1. Introdução e Objetivos

Este projeto simula o comportamento do **Ransomware** e do **Keylogger** em um ambiente controlado, utilizando a linguagem Python. O foco principal não é apenas a implementação do ataque, mas a **reflexão aprofundada** sobre as estratégias de detecção, mitigação e defesa contra essas ameaças cibernéticas.

**Objetivos de Aprendizagem Demonstrados:**
* Compreensão prática do funcionamento do sequestro e da captura de dados.
* Habilidade em programar scripts simples simulando ataques (`ransomware.py`, `keylogger.py`).
* **Capacidade de *Troubleshooting*** em ambientes complexos (Kali Linux e Windows).
* Documentação detalhada do processo e reflexão sobre a **Defesa**.

## 💻 2. Configuração do Ambiente e Ferramentas

O desenvolvimento foi realizado utilizando uma combinação de sistemas para testar diferentes desafios de ambiente e segurança:

* **Sistemas Operacionais:** Kali Linux (via VirtualBox) e Windows 10.
* **IDE/Editor:** Visual Studio Code (VS Code).
* **Bibliotecas Python:** `cryptography` (para Ransomware) e `pynput` (para Keylogger).

---

## 🔒 3. Ataque 1: Ransomware Simulado

O script **`ransomware.py`** demonstra o processo de sequestro de dados e a geração da chave para reversão.

### A. Processo de Criptografia
* **Funcionalidade:** O script utiliza a biblioteca `cryptography.fernet` para gerar uma chave simétrica (`chave.key`).
* A função `encontrar_arquivos` foi ajustada para criptografar apenas os arquivos na pasta `test_files`.

#### ✅ Prova de Conceito: Execução do Ransomware

Gerando o código em python.
> ![criando o codigo no python](https://github.com/user-attachments/assets/5bd5c243-38c8-4cbf-8dc0-7ba09be48210)
> ![Criando código para descriptografar](https://github.com/user-attachments/assets/6eacdbee-990c-4650-ac3b-5e2a5fd43999)


>![Gerando comando para descriptografar](https://github.com/user-attachments/assets/56e79c0a-18fb-4ae1-8fa6-321af092d225)

> **Descrição:** Terminal do PowerShell mostrando a execução bem-sucedida do `ransomware.py`, que imprime a mensagem de confirmação e gera os arquivos `chave.key` e `LEIA ISTO.txt` na pasta raiz.

### B. Processo de Descriptografia
* O script **`descriptografar.py`** carrega a chave gerada para reverter o processo e restaurar os arquivos originais.
* **Correção de Lógica:** Durante a implementação, foi identificado um erro de digitação no método (`f.descript` em vez de `f.decrypt`), corrigido para garantir a reversão.

#### ✅ Prova de Conceito: Restauração dos Dados

> ![Arquivos recumperados com sucesso](https://github.com/user-attachments/assets/2338032c-5e04-474f-b988-b2b14b2c4cb3)

>
> **Descrição:** Execução do `descriptografar.py` no terminal, confirmando que os "Arquivos restaurados com sucesso", provando a reversão do ataque.

---

## 🔑 4. Ataque 2: Keylogger Simulado

O script **`keylogger.py`** demonstra a captura de dados (teclas digitadas) de forma furtiva.

### A. Implementação
* **Funcionalidade:** Utiliza a biblioteca **`pynput`** para escutar eventos de teclado e salvar as entradas no arquivo `log.txt`.
* **Correção de Código:** Foi necessário tratar o `TypeError` (Erro de Argumento `None`) adicionando a verificação `if key.char is not None:` para garantir que a escrita no arquivo só ocorra para caracteres válidos.

#### ✅ Prova de Conceito: Captura de Teclas

> ![Salvando tudo](https://github.com/user-attachments/assets/12299a2c-969b-495a-b807-6ce5a1971e41)
> ![tudo que é digitado é gravado](https://github.com/user-attachments/assets/125f6bf5-9a77-457c-9b86-bf28c2bda70a)

 tudo que é digitado é gravado
>
> **Descrição:** O `keylogger.py` rodando em segundo plano e capturando as teclas digitadas em tempo real no arquivo `log.txt`.

---

## 🛡️ 5. Reflexão sobre Defesa (O Destaque do Projeto)

A jornada de implementação foi mais valiosa pela quantidade de desafios de ambiente que funcionaram como **lições práticas de segurança** e defesa:

### A. Isolamento de Dependências: A Lição do Kali Linux
* **O Desafio:** Ao tentar instalar bibliotecas, o Kali Linux gerou um erro (`externally-managed-environment`), bloqueando a instalação global.
* **A Defesa (Sandboxing):** A solução foi forçar a criação de um **Ambiente Virtual (`venv`)** com o comando `python3 -m venv venv_malware`.
* **Valor para a Defesa:** Isso demonstra a prática de **Isolamento de Código/Sandboxing**. Instalar dependências em ambientes virtuais garante que um código potencialmente malicioso (ou com muitas dependências) não corrompa o sistema operacional principal ou interfira em outros projetos.

### B. Permissões Elevadas (Privilégios Mínimos)
* **O Desafio:** O Keylogger (`pynput`) no Windows e no Kali falhou ao ser executado no terminal padrão.
* **A Defesa:** A solução foi rodar o terminal como **Administrador (`sudo` no Kali ou 'Executar como Administrador' no Windows)**.
* **Valor para a Defesa:** Isso reforça o princípio da **Concessão de Privilégios Mínimos**. O sistema operacional, por segurança, restringe que programas interajam com componentes críticos (como o teclado) sem a autorização explícita do usuário administrador.

### C. Conscientização e Backup (Ransomware)
* A defesa mais eficaz contra Ransomware é a conscientização (evitar phishing e anexos suspeitos) e, principalmente, a implementação de uma política robusta de **backup** (regra 3-2-1). O script de descriptografia só foi possível porque a "vítima" possuía a chave (o que simula ter o backup).

---

## 🔗 6. Entrega do Desafio

O projeto demonstra o sucesso na implementação do Ransomware, Keylogger e, o mais importante, a documentação das defesas aprendidas.

* **Link do Repositório GitHub:** https://github.com/Celsofigueiredomaciel/Desafio-de-Ciberseguran-a-Simula-o-e-Defesa-Contra-Ransomware-e-Keylogger-com-Python/blob/main/README.md
