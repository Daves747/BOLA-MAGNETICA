import time
import math

# Simulação de um jogador no jogo com função de bola magnética
class Jogador:
    def __init__(self, nome, posicao_x, posicao_y):
        self.nome = nome
        self.posicao_x = posicao_x
        self.posicao_y = posicao_y
        self.forca_magnetica = 1000  # Força magnética (pode ser ajustada)

    def atrair_bola(self, bola):
        """
        Função para atrair a bola para o jogador com base na força magnética.
        """
        # Cálculo da distância entre o jogador e a bola
        distancia_x = bola.posicao_x - self.posicao_x
        distancia_y = bola.posicao_y - self.posicao_y
        distancia = math.sqrt(distancia_x ** 2 + distancia_y ** 2)

        # Se a bola está dentro do alcance da atração (menor que 1000 unidades)
        if distancia < 1000:
            # Força de atração proporcional à distância
            forca_atracao = self.forca_magnetica / distancia

            # Movendo a bola em direção ao jogador
            bola.posicao_x -= forca_atracao * (distancia_x / distancia)
            bola.posicao_y -= forca_atracao * (distancia_y / distancia)
            print(f"Bola atraída para o jogador {self.nome}: ({bola.posicao_x}, {bola.posicao_y})")
        else:
            print("Bola está muito longe para ser atraída.")

class Bola:
    def __init__(self, posicao_x, posicao_y):
        self.posicao_x = posicao_x
        self.posicao_y = posicao_y

    def mostrar_posicao(self):
        print(f"Posição da Bola: ({self.posicao_x}, {self.posicao_y})")


# Função para simular o comportamento no jogo
def jogo():
    jogador = Jogador("Jogador 1", 0, 0)
    bola = Bola(500, 500)

    while True:
        bola.mostrar_posicao()  # Mostrar posição da bola
        jogador.atrair_bola(bola)  # Jogador tenta atrair a bola
        time.sleep(1)  # A cada segundo a bola se move em direção ao jogador

if __name__ == "__main__":
    jogo()
