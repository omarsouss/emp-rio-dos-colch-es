import math
import random

class JogoDaVelha:
    def __init__(self):
        self.tabuleiro = [[' ' for _ in range(3)] for _ in range(3)]
        self.jogador_humano = 'X'
        self.jogador_ia = 'O'
    
    def imprimir_tabuleiro(self):
        print("\n   0   1   2")
        for i in range(3):
            print(f"{i}  {self.tabuleiro[i][0]} | {self.tabuleiro[i][1]} | {self.tabuleiro[i][2]} ")
            if i < 2:
                print("  -----------")
    
    def fazer_jogada(self, linha, coluna, jogador):
        if self.tabuleiro[linha][coluna] == ' ':
            self.tabuleiro[linha][coluna] = jogador
            return True
        return False
    
    def verificar_vencedor(self):
        # Verificar linhas
        for linha in self.tabuleiro:
            if linha[0] == linha[1] == linha[2] != ' ':
                return linha[0]
        
        # Verificar colunas
        for col in range(3):
            if self.tabuleiro[0][col] == self.tabuleiro[1][col] == self.tabuleiro[2][col] != ' ':
                return self.tabuleiro[0][col]
        
        # Verificar diagonais
        if self.tabuleiro[0][0] == self.tabuleiro[1][1] == self.tabuleiro[2][2] != ' ':
            return self.tabuleiro[0][0]
        if self.tabuleiro[0][2] == self.tabuleiro[1][1] == self.tabuleiro[2][0] != ' ':
            return self.tabuleiro[0][2]
        
        return None
    
    def tabuleiro_cheio(self):
        for linha in self.tabuleiro:
            if ' ' in linha:
                return False
        return True
    
    def minimax(self, profundidade, is_maximizing):
        # Verificar estados terminais
        vencedor = self.verificar_vencedor()
        
        if vencedor == self.jogador_ia:
            return 1
        elif vencedor == self.jogador_humano:
            return -1
        elif self.tabuleiro_cheio():
            return 0
        
        # Algoritmo Minimax
        if is_maximizing:
            melhor_valor = -math.inf
            for i in range(3):
                for j in range(3):
                    if self.tabuleiro[i][j] == ' ':
                        self.tabuleiro[i][j] = self.jogador_ia
                        valor = self.minimax(profundidade + 1, False)
                        self.tabuleiro[i][j] = ' '
                        melhor_valor = max(valor, melhor_valor)
            return melhor_valor
        else:
            melhor_valor = math.inf
            for i in range(3):
                for j in range(3):
                    if self.tabuleiro[i][j] == ' ':
                        self.tabuleiro[i][j] = self.jogador_humano
                        valor = self.minimax(profundidade + 1, True)
                        self.tabuleiro[i][j] = ' '
                        melhor_valor = min(valor, melhor_valor)
            return melhor_valor
    
    def melhor_jogada_ia(self):
        melhor_valor = -math.inf
        melhor_movimento = None
        
        # Testar todas as posições vazias
        for i in range(3
