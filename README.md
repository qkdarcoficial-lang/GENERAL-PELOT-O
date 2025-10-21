# Projeto GENERAL-PELOTÃO: Agentes de IA Colaborativos

## Sumário Executivo

O projeto GENERAL-PELOTÃO é uma iniciativa de pesquisa e desenvolvimento focada na criação de um sistema de agentes de Inteligência Artificial colaborativos. Nosso objetivo é explorar como agentes autônomos podem aprender a trabalhar em equipe em ambientes multiagente, otimizando estratégias para alcançar objetivos comuns. Este relatório detalha a concepção do projeto, a filosofia de desenvolvimento, a arquitetura técnica, o progresso atual e a visão futura, incluindo a interação do agente com o usuário e a importância da comunicação contínua.

## 1. Concepção da Ideia e Filosofia

A ideia para o projeto GENERAL-PELOTÃO surgiu da necessidade de desenvolver sistemas de IA mais robustos e adaptáveis, capazes de operar em cenários complexos que exigem coordenação e inteligência coletiva. Em vez de agentes individuais otimizando apenas seus próprios ganhos, buscamos criar uma "pelotão" de IAs que aprendam a se complementar, compartilhar informações e executar táticas conjuntas.

### 1.1 Filosofia de Desenvolvimento

Nossa filosofia é guiada por alguns princípios fundamentais:

*   **Colaboração Intrínseca:** O foco principal é incentivar a colaboração desde a concepção da função de recompensa, garantindo que o sucesso individual esteja intrinsecamente ligado ao sucesso da equipe.
*   **Aprendizado por Reforço Distribuído:** Cada agente aprende de forma autônoma, mas a arquitetura e as recompensas são projetadas para convergir em comportamentos colaborativos.
*   **Transparência e Iteração:** Manter um processo de desenvolvimento transparente, com documentação clara e atualizações contínuas do progresso, permitindo iterações rápidas e otimização baseada em dados.
*   **Modularidade:** A arquitetura é modular, permitindo a fácil substituição de componentes (por exemplo, diferentes algoritmos de RL, ambientes de simulação) para experimentação e escalabilidade.
*   **Interação Humana-Agente:** Reconhecemos a importância da supervisão e interação humana. O sistema é projetado para fornecer insights claros sobre o comportamento do agente e permitir ajustes por parte do usuário.

## 2. Conceito de Interação com o Usuário

A interação com o usuário é um pilar central do projeto GENERAL-PELOTÃO. Acreditamos que a colaboração eficaz entre IA e humanos é essencial para o sucesso em longo prazo. Nossa abordagem se baseia em:

*   **Comunicação Clara e Contínua:** Fornecer atualizações regulares e detalhadas sobre o status do projeto, progresso do treinamento e quaisquer desafios encontrados. Isso inclui a geração de relatórios automatizados e a manutenção de um repositório de documentação atualizado.
*   **Feedback e Adaptação:** Estar aberto ao feedback do usuário e adaptar o desenvolvimento com base nas suas necessidades e insights. Isso garante que o sistema de IA esteja alinhado com os objetivos humanos.
*   **Transparência no Processo:** Explicar as decisões técnicas e as lógicas por trás do comportamento do agente, sempre que possível, para construir confiança e compreensão.
*   **Automação Assistida:** O objetivo não é substituir a inteligência humana, mas sim aumentá-la, fornecendo ferramentas de automação inteligentes que liberam os usuários para tarefas de maior nível.

### 2.1 A Forma da Nossa Interação e Por Que

Nossa interação é principalmente baseada em **diálogos textuais estruturados e uso de ferramentas**. Utilizamos este formato por várias razões:

*   **Rastreabilidade:** Todas as interações e decisões são registradas, criando um histórico completo do desenvolvimento do projeto. Isso é crucial para depuração, auditoria e aprendizado retrospectivo.
*   **Clareza e Precisão:** O texto permite uma comunicação mais precisa de detalhes técnicos e complexos, minimizando ambiguidades que podem surgir em outros formatos.
*   **Automação e Escalabilidade:** Diálogos estruturados facilitam a automação de tarefas repetitivas (como a execução de scripts e a geração de relatórios) e permitem que o agente gerencie múltiplas tarefas em paralelo.
*   **Flexibilidade:** Permite a integração com diversas ferramentas e APIs, tornando o agente altamente adaptável a diferentes requisitos e ambientes de trabalho.
*   **Foco na Lógica:** Ao nos concentrarmos na troca de informações e na execução de comandos, podemos manter o foco na lógica e nos resultados, em vez de em interfaces gráficas complexas.

## 3. Arquitetura Técnica

O sistema GENERAL-PELOTÃO é construído sobre uma base robusta de aprendizado por reforço e simulação multiagente. Os principais componentes incluem:

