# N.E.X.U.S. — Android assistant starter

Projeto inicial Android nativo, compilável via GitHub Actions, pensado para evoluir para um assistente pessoal inspirado no JARVIS.

## Incluído nesta primeira entrega
- Interface escura futurista com navegação Chat / Image Studio / Config.
- Conversa por texto com endpoint compatível com OpenAI Chat Completions.
- Entrada por voz em português do Brasil usando o reconhecimento de fala disponível no Android.
- Resposta falada via Text-to-Speech do Android.
- Configuração de endpoint, modelo e chave de API na tela Config.
- Módulo Image Studio para preparar prompts de arte/mangá.
- Workflow GitHub Actions para compilar e publicar o APK como artifact.

## Limitações honestas desta versão
- O app ainda não tem controle geral do celular, wake word contínua, PIN próprio, memória de conversa persistente ou geração de imagens conectada. Esses recursos precisam de implementação e permissões/integradores específicos.
- O Image Studio cria e copia prompts; não gera a imagem ainda.
- O endpoint de chat precisa responder no formato `choices[0].message.content`.
- Não há APK pré-compilado neste pacote. O GitHub Actions compila o APK quando você executa o workflow.

## Requisitos
- Conta GitHub.
- Celular com navegador.
- Endpoint HTTPS de chat compatível com OpenAI Chat Completions.
- Para testes pessoais, uma chave de API pode ser informada em Config. **Não distribua um APK com uma chave embutida**: ela pode ser extraída. Para uso real, prefira um backend/proxy seu e mantenha a chave no servidor.

## Compilar usando somente o celular
1. Baixe e extraia o ZIP.
2. Entre em https://github.com e crie um repositório vazio chamado `NEXUS-Android`.
3. Envie os arquivos e pastas deste projeto para a raiz do repositório. Confira que `.github/workflows/android.yml` foi enviado.
4. Abra a aba **Actions** do repositório. Se solicitado, habilite GitHub Actions.
5. Selecione **Build N.E.X.U.S. Android APK** e toque em **Run workflow**. Também compila automaticamente em cada push para `main`.
6. Aguarde o workflow ficar verde. Abra a execução concluída, desça até **Artifacts** e baixe `NEXUS-debug-apk`.
7. Extraia o ZIP do artifact e instale `app-debug.apk`. O Android pode pedir autorização para instalar apps dessa origem.

## Configurar a IA
1. Obtenha um endpoint HTTPS de chat compatível com OpenAI Chat Completions.
2. Abra o N.E.X.U.S. > **CONFIG**.
3. Preencha o endpoint completo, modelo e chave (se seu endpoint exigir) e salve.
4. Volte ao CHAT e envie uma mensagem.
5. Se ocorrer erro HTTP, confira endpoint, modelo, saldo/cota do provedor e formato de resposta.

### Exemplo de formato esperado
`POST https://seu-servidor/v1/chat/completions`
Header: `Content-Type: application/json`
Header opcional: `Authorization: Bearer SUA_CHAVE`
Body:
`{"model":"seu-modelo","messages":[{"role":"system","content":"..."},{"role":"user","content":"Olá"}],"temperature":0.7}`

## Próximas fases recomendadas
1. Proxy seguro para a API e gerenciamento de segredos.
2. Memória local com opção de apagar dados.
3. Integrações Android específicas para abrir apps, alarmes e notificações.
4. Endpoint de geração de imagens e exibição dos resultados.
5. PIN/biometria e serviço de voz em primeiro plano, se necessário.
6. Testes em aparelhos reais e assinatura de release para distribuição.

## Privacidade
A fala pode ser processada pelo serviço de reconhecimento instalado no aparelho, dependendo da configuração Android. Não implemente escuta contínua sem indicação clara e consentimento. Use apenas permissões necessárias.
