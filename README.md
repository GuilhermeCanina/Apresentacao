# Padrão de Projeto Adapter

## Descrição

O padrão **Adapter** é um padrão estrutural que permite que interfaces incompatíveis trabalhem juntas. Ele age como um "adaptador" que converte a interface de uma classe em uma interface esperada por outra classe. Isso é particularmente útil quando se trabalha com sistemas legados ou bibliotecas de terceiros cujas interfaces não podem ser alteradas, mas precisam ser integradas a novos sistemas.

## Quando Usar

- Quando você tem um sistema legado com uma interface que não pode ser modificada, mas precisa ser integrado com um novo sistema.
- Quando você deseja reutilizar código de bibliotecas externas, mas a interface delas não é compatível com o restante do seu sistema.
- Quando você deseja fazer com que classes com interfaces diferentes possam interagir sem modificar seu código original.

## Estrutura

O padrão Adapter envolve três componentes principais:

- **Cliente**: O código que utiliza o serviço e que precisa de uma interface compatível.
- **Interface alvo (Target)**: A interface que o cliente espera usar.
- **Classe adaptada (Adaptee)**: A classe que possui a funcionalidade desejada, mas com uma interface incompatível com a interface alvo.
- **Adapter**: O componente responsável por adaptar a interface da classe adaptada para que ela se torne compatível com a interface alvo.

## Diagrama de Classes

```plaintext
+----------------+            +----------------+  
|    Cliente     |            |    Target      |  
|----------------|            |----------------|  
| + operation()  |<>----------| + operation()  |  
+----------------+            +----------------+  
                                    |  
                                    |  
                            +----------------+  
                            |    Adapter     |  
                            |----------------|  
                            | + operation()  |  
                            +----------------+  
                                    |  
                                    |  
                            +----------------+  
                            |    Adaptee     |  
                            |----------------|  
                            | + specificOp() |  
                            +----------------+  

```

## Exemplo de Implementação

```javascript
// Classe Adaptee (classe que possui a funcionalidade, mas com interface incompatível)
class Adaptee {
  specificOperation() {
    return "Resultado da operação específica";
  }
}

// Interface Target (interface esperada pelo cliente)
class Target {
  operation() {
    throw "Método não implementado!";
  }
}

// Adapter (converte a interface da Adaptee para a interface Target)
class Adapter extends Target {
  constructor(adaptee) {
    super();
    this.adaptee = adaptee;
  }
  
  operation() {
    return this.adaptee.specificOperation();
  }
}

// Cliente (código que usa a interface Target)
class Client {
  execute(target) {
    console.log(`Resultado da operação: ${target.operation()}`);
  }
}

// Demonstração do uso
const adaptee = new Adaptee();
const adapter = new Adapter(adaptee);
const client = new Client();

client.execute(adapter);
```

## Saída esperada:

```terminal
Resultado da operação: Resultado da operação específica
```

## Vantagens

- **Reusabilidade**: Permite que o código existente seja reutilizado sem modificação.
- **Flexibilidade**: Pode ser usado para conectar interfaces que não foram projetadas para trabalhar juntas.
- **Desacoplamento**: Permite que classes incompatíveis interajam sem precisar de alterações profundas no código existente.

## Desvantagens

- **Complexidade**: Adiciona uma camada extra de abstração, o que pode tornar o sistema mais complexo.
- **Desempenho**: O uso de adaptadores pode impactar levemente o desempenho devido à sobrecarga adicional de chamadas de métodos.

## Conclusão

O padrão **Adapter** é extremamente útil em sistemas onde é necessário integrar funcionalidades com interfaces incompatíveis. Ele permite manter o código modular e reutilizável, sem a necessidade de modificar classes existentes.
