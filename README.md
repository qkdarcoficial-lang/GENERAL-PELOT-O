# GENERAL-PELOTÃO

Este repositório contém o projeto para o desenvolvimento de agentes de IA colaborativos no ambiente PettingZoo, seguindo o Protocolo do General.

## Estrutura do Projeto (Esqueleto)

- `src/`: Contém o código dos agentes e do loop de treinamento.
- `environments/`: Adaptações do ambiente PettingZoo.
- `models/`: Modelos de agentes treinados.
- `configs/`: Arquivos de configuração.
- `rewards/`: Funções de recompensa personalizadas.

## Configuração

Para configurar o ambiente, execute:
```bash
pip install -r requirements.txt
```

## Treinamento

Para iniciar o treinamento, execute:
```bash
python src/train.py
```

