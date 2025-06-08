import re

# Saudação inicial
print('Hello!')
nome = input('Quem é você: ')
print('Olá', nome, 'seja bem-vindo!')

# Algoritmo de Luhn para validar o número do cartão
def luhn(numero):
    soma = 0
    alterna = False
    for digito in reversed(numero):
        d = int(digito)
        if alterna:
            d *= 2
            if d > 9:
                d -= 9
        soma += d
        alterna = not alterna
    return soma % 10 == 0

# Verifica a bandeira do cartão com base nos padrões
def identificar_bandeira(numero):
    bandeiras = {
        'Visa':      r'^4\d{12}(\d{3})?$',
        'MasterCard':r'^(5[1-5]\d{14}|2(2[2-9]|[3-6]\d|7[01])\d{12})$',
        'Amex':      r'^3[47]\d{13}$',
        'Discover':  r'^6(?:011|5\d{2})\d{12}$',
        'Elo':       r'^(4011(78|79)|431274|438935|451416|457393|504175|5067\d{2}|509\d{3}|627780|636297|636368|650\d{3}|6516\d{2}|6550\d{2})\d+$',
        'Hipercard': r'^(606282\d{10}(\d{3})?|3841\d{15})$',
        'Diners':    r'^3(0[0-5]|[68]\d)\d{11}$',
        'JCB':       r'^(352[89]|35[3-8][0-9])\d{12}$'
    }
    for nome, padrao in bandeiras.items():
        if re.match(padrao, numero):
            return nome
    return 'Desconhecida'

# Junta tudo: limpeza, identificação e validação
def validar_cartao(numero):
    numero = re.sub(r'\D', '', numero)  # Remove espaços, traços e outros caracteres não numéricos
    bandeira = identificar_bandeira(numero)
    valido = luhn(numero)
    return bandeira, valido

# Executa o programa
if __name__ == "__main__":
    numero = input("Digite o número do cartão (com ou sem espaços): ")
    bandeira, valido = validar_cartao(numero)

    if bandeira == 'Desconhecida':
        print("Bandeira não reconhecida.")
    else:
        print(f"Bandeira: {bandeira}")
        print("Cartão válido!" if valido else "Cartão inválido!")

# Fim do programa
#Usei o Copiloit para criar esse código, mas fiz algumas alterações para melhorar a legibilidade e a funcionalidade.Como por ecenplo desconsiderar o espaço, traços e outros caracteres não numéricos.'''
