import os

def limpa():
    os.system('cls' if os.name == 'nt' else 'clear')

while True:
    limpa()
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

    if op == "0":
        limpa()
        print("Tchau!")
        break

    # 1 - Cifra de César
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
                break

            if sub != "1" and sub != "2":
                continue

            limpa()
            texto = input("Texto: ")

            resultado = ""
            passo = 3 if sub == "1" else -3

            for letra in texto:
                if letra.isupper():
                    resultado += chr((ord(letra) + passo - 65) % 26 + 65)
                elif letra.islower():
                    resultado += chr((ord(letra) + passo - 97) % 26 + 97)
                else:
                    resultado += letra

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado)
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    # 2 - Rot-13
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
                    resultado += letra

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado)
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    # 3 - Código Morse
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
                for letra in texto.upper():
                    if letra in morse_dict:
                        resultado += morse_dict[letra] + " "
                    else:
                        resultado += " "

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
                partes = texto.split(" ")
                for parte in partes:
                    if parte in morse_dict:
                        resultado += morse_dict[parte]
                    elif parte == "":
                        resultado += " "

            limpa()
            print("Resultado:")
            print("------------------------")
            print(resultado.strip())
            print("------------------------")
            input("Precione qualquer tecla para continuar...")

    else:
        limpa()
        print("Opção errada")
        input("Precione qualquer tecla para continuar...")
