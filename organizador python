"""
Organizador de Arquivos
-----------------------
Organiza os arquivos de uma pasta em subpastas por tipo
(Imagens, Documentos, Vídeos, etc.).

Uso:
    python organizador.py CAMINHO_DA_PASTA
    python organizador.py CAMINHO_DA_PASTA --simular
"""

import argparse
import shutil
from pathlib import Path

# Mapeia cada categoria às extensões que pertencem a ela
CATEGORIAS = {
    "Imagens": [".jpg", ".jpeg", ".png", ".gif", ".bmp", ".svg", ".webp"],
    "Documentos": [".pdf", ".doc", ".docx", ".txt", ".odt", ".pptx", ".xlsx", ".csv"],
    "Videos": [".mp4", ".mkv", ".avi", ".mov"],
    "Audios": [".mp3", ".wav", ".flac", ".ogg"],
    "Compactados": [".zip", ".rar", ".7z", ".tar", ".gz"],
    "Codigos": [".py", ".js", ".html", ".css", ".java", ".c", ".cpp", ".json"],
}


def descobrir_categoria(arquivo: Path) -> str:
    """Retorna a categoria do arquivo com base na extensão."""
    extensao = arquivo.suffix.lower()
    for categoria, extensoes in CATEGORIAS.items():
        if extensao in extensoes:
            return categoria
    return "Outros"


def gerar_destino_unico(destino: Path) -> Path:
    """Evita sobrescrever: se já existir, adiciona (1), (2), ..."""
    contador = 1
    novo = destino
    while novo.exists():
        novo = destino.with_name(f"{destino.stem} ({contador}){destino.suffix}")
        contador += 1
    return novo


def organizar(pasta: Path, simular: bool = False) -> int:
    """Move os arquivos para subpastas. Retorna quantos foram processados."""
    total = 0

    for arquivo in pasta.iterdir():
        # Ignora subpastas e arquivos ocultos
        if not arquivo.is_file() or arquivo.name.startswith("."):
            continue

        categoria = descobrir_categoria(arquivo)
        pasta_destino = pasta / categoria
        destino = gerar_destino_unico(pasta_destino / arquivo.name)

        if simular:
            print(f"[SIMULAÇÃO] {arquivo.name} -> {categoria}/")
        else:
            pasta_destino.mkdir(exist_ok=True)
            shutil.move(str(arquivo), str(destino))
            print(f"Movido: {arquivo.name} -> {categoria}/")

        total += 1

    return total


def main():
    parser = argparse.ArgumentParser(description="Organiza arquivos por tipo.")
    parser.add_argument("pasta", help="Caminho da pasta a ser organizada")
    parser.add_argument(
        "--simular",
        action="store_true",
        help="Mostra o que seria feito, sem mover nada",
    )
    args = parser.parse_args()

    pasta = Path(args.pasta).expanduser()

    if not pasta.is_dir():
        print(f"Erro: '{pasta}' não é uma pasta válida.")
        return

    total = organizar(pasta, args.simular)
    print(f"\nConcluído! {total} arquivo(s) processado(s).")


if __name__ == "__main__":
    main()
