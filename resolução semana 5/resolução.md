# Resoluções dos Exercícios Semanais

## Questão 1: Happy Number

**Objetivo:**
O código implementa um algoritmo de verificação para classificar um número inteiro positivo com base em uma propriedade matemática (Happy number). 
Ele executa um processo iterativo de transformação numérica, calculando a soma dos quadrados dos dígitos, e valida se a sequência resultante converge para a unidade ou se entra em um ciclo de repetição infinito.

### Resolução : **C++** por Yuri Delgado
```cpp
#include <iostream>

int main() {
    int n;
    bool happy = false;
    
    std::cout << "Digite um número inteiro: ";
    std::cin >> n; 

    while (n != 1 && n != 4) {
        
        int sum = 0;

        while (n > 0) {
            int unidade = n % 10; 
            sum += unidade * unidade; 
            n = n / 10; 
        }

        n = sum;
        
        std::cout << n << "\n";
    }
    
    if (n == 1) {
        happy = true;
    }

    std::cout << std::boolalpha << happy << std::endl;
    
    return 0;
}
```

## Questão 2: 

**Objetivo:**
Dado um array não vazio de $n$ números inteiros $n$ onde todos aparecem exatamente duas vezes (formando pares), exceto um único número que aparece apenas uma vez. 
O exercício consiste em encontrar este único número que não se repete. 

### Resolução : **C++** por Yuri Delgado
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> nums = {3, 4, 1, 2, 9, 3, 1, 2, 4};

    int result = 0;

    for (int i = 0; i < nums.size(); i++) {
        
        result = result ^ nums[i];
    }

    std::cout << result << std::endl;

    return 0;

}
```
