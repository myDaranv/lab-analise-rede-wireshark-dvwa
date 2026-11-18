# 🛡️ Laboratório Prático: Análise de Tráfego de Rede e Captura de Credenciais com Wireshark

Neste repositório, estou documentando o passo a passo da execução prática do meu laboratório de análise de tráfego de rede e segurança em aplicações web. Utilizei um ambiente isolado no VirtualBox integrando o Kali Linux e uma máquina com a aplicação vulnerável **DVWA** (*Damn Vulnerable Web Application*), focando no uso do **Wireshark** para monitoramento e inspeção de pacotes.

---

## 💻 Ambiente que Utilizei
* **Máquina Atacante/Analista:** Kali Linux (`192.168.56.102`)
* **Máquina Alvo/Servidor Web:** Ambiente com DVWA (`192.168.56.101`)
* **Ferramentas:** Wireshark (Captura e Análise de Protocolos), Navegador Web.

---

## 🛠️ Passo a Passo do que Eu Fiz

### 1. Inicialização da Captura no Wireshark
* Abri o Wireshark no Kali Linux e selecionei a interface de rede ativa (`eth0`) para iniciar a escuta de todo o tráfego gerado no segmento de rede do laboratório (`192.168.56.x`)[cite: 19].

### 2. Acesso e Autenticação na Aplicação Vulnerável (DVWA)
* Naveguei até o endereço da aplicação (`http://192.168.56.101/dvwa/login.php`) e realizei o login utilizando as credenciais padrão (`admin / password`) com o nível de segurança ajustado para teste[cite: 18, 22].

### 3. Filtragem e Análise de Tráfego HTTP no Wireshark
* Para isolar o tráfego de autenticação gerado pelo formulário de login, apliquei um filtro específico de exibição no Wireshark:
  ```text
  http.request.method=="POST"O filtro destacou imediatamente a requisição enviada para o script de login (/dvwa/login.php).
  
    4. Inspeção de Dados Sensíveis em Texto PlanoAo expandir os detalhes do pacote capturado (Frame 27), analisei a estrutura da camada de aplicação HTTP e consegui visualizar claramente os dados do formulário preenchido (HTML Form URL Encoded):Usuário: admin   Senha: password
   Essa inspeção evidenciou como protocolos não criptografados expõem informações confidenciais para qualquer observador na mesma rede.
  🛡️ Lições Aprendidas e Alertas de SegurançaFazer este laboratório me mostrou na prática a importância de proteger os dados em trânsito.
   Aprendi que:Importância do HTTPS (Criptografia): Como o protocolo HTTP transmite dados em texto plano, qualquer atacante com acesso à rede consegue interceptar senhas e sessões usando sniffers como o Wireshark. O uso de SSL/TLS (HTTPS) é obrigatório para mascarar essas informações.Riscos de Redes Não Segmentadas:
  Em redes corporativas ou públicas sem isolamento adequado, o tráfego desprotegido fica vulnerável a ataques de escuta passiva.
  Visibilidade Defensiva: Da mesma forma que um invasor pode usar o Wireshark para capturar credenciais, profissionais de segurança defensiva utilizam a ferramenta para auditar redes, identificar conexões suspeitas e diagnosticar falhas de configuração.
