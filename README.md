import os

# Limpa o ecrã — funciona tanto no Windows (cls) como no Linux/Mac (clear)
def limpa():
    os.system('cls' if os.name == 'nt' else 'clear')

# Loop principal — o programa fica a correr até o utilizador escolher sair
while True:
    limpa()
    # Menu principal
    print("╔══════════════════════════════╗")
    print("║   Codificar / Descodificar   ║")
    print("╚══════════════════════════════╝")
    print()
    print("1 → Cifra de César")
    print("2 → Rot-13")
    print("3 → Código Morse")
    print("0 → Sair")
    print()
    op = input("→ ")

    # Sair do programa
    if op == "0":
        limpa()
        print("Tchau!")
        break

    # ─────────────────────────────────────
    # OPÇÃO 1 — Cifra de César
    # Desloca cada letra 3 posições no alfabeto
    # ─────────────────────────────────────
    if op == "1":
        while True:
            limpa()
            print("CIFRA DE CÉSAR")
            print("1 → Codificar")
            print("2 → Descodificar")
            print("0 → Voltar")
            print()
            sub = input("→ ")

            if sub == "0":
                break  # Volta ao menu principal

            if sub != "1" and sub != "2":
                continue  # Opção inválida, pede de novo

            limpa()
            texto = input("Texto: ")

            resultado = ""
            passo = 3 if sub == "1" else -3  # +3 para codificar, -3 para descodificar

            for letra in texto:
                if letra.isupper():
                    # Desloca letra maiúscula, com wrap usando % 26
                    resultado += chr((ord(letra) + passo - 65) % 26 + 65)
                elif letra.islower():
                    # Desloca letra minúscula, com wrap usando % 26
                    resultado += chr((ord(letra) + passo - 97) % 26 + 97)
                else:
                    resultado += letra  # Espaços e símbolos ficam iguais

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado)
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    # ─────────────────────────────────────
    # OPÇÃO 2 — ROT-13
    # Igual à César mas sempre com passo 13
    # Codificar e descodificar são a mesma operação
    # ─────────────────────────────────────
    elif op == "2":
        while True:
            limpa()
            print("ROT-13")
            print("1 → Codificar")
            print("2 → Descodificar")
            print("0 → Voltar")
            print()
            sub = input("→ ")

            if sub == "0":
                break

            if sub != "1" and sub != "2":
                continue

            limpa()
            texto = input("Texto: ")

            resultado = ""
            for letra in texto:
                if letra.isupper():
                    resultado += chr((ord(letra) + 13 - 65) % 26 + 65)
                elif letra.islower():
                    resultado += chr((ord(letra) + 13 - 97) % 26 + 97)
                else:
                    resultado += letra  # Espaços e símbolos ficam iguais

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado)
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    # ─────────────────────────────────────
    # OPÇÃO 3 — Código Morse
    # Converte texto → morse ou morse → texto
    # ─────────────────────────────────────
    elif op == "3":
        while True:
            limpa()
            print("CÓDIGO MORSE")
            print("1 → Codificar")
            print("2 → Descodificar")
            print("0 → Voltar")
            print()
            sub = input("→ ")

            if sub == "0":
                break

            if sub != "1" and sub != "2":
                continue

            limpa()
            texto = input("Texto: ")

            # Codificar: texto → morse
            if sub == "1":
                morse_dict = {
                    'A': '.-', 'B': '-...', 'C': '-.-.', 'D': '-..', 'E': '.',
                    'F': '..-.', 'G': '--.', 'H': '....', 'I': '..', 'J': '.---',
                    'K': '-.-', 'L': '.-..', 'M': '--', 'N': '-.', 'O': '---',
                    'P': '.--.', 'Q': '--.-', 'R': '.-.', 'S': '...', 'T': '-',
                    'U': '..-', 'V': '...-', 'W': '.--', 'X': '-..-', 'Y': '-.--',
                    'Z': '--..', '0': '-----', '1': '.----', '2': '..---',
                    '3': '...--', '4': '....-', '5': '.....', '6': '-....',
                    '7': '--...', '8': '---..', '9': '----.', ' ': '   '
                }

                resultado = ""
                for letra in texto.upper():  # Converte tudo para maiúsculas
                    if letra in morse_dict:
                        resultado += morse_dict[letra] + " "  # Adiciona código + espaço
                    else:
                        resultado += " "  # Caracteres desconhecidos viram espaço

            # Descodificar: morse → texto
            else:
                morse_dict = {
                    '.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E',
                    '..-.': 'F', '--.': 'G', '....': 'H', '..': 'I', '.---': 'J',
                    '-.-': 'K', '.-..': 'L', '--': 'M', '-.': 'N', '---': 'O',
                    '.--.': 'P', '--.-': 'Q', '.-.': 'R', '...': 'S', '-': 'T',
                    '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X', '-.--': 'Y',
                    '--..': 'Z', '-----': '0', '.----': '1', '..---': '2',
                    '...--': '3', '....-': '4', '.....': '5', '-....': '6',
                    '--...': '7', '---..': '8', '----.': '9', '': ' '
                }

                resultado = ""
                partes = texto.split(" ")  # Divide o morse por espaços
                for parte in partes:
                    if parte in morse_dict:
                        resultado += morse_dict[parte]  # Traduz o código para letra
                    elif parte == "":
                        resultado += " "  # Espaço duplo entre palavras vira espaço

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado.strip())  # .strip() remove espaços no início e fim
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    # Opção inválida no menu principal
    else:
        limpa()
        print("Opção errada")
        input("Precione qualquer tecla para continuar...")
