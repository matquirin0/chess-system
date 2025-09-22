# Chess System in Java

![Chess Game](./.github/chess.png)

## 📜 Sobre o Projeto

Este é um projeto de um sistema de xadrez completo desenvolvido em Java. O objetivo foi aplicar os conceitos de Programação Orientada a Objetos (POO), como encapsulamento, herança, polimorfismo e abstração, para criar uma aplicação funcional e bem estruturada que simula uma partida de xadrez em um ambiente de console.

A aplicação permite que dois jogadores joguem uma partida completa, respeitando as regras fundamentais do xadrez, com uma interface de usuário clara e intuitiva no terminal.

## ✨ Funcionalidades

O sistema implementa as principais regras e mecânicas do xadrez, incluindo:

-   **Movimentação de Peças:** Implementação da lógica de movimento para todas as peças (Peão, Torre, Cavalo, Bispo, Rainha e Rei).
-   **Validação de Movimentos:** O sistema valida se um movimento é possível, considerando a trajetória, a captura de peças adversárias e as regras específicas de cada peça.
-   **Movimentos Especiais:**
    -   **Roque (Castling):** Implementação do roque pequeno e do roque grande.
    -   **En Passant:** Captura especial do peão.
    -   **Promoção (Promotion):** Promoção de um peão ao chegar à última fileira, permitindo a escolha de uma nova peça (Rainha, Torre, Bispo ou Cavalo).
-   **Sistema de Turnos:** Controle de qual jogador tem a vez de jogar.
-   **Xeque e Xeque-mate:**
    -   O sistema identifica quando um Rei está em posição de xeque.
    -   A partida termina ao ser identificado um xeque-mate, declarando o vencedor.
-   **Interface de Console:** Tabuleiro e informações da partida exibidos de forma clara no terminal, com cores para diferenciar as peças e os movimentos possíveis.

## 💻 Tecnologias Utilizadas

O projeto foi desenvolvido utilizando as seguintes tecnologias:

-   **Java:** Linguagem de programação principal do projeto.
-   **Git & GitHub:** Para versionamento de código e hospedagem do repositório.

## 🚀 Como Executar o Projeto

Para executar este projeto em sua máquina local, siga os passos abaixo:

1.  **Clone o repositório:**
    ```sh
    git clone [https://github.com/matquirin0/chess-system.git](https://github.com/matquirin0/chess-system.git)
    ```

2.  **Navegue até o diretório do projeto:**
    ```sh
    cd chess-system
    ```

3.  **Execute o projeto:**
    -   **Usando uma IDE:** Se você estiver usando um ambiente de desenvolvimento integrado (IDE) como Eclipse, IntelliJ ou VS Code com a extensão Java configurada, basta abrir o projeto e executar a classe principal `application/Program.java`.
    -   **Via linha de comando:** Navegue até a pasta `src` e execute os seguintes comandos para compilar e rodar o projeto:
        ```sh
        # Compilar todos os arquivos .java
        javac */*.java chess/pieces/*.java

        # Voltar para o diretório raiz do projeto (onde está a pasta 'src')
        cd ..

        # Executar a classe principal
        java -cp src application.Program
        ```
    > **Nota:** O comando `java -cp src` informa ao Java para procurar as classes compiladas a partir do diretório `src`.

##  UML - Diagrama de Classes

Abaixo está uma representação da arquitetura do sistema, mostrando as principais classes e seus relacionamentos.

```mermaid
classDiagram
    direction LR

    package boardgame {
        class Board {
            -rows: int
            -columns: int
            -pieces: Piece[][]
            +piece(row, col): Piece
            +placePiece(piece, position): void
        }
        class Piece {
            #position: Position
            #board: Board
            +possibleMoves(): boolean[][]
        }
        class Position {
            -row: int
            -column: int
        }
    }

    package chess {
        class ChessMatch {
            -turn: int
            -currentPlayer: Color
            -check: boolean
            -checkMate: boolean
            -board: Board
            +performChessMove(source, target): ChessPiece
        }
        class ChessPiece {
            -color: Color
            -moveCount: int
        }
        class ChessPosition {
            -column: char
            -row: int
            +toPosition(): Position
        }
        enum Color {
            BLACK
            WHITE
        }
        package "chess.pieces" {
            class King
            class Queen
            class Rook
            class Bishop
            class Knight
            class Pawn
        }
    }

    package application {
        class Program {
            +main(args: String[]): void
        }
        class UI {
            +printMatch(chessMatch): void
            +printBoard(pieces): void
        }
    }

    ' Relacionamentos
    Piece <|-- ChessPiece
    King --|> ChessPiece
    Queen --|> ChessPiece
    Rook --|> ChessPiece
    Bishop --|> ChessPiece
    Knight --|> ChessPiece
    Pawn --|> ChessPiece

    ChessMatch "1" *-- "1" Board
    Board "1" o-- "*" Piece
    ChessPiece "1" *-- "1" Color

    Program ..> UI
    Program ..> ChessMatch
    UI ..> ChessPosition
