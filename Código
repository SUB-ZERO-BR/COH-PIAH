import re
from itertools import chain

def le_assinatura():
    '''A funcao le os valores dos tracos linguisticos do modelo e devolve uma assinatura a ser comparada com os textos fornecidos'''
    print("Bem-vindo ao detector automático de COH-PIAH.")
    print("Informe a assinatura típica de um aluno infectado:")

    wal = float(input("Entre o tam médio de palavra:"))
    ttr = float(input("Entre a relação Type-Token:"))
    hlr = float(input("Entre a Razão Hapax Legomana:"))
    sal = float(input("Entre o tam médio de sentença:"))
    sac = float(input("Entre a complexidade média da sentença:"))
    pal = float(input("Entre o tam medio de frase:"))

    return [wal, ttr, hlr, sal, sac, pal]

def le_textos():
    '''A funcao le todos os textos a serem comparados e devolve uma lista contendo cada texto como um elemento'''
    i = 1
    textos = []
    texto = input("Digite o texto " + str(i) +" (aperte enter para sair):")
    while texto:
        textos.append(texto)
        i += 1
        texto = input("Digite o texto " + str(i) +" (aperte enter para sair):")
    return textos

def separa_sentencas(texto):
    '''A funcao recebe um texto e devolve uma lista das sentencas dentro do texto'''
    sentencas = re.split(r'[.!?]+', texto)
    if sentencas[-1] == '':
        del sentencas[-1]
    return sentencas

def separa_frases(sentenca):
    '''A funcao recebe uma sentenca e devolve uma lista das frases dentro da sentenca'''
    return re.split(r'[,:;]+', sentenca)

def separa_palavras(frase):
    '''A funcao recebe uma frase e devolve uma lista das palavras dentro da frase'''
##    palavras = list(chain(*frase))
##    print(palavras,'\n')
##    palavras.split()
##    print(palavras)
##    return frase
    return frase.split()

def n_palavras_unicas(lista_palavras):
    '''Essa funcao recebe uma lista de palavras e devolve o numero de palavras que aparecem uma unica vez'''
    freq = dict()
    unicas = 0
    for palavra in lista_palavras:
        p = palavra.lower()
        if p in freq:
            if freq[p] == 1:
                unicas -= 1
            freq[p] += 1
        else:
            freq[p] = 1
            unicas += 1

    return unicas

def n_palavras_diferentes(lista_palavras):
    '''Essa funcao recebe uma lista de palavras e devolve o numero de palavras diferentes utilizadas'''
    freq = dict()
    for palavra in lista_palavras:
        p = palavra.lower()
        if p in freq:
            freq[p] += 1
        else:
            freq[p] = 1

    return len(freq)

def compara_assinatura(as_a, as_b):
    '''IMPLEMENTAR. Essa funcao recebe duas assinaturas de texto e deve devolver o grau de similaridade nas assinaturas.'''
    sab = 0
    for i in range(0,len(as_a)):
        sab = sab + abs(as_a[i]-as_b[i])
    sab = sab/6
    return sab

def calcula_assinatura(texto):
    '''IMPLEMENTAR. Essa funcao recebe um texto e deve devolver a assinatura do texto.'''
    sentencas = separa_sentencas(texto)
    frases = []
    palavras = []
    todas_as_palavras = []
    tam_medio_sentenca_lista = []
    tam_medio_lista = []
    tam_medio_frases_lista = []
    tam_medio_frases2_lista= []
    for sentenca in sentencas:
        frases.append(separa_frases(sentenca))
        tam_medio_sentenca_lista.append(len(sentenca))
    for frase1 in frases:
        tam_medio_frases_lista.append(len(frase1))
        for frase2 in frase1:
            palavras.append(separa_palavras(frase2))
            tam_medio_frases2_lista.append(len(frase2))
    for palavra in palavras:
        for palavra1 in palavra:
            todas_as_palavras.append(palavra1)
            tam_medio_lista.append(len(palavra1))
    hapax_legomana = n_palavras_unicas(todas_as_palavras)/len(todas_as_palavras)
    type_token = n_palavras_diferentes(todas_as_palavras)/len(todas_as_palavras)
    tam_medio = sum(tam_medio_lista)/len(tam_medio_lista)
    tam_medio_sentenca = sum(tam_medio_sentenca_lista) /(len(sentencas))
    complexidade = sum(tam_medio_frases_lista)/len(tam_medio_frases_lista)
    tam_medio_frases = sum(tam_medio_frases2_lista)/len(tam_medio_frases2_lista)
    assinatura = [tam_medio, type_token, hapax_legomana, tam_medio_sentenca, complexidade, tam_medio_frases]
    return assinatura
       
def avalia_textos(textos, ass_cp):
    '''IMPLEMENTAR. Essa funcao recebe uma lista de textos e uma assinatura ass_cp e deve devolver o numero (1 a n) do texto com maior probabilidade de ter sido infectado por COH-PIAH.'''
    i = 0
    assinatura = []
    similaridade = []
    textos_entrada = textos
    for i in range (0, len(textos_entrada)):
        assinatura.append(calcula_assinatura(textos_entrada[i]))
        similaridade.append(compara_assinatura(assinatura[i],ass_cp))
    mais_similar = similaridade[0]
    j = 0
    for i in range (1, len(textos_entrada)):
        if mais_similar > similaridade[i]:
            mais_similar = similaridade[i]
            j = i
    print("O autor do texto ", j+1, " está infectado com COH-PIAH")
    return j+1
def main():
    assinatura_entrada = le_assinatura()
    user_input = le_textos()
    avalia_textos(user_input, assinatura_entrada)

main()
