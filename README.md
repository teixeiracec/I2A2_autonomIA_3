# Desafio I2A2: Análise de CSV

## Mini-tutorial sobre a criação de Agente de IA para análise de arquivos CSV zipados (para ser utilizado localmente em ambiente Windows)

1. No chatGPT 4o, realizar o upload dos arquivos a serem analisados e inserir o seguinte prompt:
Now, you are a GenAI Application Engineer. Analyze these uploaded CSV files. Create one (or more, if necessary) agents that allow a user to ask questions about the uploaded CSV files provided. The agent mode of operation includes: an interface where the user enters his/her question and the agent(s) generates the response; the agent(s) must unzip the files, select the desired file, load the data, perform the queries and generate the response for the user. Technologies like Python scripts or LowCode/NoCode tools can be used (I prefer Python-based ones). We must use at least 1 of the following frameworks/tools: • https://autogenhub.github.io/autogen/ • https://ai.pydantic.dev/ • https://www.langchain.com/ • https://www.llamaindex.ai/ • https://www.crewai.com/ • https://n8n.io/ • https://www.langflow.org/. Give me the whole architecture, as well as a step by step guide to deploy the agent(s).

2. Resposta da LLM

2.1 Visão Geral dos Arquivos CSV
O arquivo compactado (202401_NFs.zip) contém:

•	202401_NFs_Cabecalho.csv: metadados das notas fiscais, como:
o	Chave de acesso, CNPJ, data de emissão, valor total, UF etc.
•	202401_NFs_Itens.csv: itens vendidos ou movimentados nas notas:
o	Produtos, quantidade, CFOP, NCM, valores unitários e totais

Esses dois arquivos se relacionam pela "Chave de Acesso", possibilitando consultas por perguntas em linguagem natural com contexto cruzado.

2.2 Arquitetura da Solução (LangChain + Streamlit + OpenAI)

![image](https://github.com/user-attachments/assets/ece5e0c1-ce12-4ef6-9762-464a690f0dbe)

2.3 Ferramenta utilizada: LangChain
•	Usada diretamente para criar o agente de consulta baseado em arquivos CSV.
•	O agente criado (create_csv_agent) pertence ao módulo langchain_experimental.agents.
•	Permite que perguntas em linguagem natural sejam transformadas em operações reais sobre os dados com apoio de um LLM (modelo de linguagem como o da OpenAI).

2.4 Arquivos e Estrutura do Projeto
A LLM forneceu os arquivos main.py (com o código python que conversa com a LLM) e requirements.txt (que apresenta todos os pacotes com instalação requerida). Ambos os arquivos podem ser abertos e editados em um editor de texto.
A LLM também fornece um arquivo .env, o qual você deverá editar, inserindo sua chave da openAI. Este arquivo também pode ser aberto e editado em um editor de texto.

3. Obtenha uma chave da OpenAI
•	Acesse: https://platform.openai.com/signup
•	Crie uma conta (pode usar Google ou Microsoft)
•	Vá em https://platform.openai.com/api-keys
•	Clique em “Create new secret key”
•	Copie a chave (sk-xxxxxxxxxxxxxxxx) e salve com segurança

3.1 Como usar a chave da OpenAI?
Na pasta do projeto, edite o arquivo .env, inserindo sua chave:
OPENAI_API_KEY=sk-sua-chave-aqui

4. Estrutura do projeto
Ao final, no seu computador, a estrutura do projeto deve ficar assim:

csv_agent_full_app/        #uma pasta
├── main.py
├── .env
├── requirements.txt
└── data/                  #uma pasta
    └── 202401_NFs.zip

5. Baixe e instale o Anaconda
Anaconda?
Anaconda é uma plataforma livre e de código aberto que facilita o uso da linguagem de programação Python, especialmente em projetos de ciência de dados, inteligência artificial, análise estatística e aprendizado de máquina.
Seu principal objetivo é simplificar a instalação, o gerenciamento de pacotes e a criação de ambientes isolados, evitando conflitos entre projetos e promovendo maior organização no desenvolvimento de soluções baseadas em dados.

Por que usar o Anaconda?
Ao instalar o Anaconda, o usuário já recebe:
•	O interpretador Python pronto para uso
•	Centenas de bibliotecas populares (como pandas, numpy, matplotlib, scikit-learn, tensorflow, entre outras)
•	O Conda, um gerenciador de pacotes e ambientes virtuais
•	Interfaces gráficas como o Anaconda Navigator e o Jupyter Notebook, que facilitam o trabalho mesmo para quem não domina o terminal

Exemplo de uso no projeto
Neste projeto, o Anaconda foi/será utilizado para:
•	Criar um ambiente virtual chamado nfagent, dedicado exclusivamente à execução do agente de inteligência artificial
•	Instalar pacotes como streamlit, langchain, openai, pandas e outros, sem afetar outras instalações do sistema
•	Garantir reprodutibilidade e segurança durante a análise dos arquivos CSV compactados das Notas Fiscais
Em resumo: "Anaconda é como um kit completo que instala o Python e tudo que você precisa para trabalhar com dados — de forma organizada, segura e eficiente."

6. Crie um ambiente virtual Conda

•	Abra o Anaconda Prompt e vá até a pasta do projeto:
exemplo: cd \Users\Você\Documents\agentes\csv_agent_full_app

•	Na pasta csv_agent_full_app, crie um ambiente virtual Conda:
conda create --name nfagent python=3.11
conda activate nfagent

•	Instale as dependências:
pip install -r requirements.txt

7. Como executar o agente localmente?
No Anaconda Prompt, com o ambiente nfagent ativado, execute:
streamlit run main.py
O navegador será aberto com a interface do agente.

7.1 Exemplos do que você pode perguntar ao Agente
•	"Qual o valor total das notas emitidas para SP?"
•	"Quais produtos foram mais vendidos em janeiro?"
•	"Quantas notas foram emitidas por cada CNPJ?"
•	"Qual a soma dos itens com NCM 22011000?"
•	"Qual o total de notas destinadas ao DF?"

8. Como encerrar o agente?
Na interface Web, clique no botão 🛑 Encerrar Agente

9. Manutenção e segurança
•	Ambientes isolados: mantenha o agente em ambiente Conda separado.
•	Evite expor sua chave da OpenAI em lugares públicos. 
