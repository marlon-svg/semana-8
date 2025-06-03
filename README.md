# Implementación de Cola de Prioridad desde cero

class NodoPrioridad:
    def __init__(self, valor, prioridad):
        self.valor = valor
        self.prioridad = prioridad
        self.siguiente = None

class ColaDePrioridad:
    def __init__(self):
        self.frente = None

    def is_empty(self):
        return self.frente is None

    def enqueue(self, valor, prioridad):
        nuevo = NodoPrioridad(valor, prioridad)
        # Insertar al inicio si la cola está vacía o si tiene mayor prioridad
        if self.is_empty() or prioridad > self.frente.prioridad:
            nuevo.siguiente = self.frente
            self.frente = nuevo
        else:
            actual = self.frente
            while actual.siguiente and actual.siguiente.prioridad >= prioridad:
                actual = actual.siguiente
            nuevo.siguiente = actual.siguiente
            actual.siguiente = nuevo

    def dequeue(self):
        if self.is_empty():
            raise IndexError("No se puede hacer dequeue de una cola vacía")
        valor = self.frente.valor
        self.frente = self.frente.siguiente
        return valor

    def peek(self):
        if self.is_empty():
            raise IndexError("No se puede hacer peek de una cola vacía")
        return self.frente.valor

    def size(self):
        contador = 0
        actual = self.frente
        while actual:
            contador += 1
            actual = actual.siguiente
        return contador

    def mostrar(self):
        actual = self.frente
        elementos = []
        while actual:
            elementos.append(f"{actual.valor}(P{actual.prioridad})")
            actual = actual.siguiente
        return " -> ".join(elementos)


# Ejemplo de uso
if __name__ == "__main__":
    cola = ColaDePrioridad()

    cola.enqueue("Tarea urgente", 5)
    cola.enqueue("Revisión de correos", 2)
    cola.enqueue("Reunión", 4)
    cola.enqueue("Tarea menor", 1)

    print("📋 Estado actual de la cola de prioridad:")
    print(cola.mostrar())

    print("\n🚀 Atendiendo tareas según prioridad:")
    while not cola.is_empty():
        print("🟢 Atendiendo:", cola.dequeue())
