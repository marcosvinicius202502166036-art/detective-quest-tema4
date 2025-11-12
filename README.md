# detective-quest-tema4
Projeto em linguagem C desenvolvido para o Desafio Detective Quest – Tema 4 (Estrutura de Dados – Estácio)
detective-quest-tema4/
│
├── detective_quest.py      # Código principal
├── main.py                 # Arquivo para executar o programa
├── README.md               # Explicação do projeto
└── .gitignore              # (opcional)
# detective_quest.py

class Room:
    def __init__(self, name):
        self.name = name
        self.left = None
        self.right = None

class MansionMap:
    def __init__(self):
        self.root = None

    def insert(self, name):
        """Insere um novo cômodo na árvore"""
        if self.root is None:
            self.root = Room(name)
        else:
            self._insert_recursive(self.root, name)

    def _insert_recursive(self, current, name):
        if name < current.name:
            if current.left is None:
                current.left = Room(name)
            else:
                self._insert_recursive(current.left, name)
        elif name > current.name:
            if current.right is None:
                current.right = Room(name)
            else:
                self._insert_recursive(current.right, name)

    def search(self, name):
        """Busca um cômodo pelo nome"""
        return self._search_recursive(self.root, name)

    def _search_recursive(self, current, name):
        if current is None:
            return None
        if current.name == name:
            return current
        elif name < current.name:
            return self._search_recursive(current.left, name)
        else:
            return self._search_recursive(current.right, name)

    def show_map(self):
        """Mostra o mapa da mansão em ordem"""
        print("Mapa da Mansão (em ordem):")
        self._inorder(self.root)

    def _inorder(self, current):
        if current:
            self._inorder(current.left)
            print(f" - {current.name}")
            self._inorder(current.right)
# main.py
from detective_quest import MansionMap

def main():
    mansion = MansionMap()

    print("=== Detective Quest: Mapa da Mansão ===")

    # Inserindo cômodos
    mansion.insert("Sala Principal")
    mansion.insert("Cozinha")
    mansion.insert("Biblioteca")
    mansion.insert("Jardim")
    mansion.insert("Escritório")

    # Mostrando o mapa
    mansion.show_map()

    # Buscando um cômodo
    search_room = input("\nDigite o nome do cômodo que deseja procurar: ")
    room = mansion.search(search_room)

    if room:
        print(f"O cômodo '{room.name}' foi encontrado!")
    else:
        print(f"O cômodo '{search_room}' não foi encontrado.")

if __name__ == "__main__":
    main()
# 🕵️ Detective Quest – Tema 4

Projeto desenvolvido para a disciplina **Estrutura de Dados** da Estácio.

## 🎯 Objetivo
Implementar uma **árvore binária** que representa o mapa da mansão do jogo *Detective Quest*.  
Cada nó da árvore é um cômodo, e as ligações representam as conexões entre eles.

## 🧱 Estrutura
- **Room** → representa um cômodo.
- **MansionMap** → estrutura de árvore binária que organiza os cômodos.
- **main.py** → executa o programa e demonstra as funções.

## ⚙️ Funcionalidades
- Inserção de cômodos.
- Busca por cômodo.
- Exibição do mapa completo (em ordem).

## 🚀 Como executar
1. Clone o repositório:
   ```bash
   git clone https://github.com/SEU_USUARIO/detective-quest-tema4.git