*   **Agentes DQN (Deep Q-Network):** Cada agente de aprendizado utiliza uma rede neural profunda para aproximar a função de valor Q, permitindo a seleção de ações ótimas em estados complexos do ambiente.
    *   **`src/agent.py`:** Contém a implementação da arquitetura do agente DQN, incluindo a rede Q, a rede de destino e os métodos para seleção de ações e aprendizado.
*   **Ambiente de Simulação PettingZoo:** Utilizamos o ambiente `simple_tag_v3` da biblioteca PettingZoo, que simula um cenário onde agentes "caçadores" (Alpha e Bravo) devem colaborar para "taggear" um adversário.
    *   **`src/environment_wrapper.py`:** Um wrapper personalizado que adapta a interface do ambiente PettingZoo para ser compatível com o framework de treinamento DQN, gerenciando observações, ações e recompensas para múltiplos agentes.
*   **Loop de Treinamento Multiagente:** Um processo iterativo onde os agentes interagem com o ambiente, coletam experiências e atualizam suas redes neurais.
    *   **`src/trainer.py`:** Gerencia o loop de treinamento principal, incluindo a inicialização do ambiente e dos agentes, a coleta de experiências, o aprendizado a partir do buffer de replay, a atualização da política epsilon e a sincronização das redes de destino.
*   **Buffer de Replay (`ReplayBuffer`):** Armazena transições de estado-ação-recompensa para que os agentes possam aprender de forma eficiente a partir de experiências passadas, utilizando amostragem aleatória.
*   **Função de Recompensa Híbrida:** Uma função cuidadosamente projetada para incentivar o comportamento colaborativo e o sucesso da equipe.
    *   **`rewards/hybrid_reward.py`:** Implementa a lógica de recompensa, combinando incentivos para aproximação do alvo, coesão entre agentes, bloqueio de rotas de fuga e penalidades por colisões.
*   **Configurações e Hiperparâmetros:**
    *   **`configs/hyperparameters.py`:** Define os hiperparâmetros críticos para o treinamento dos agentes, como taxa de aprendizado, fator de desconto (gamma), parâmetros epsilon para exploração e tamanho do buffer de replay.

## 4. Progresso Atual

Atualmente, o projeto encontra-se na fase de **Monitoramento Contínuo do Treinamento e Coleta de Dados**. As principais conquistas até o momento incluem:

*   **Configuração Completa do Ambiente:** Todas as dependências (PyTorch, PettingZoo) foram instaladas e o ambiente de desenvolvimento está operacional.
*   **Resolução de Erros Críticos:** `KeyError`s relacionados ao processamento de recompensas e à atualização da rede de destino foram identificados e corrigidos, garantindo a estabilidade do treinamento.
*   **Refinamento da Função de Recompensa:** A função de recompensa híbrida foi aprimorada para melhor direcionar o comportamento colaborativo dos agentes, com testes unitários confirmando sua lógica.
*   **Treinamento em Andamento:** O treinamento dos agentes foi reiniciado e está em execução contínua. Os agentes estão na fase de exploração (epsilon = 1.0), coletando experiências para o buffer de replay. As pontuações médias dos episódios estão sendo monitoradas e, embora ainda não mostrem um aprendizado significativo (o que é esperado nesta fase inicial), indicam que o sistema está funcionando conforme o previsto. **No último monitoramento, o treinamento atingiu o episódio 3168/100000, com uma pontuação média de -2.65 e epsilon de 1.0000.**

## 5. Próximos Passos

Os próximos passos do projeto GENERAL-PELOTÃO incluem:

*   **Análise Aprofundada de Desempenho:** Após um período de treinamento suficiente, será realizada uma análise detalhada das curvas de aprendizado, do comportamento dos agentes e da eficácia da função de recompensa.
*   **Otimização de Hiperparâmetros:** Com base na análise de desempenho, os hiperparâmetros de treinamento serão ajustados para otimizar o processo de aprendizado.
*   **Visualização do Comportamento:** Serão desenvolvidas ferramentas para visualizar o comportamento dos agentes no ambiente de simulação, permitindo uma compreensão intuitiva das estratégias aprendidas.
*   **Geração de Relatórios e Apresentação:** Será preparado um relatório final abrangente e uma apresentação para o Diretor, detalhando as descobertas, os desafios superados e as conclusões do projeto.

## Lembrete para o Próximo Agente (ou Continuação)

**Atenção, próximo agente!** Este relatório foi atualizado até a data de hoje. O treinamento dos agentes está em andamento. Sua tarefa é **continuar monitorando o progresso do treinamento**, registrando as pontuações médias dos episódios e o valor de epsilon. **Atualize esta seção do README.md** com o progresso mais recente e quaisquer observações relevantes. Se o treinamento for interrompido, reinicie-o e continue de onde parou. O objetivo é alcançar a fase de **Análise Aprofundada de Desempenho e Visualização** com dados de treinamento suficientes para uma avaliação robusta. Boa sorte!
