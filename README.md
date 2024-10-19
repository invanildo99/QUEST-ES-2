# QUEST-ES-2
LOGICA E TECNICA DE PROGRAMAÇÃO
QUESTÃO 1: Observe o trecho de código abaixo: int INDICE = 13, SOMA = 0, K = 0;
Enquanto K < INDICE faça { K = K + 1; SOMA = SOMA + K; }
Imprimir(SOMA);
Ao final do processamento, qual será o valor da variável SOMA? 

R=91


QUESTÃO 2:Dado a sequência de Fibonacci, onde se inicia por 0 e 1 e o próximo valor sempre será a soma dos 2 valores anteriores (exemplo: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...), escreva um programa na linguagem que desejar onde, informado um número, ele calcule a sequência de Fibonacci e retorne uma mensagem avisando se o número informado pertence ou não a sequência.

IMPORTANTE: Esse número pode ser informado através de qualquer entrada de sua preferência ou pode ser previamente definido no código; 
def fibonacci_sequence(n):
    # Iniciando a sequência com os dois primeiros números
    fib_sequence = [0, 1]
    
    # Calculando a sequência de Fibonacci até o número informado
    while True:
        next_fib = fib_sequence[-1] + fib_sequence[-2]
        if next_fib > n:
            break
        fib_sequence.append(next_fib)
    
    return fib_sequence

def main():
    # Número previamente definido
    number = 21  # Você pode alterar este número para testar

    # Ou, caso queira permitir entrada do usuário, use:
    # number = int(input("Informe um número: "))
    
    # Obtendo a sequência de Fibonacci
    fib_sequence = fibonacci_sequence(number)
    
    # Exibindo a sequência
    print(f"Séquence de Fibonacci até {number}: {fib_sequence}")
    
    # Verificando se o número informado pertence à sequência
    if number in fib_sequence:
        print(f"O número {number} pertence à sequência de Fibonacci.")
    else:
        print(f"O número {number} NÃO pertence à sequência de Fibonacci.")

# Executando o programa
if __name__ == "__main__":
    main()


QUESTÃO 3: Dado um vetor que guarda o valor de faturamento diário de uma distribuidora, faça um programa, na linguagem que desejar, que calcule e retorne:
• O menor valor de faturamento ocorrido em um dia do mês;
• O maior valor de faturamento ocorrido em um dia do mês;
• Número de dias no mês em que o valor de faturamento diário foi superior à média mensal.

IMPORTANTE:
a) Usar o json ou xml disponível como fonte dos dados do faturamento mensal;
b) Podem existir dias sem faturamento, como nos finais de semana e feriados. Estes dias devem ser ignorados no cálculo da média; 
JSON
{
    "faturamento": [
        {"dia": 1, "valor": 200.50},
        {"dia": 2, "valor": 300.00},
        {"dia": 3, "valor": 0.00},
        {"dia": 4, "valor": 150.25},
        {"dia": 5, "valor": 400.00},
        {"dia": 6, "valor": 0.00},
        {"dia": 7, "valor": 500.00},
        {"dia": 8, "valor": 600.00},
        {"dia": 9, "valor": 700.00},
        {"dia": 10, "valor": 0.00},
        {"dia": 11, "valor": 800.00},
        {"dia": 12, "valor": 250.00},
        {"dia": 13, "valor": 0.00},
        {"dia": 14, "valor": 0.00},
        {"dia": 15, "valor": 450.00},
        {"dia": 16, "valor": 650.00},
        {"dia": 17, "valor": 750.00},
        {"dia": 18, "valor": 0.00},
        {"dia": 19, "valor": 300.00},
        {"dia": 20, "valor": 0.00},
        {"dia": 21, "valor": 1000.00},
        {"dia": 22, "valor": 1200.00},
        {"dia": 23, "valor": 0.00},
        {"dia": 24, "valor": 400.00},
        {"dia": 25, "valor": 300.00},
        {"dia": 26, "valor": 0.00},
        {"dia": 27, "valor": 600.00},
        {"dia": 28, "valor": 700.00},
        {"dia": 29, "valor": 800.00},
        {"dia": 30, "valor": 0.00}
    ]
}

PYTHON
import json

def carregar_dados(fichero):
    with open(fichero, 'r') as file:
        data = json.load(file)
    return data["faturamento"]

def calcular_faturamento(faturamento):
    valores = [item['valor'] for item in faturamento if item['valor'] > 0]
    
    if not valores:
        return None, None, 0  # Se não houver faturamento, retorna None e 0
    
    menor_faturamento = min(valores)
    maior_faturamento = max(valores)
    
    media_mensal = sum(valores) / len(valores)
    
    dias_acima_media = sum(1 for valor in valores if valor > media_mensal)

    return menor_faturamento, maior_faturamento, dias_acima_media

def main():
    # Carregando dados do arquivo JSON
    faturamento = carregar_dados('faturamento.json')
    
    menor_faturamento, maior_faturamento, dias_acima_media = calcular_faturamento(faturamento)
    
    if menor_faturamento is not None:
        print(f"Menor faturamento: R${menor_faturamento:.2f}")
        print(f"Maior faturamento: R${maior_faturamento:.2f}")
        print(f"Número de dias com faturamento acima da média mensal: {dias_acima_media}")
    else:
        print("Não há dados de faturamento para calcular.")

if __name__ == "__main__":
    main()



QUESTÃO 4:  Dado o valor de faturamento mensal de uma distribuidora, detalhado por estado:
• SP – R$67.836,43
• RJ – R$36.678,66
• MG – R$29.229,88
• ES – R$27.165,48
• Outros – R$19.849,53

Escreva um programa na linguagem que desejar onde calcule o percentual de representação que cada estado teve dentro do valor total mensal da distribuidora.  

def calcular_percentuais(faturamento):
    total_faturamento = sum(faturamento.values())
    percentuais = {estado: (valor / total_faturamento) * 100 for estado, valor in faturamento.items()}
    return percentuais, total_faturamento

def main():
    # Faturamento mensal por estado
    faturamento = {
        "SP": 67836.43,
        "RJ": 36678.66,
        "MG": 29229.88,
        "ES": 27165.48,
        "Outros": 19849.53
    }
    
    # Calculando os percentuais
    percentuais, total_faturamento = calcular_percentuais(faturamento)

    # Exibindo os resultados
    print(f"Faturamento Total: R${total_faturamento:.2f}\n")
    print("Percentual de representação por estado:")
    for estado, percentual in percentuais.items():
        print(f"{estado}: {percentual:.2f}%")

if __name__ == "__main__":
    main()


QUESTÃO 5: Escreva um programa que inverta os caracteres de um string.

IMPORTANTE:
a) Essa string pode ser informada através de qualquer entrada de sua preferência ou pode ser previamente definida no código;
b) Evite usar funções prontas, como, por exemplo, reverse;

def inverter_string(s):
    # Inicializa uma string vazia para armazenar o resultado
    string_invertida = ''
    
    # Percorre a string original de trás para frente
    for i in range(len(s) - 1, -1, -1):
        string_invertida += s[i]  # Adiciona cada caractere à nova string
    
    return string_invertida

def main():
    # String previamente definida
    # string_original = "Hello, World!"
    
    # Ou, permitindo entrada do usuário
    string_original = input("Informe uma string para inverter: ")
    
    # Invertendo a string
    resultado = inverter_string(string_original)
    
    # Exibindo o resultado
    print(f"String original: {string_original}")
    print(f"String invertida: {resultado}")

# Executando o programa
if __name__ == "__main__":
    main()

