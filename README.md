# trabalhoDE

class Nodo:
    def __init__(self, char):
        self.char = char
        self.next = None
        self.prev = None


class ListaDE:
    def __init__(self):
        self.head = None
        self.tail = None

    def inserir(self, char):
        NewNodo = Nodo(char)
        if not self.head:  
            self.head = self.tail = NewNodo
        else:
            self.tail.next = NewNodo
            NewNodo.prev = self.tail
            self.tail = NewNodo

    def __iter__(self):
        atual = self.head
        while atual:
            yield atual
            atual = atual.next

    def criptografar(self, deslocamento):
        for nodo in self:
            if nodo.char.isalpha():  
                base = ord('A') if nodo.char.isupper() else ord('a')
                nodo.char = chr((ord(nodo.char) - base + deslocamento) % 26 + base)

    def descriptografar(self, deslocamento):
        self.criptografar(-deslocamento)

    def exibir(self):
        return ''.join(nodo.char for nodo in self)


def ObterDeslocamento():
    while True:
        try:
            deslocamento = int(input("Digite o valor do deslocamento (inteiro positivo): "))
            if deslocamento < 0:
                print("O deslocamento deve ser positivo. Tente novamente.")
            else:
                return deslocamento
        except ValueError:
            print("Entrada inválida. Digite um número inteiro.")


def main():
    while True:
        lista = ListaDE()
        mensagem = input("Digite a mensagem para criptografar: ")
        for char in mensagem:
            lista.inserir(char)
        deslocamento = ObterDeslocamento()

        lista.criptografar(deslocamento)
        print(f"\nMensagem Criptografada: {lista.exibir()}")

        if input("\nDeseja descriptografar a mensagem? (s/n): ").lower() == 's':
            lista.descriptografar(deslocamento)
            print(f"Mensagem Descriptografada: {lista.exibir()}")

        if input("\nDeseja executar novamente? (s/n): ").lower() != 's':
            print("Encerrando o programa.")
            break


if __name__ == "__main__":
    main()
