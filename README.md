# 🗂️ Organizador de Arquivos

Script em Python que organiza automaticamente os arquivos de uma pasta em subpastas por tipo (Imagens, Documentos, Vídeos, Áudios, etc.).

## ✨ Funcionalidades

- Classifica arquivos pela extensão
- Modo simulação (`--simular`) para ver o resultado antes de mover
- Não sobrescreve arquivos com o mesmo nome
- Sem dependências externas (só biblioteca padrão)

## 🚀 Como usar

Requisitos: Python 3.8+

```bash
git clone https://github.com/guilhermedias-dev/organizador-de-arquivos.git
cd organizador-de-arquivos

# Primeiro, simule:
python organizador.py ~/Downloads --simular

# Depois, organize de verdade:
python organizador.py ~/Downloads
```

## 📁 Exemplo

Antes:
```
Downloads/
├── foto.png
├── curriculo.pdf
└── musica.mp3
```

Depois:
```
Downloads/
├── Imagens/foto.png
├── Documentos/curriculo.pdf
└── Audios/musica.mp3
```

## 🛠️ Conceitos praticados

`pathlib` · `shutil` · `argparse` · funções com type hints · tratamento de nomes duplicados

## 💡 Ideias para evoluir

- Organizar também por data
- Arquivo de configuração (JSON) para categorias personalizadas
- Desfazer a última organização
- Testes com `pytest`


