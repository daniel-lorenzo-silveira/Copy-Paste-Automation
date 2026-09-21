import time
import pyperclip
import pyautogui

# Desativa parada brusca para movimentos rápidos
pyautogui.FAILSAFE = False

# ==============================================================================
# CONFIGURAÇÕES
# ==============================================================================
TOTAL_AUDIOS = 15          # Quantidade de caixas no lote
TABS_ENTRE_CAIXAS = 29     # Quantidade de TABs para saltar entre caixas
DELIMITADOR = " ;;"

PROMPT_INICIAL = (
    ""      
)

print("=========================================================")
print("🎯 COLETA RIGOROSA EM ORDEM (1 A 15)")
print("=========================================================")
print("1. Clique DENTRO da PRIMEIRA caixa de texto de transcrição (#1).")
print("2. Pressione ENTER aqui no terminal...")
input()

print("\n⏳ Alternando... A coleta iniciará em 3 segundos!")
time.sleep(3)

lote_textos = []

for i in range(1, TOTAL_AUDIOS + 1):
    # 1. Limpa o Clipboard antes de copiar o item atual
    pyperclip.copy("")
    time.sleep(0.05)
    
    # 2. Seleciona e copia o texto do campo ativo
    pyautogui.hotkey('ctrl', 'a')
    time.sleep(0.1)
    pyautogui.hotkey('ctrl', 'c')
    time.sleep(0.1)
    
    # 3. Pega o texto capturado
    texto = pyperclip.paste().strip()
    
    # Caso a caixa esteja vazia ou o Ctrl+C falhe, registra aviso
    if not texto:
        texto_capturado = "[CAIXA VAZIA OU FALHA DE COPIA]"
    else:
        texto_capturado = texto
    
    # Adiciona à lista garantindo a posição exata
    lote_textos.append(f"{texto_capturado}{DELIMITADOR}")
    
    # Exibe no terminal a ordem exata para você acompanhar
    print(f"  [Item {i:02d}/15] -> {texto_capturado[:45]}")
    
    # 4. Navegação para a próxima caixa via TAB (com cadência para não perder o foco)
    if i < TOTAL_AUDIOS:
        for _ in range(TABS_ENTRE_CAIXAS):
            pyautogui.press('tab')
            time.sleep(0.025)  # Pausa segura para o navegador processar cada TAB
            
        time.sleep(0.15)  # Pausa para estabilizar o foco na nova caixa

# Monta o prompt final na ordem exata de captura (do 1º ao 15º)
prompt_final = PROMPT_INICIAL + "\n".join(lote_textos)
pyperclip.copy(prompt_final)

print("\n=========================================================")
print(f"🎉 CONCLUÍDO! Os {len(lote_textos)} itens foram organizados em ordem estrita!")
print("👉 Vá até a IA (Gemini) e pressione Ctrl + V para conferir e enviar.")
print("=========================================================")
