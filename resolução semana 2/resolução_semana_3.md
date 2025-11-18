# Questão 1: Hipotenusas Inteiras

## 📝 Enunciado

    Dado um número inteiro positivo n, determinar todos os inteiros entre 1 e n que são comprimento da hipotenusa de um triângulo retângulo com catetos inteiros. 

## 🧠 Contexto

O desafio aqui é encontrar números 'h' (hipotenusa), no intervalo de 1 até n, que satisfaçam a equação de Pitágoras a2+b2=h2, onde 'a' e 'b' também são números inteiros positivos.
Uma abordagem eficiente é iterar por todos os possíveis pares de catetos 'a' e 'b' (começando de 1) e calcular o 'h' resultante. Se h2 for um quadrado perfeito (ou seja, se h2​ for um inteiro) e h≤n, então esse 'h' é uma resposta válida.

## 💻 Código

### Resolução : **Rust** por Ícaro Santana
```rust
use std::io;
use num::pow;

fn ver(x : i32, y : i32) -> i32{
    let return_t = pow(y, 2) - pow(x, 2);
    let return_t = (return_t as f32).sqrt();
    if  return_t.fract() == 0.0{
        return return_t as i32;
        // int(return_t)
    }
    0
}


fn main() -> Result<(), Box<dyn std::error::Error>>{
    let mut n = String::new();
    io::stdin()
        .read_line(&mut n)
        .expect("erro");
    let n : i32 = n.trim().parse()?;
/*
    a² = b² + c² 
    b² = a² - c²
    b = / a² - c²
*/
    for i in 1 .. n+1{
        for j in 1 .. n+1{
            if ver(i, j) != 0{
                println!("Hipotenusa : {}, cateto A:{}, Cateto B:{}",j ,i, ver(i, j));
            }
        }
    }
    Ok(())
}
```

### Resolução : **C++** por Yuri Delgado 
```c++
#include <iostream>
#include <cmath>

int main() {

   int a, b, c, n;

   std::cout << std::endl;
   std::cin >> n;

   std::cout << "Valor de n: " << n << std::endl;
 
   for (c = 1; c <= n+1; c++) {

      for (a = 1; a < c; a++) {

         for (b = 1; b < a; b++) {
         
            if (a > b && c == sqrt(pow(a, 2) + pow(b, 2))) {
               std::cout << c << "" << a << "" << b << std::endl;

              } 
         }
      }
   }

   return 0;
}
```

### Resolução : **Python** por Davi Chaves
```python
n = int(input("Digite o valor de n: "))

print(f"Hipotenusas possiveis entre 1 e  {n} : ")

for h in range(1, n+1):
    encontrou = False

    for a in range(1, h):

        for b in range(1, h):

            if a * a + b * b == h*h:

                encontrou = True

                break
        if encontrou:
            break

    if encontrou:
        print(f" hipotenusa {h} cateto {a} cateto {b}")
```

# Questão 2: Soma de Números Primos

## 📝 Enunciado

    Dados n números inteiros positivos, calcular a soma dos que são primos. 

## 🧠 Contexto

Este problema exige duas partes principais:
- Ler a entrada: Primeiro, ler o valor de n e, em seguida, usar um laço para ler os n números da sequência.
  
- Verificar primalidade: Para cada número lido, é preciso implementar uma função auxiliar (ex: ehPrimo(num)) que verifica se ele é primo. Um número é primo se for maior que 1 e divisível apenas por 1 e por ele mesmo.

- Acumular: Manter uma variável soma que acumula (soma) todos os números que passarem no teste de primalidade.

## 💻 Código

### Resolução : **Rust** por Ícaro Santana
```rust
use std::io;

fn primo(x : i32) -> bool{
    if x <= 1{
        return false
    }
    for i in 2 .. x {
        if x % i == 0{
            return false;
        }
    }
    true
}


fn main() {
    let mut x = String::new();
    io::stdin()
        .read_line(&mut x)
        .expect("erro");
    let x : i32 = x.trim().parse().expect("erro");
    let mut sum = 0;
    for nums in 1 .. x+1{
        if primo(nums){
            sum += nums;
        }
    }
    println!("Soma dos primos: {}", sum);
}

```

### Resolução : **C++** por Yuri Delgado
```C++
#include <iostream>

int main() {

   int n, numero;
   int soma = 0;

   std::cout << "Informe a quantidade de números: ";
   std::cin >> n;

   for (int s = 0; s < n; s++) {
      std::cout << "Digite um número: "; 
      std::cin >> numero;

      int div = 0;

      for (int i = 1; i <= numero; i++) {

         if (numero % i == 0) {
            div++;  
         } 

      }

      if (div == 2) {
         soma += numero;
      }

   }  

   std::cout << "Soma entre os números primos: " << soma << std::endl;
  
   return 0;
}
```

### Resolução : **Python** por Davi Chaves
```python
import math
n = int ( input ("Insira a quantidade de n-numeros: "))
soma = 0
cont = 0
while cont < n:
    num = int(input("Digite o numero: "))
    raiz = int(math.sqrt(num))

    primo = True

    if num <=1:
        primo = False
    else:
        for i in range(2,raiz + 1 ) :
            if num % i == 0:
                primo = False
                break
    if primo == True:
         soma += num

    cont +=1
print(soma)
```

# Questão 3: Máximo Divisor Comum (MDC)

## 📝 Enunciado

    Dados um inteiro positivo n e uma seqüência de n inteiros positivos, determinar o máximo divisor comum a todos eles. 

## 🧠 Contexto

O objetivo é encontrar o MDC de um conjunto de números, não apenas de dois. A estratégia mais comum é usar o Algoritmo de Euclides de forma iterativa:
- Calcule o MDC dos dois primeiros números da sequência (ex: mdc_parcial = mdc(num1, num2)).

- Use esse resultado para calcular o MDC com o próximo número (ex: mdc_parcial = mdc(mdc_parcial, num3)).

- Repita o passo 2 para todos os números restantes da sequência. O valor final de mdc_parcial será o MDC de todos os números.

## 💻 Código

### Resolução : **Rust** por Ícaro Santana
```rust
pub mod my_mdc{
    pub fn mdc(div : i32, vec_valores : &Vec<i32>) -> bool{
        for nums in vec_valores{
            if *nums % div != 0{
                return false;
            }
        }
        true
    }

    pub fn sub_vec(div : i32, vec_valores : &mut Vec<i32>) -> bool{
        let mut retorno = true;
        for nums in vec_valores{
            if *nums % div == 0 {
                *nums = *nums/div;
                retorno = false; 
            }
        }
        return  retorno;
    } 
}
```

```rust
use std::io;
use mdc::my_mdc::{mdc,sub_vec};

fn veri_break(vec_valores : &Vec<i32>) -> bool{
    for nums in vec_valores{
        if *nums != 1{
            return false;
        }
    }
    true
}

fn main() {
    let mut resultado = 1;
    let mut vec_valores : Vec<i32> = Vec::new();
    let mut n = String::new();

    io::stdin()
        .read_line(&mut n)
        .expect("erro");
    let n : i32 = n.trim().parse().expect("erro");

    //criando o vetor de valores brutos
    for _nums in 0 .. n{
        let mut x = String::new();
        io::stdin()
            .read_line(&mut x)
            .expect("erro");
        let x : i32 = x.trim().parse().expect("erro");
        vec_valores.push(x);
    }
    let mut div = 2;

    loop{
        if mdc(div, &vec_valores){
            resultado *= div;
        }
        if sub_vec(div, &mut vec_valores){
            div += 1;
        }
        if veri_break(&vec_valores){
            break;
        }
    };
    println!("{}", resultado);
}
```

### Resolução  : **Python** por Davi Chaves
```python
def mdc (a:int, b: int):
    while b != 0:
        resti = a % b
        a = b
        b = resti
    return  a

n = int ( input ("Digite a quantidade de numeros a inserir: "))

numeros = []

for i in range( 0, n):
    num = int(input("digite um numero: "))
    numeros.append(num)

resultadomdc = numeros[0]

for i in range (1, n):
    resultadomdc = mdc(resultadomdc, numeros[i])

print(f"O resultado do mdc e: {resultadomdc}")
```

# Questão 4: Verificação de Ponto na Figura H

## 📝 Enunciado

    Os pontos (x,y) que pertencem à figura H (abaixo) são tais que x≥0, y≥0 e x2+y2≤1. Dados n pontos reais (x,y), verifique se cada ponto pertence ou não a H. 

(Contexto da imagem: A figura H é o primeiro quadrante de um círculo de raio 1, centrado na origem.)

## 🧠 Contexto

Este é um problema de verificação de condições. A figura H é definida por três regras matemáticas simultâneas. Para cada ponto (x, y) fornecido, o programa deve testar se todas as três condições são verdadeiras:
- x >= 0 (Está no primeiro ou quarto quadrante)

- y >= 0 (Está no primeiro ou segundo quadrante)

- x2+y2≤1 (Está dentro ou na borda do círculo de raio 1)

Se todas as três forem verdadeiras, o ponto pertence a H.

## 💻 Código


### Resolução : **Rust** por Ícaro Santana
```rust
use std::io;

/*
regras para entrar (x, y) a H
x >= 0
y >= 0
x² + y² <= 1
*/
fn checklist(x : f32, y : f32){
    if x >= 0.0 && y>= 0.0 && (x*x + y*y <= 1.0){
        println!("x : {} e y : {} pertencem a H", x, y);
    }else{
        println!("x : {} e y : {} não pertencem a H", x, y);
    }
}

fn main() {
    // verificação quantia de pontos
    let mut n =  String::new();
    io::stdin()
        .read_line(&mut n)
        .expect("erro na leitura");
    let n: i32 = n 
        .trim()
        .parse()
        .expect("erro no parser");
    // criação do vetor dos pontos
    for pontos in 0 .. n{
        println!("ponto x {}:", pontos);
        let mut x = String::new();
        io::stdin()
            .read_line(&mut x)
            .expect("erro na leitura");
        let x : f32 = x.trim().parse().expect("erro");
        println!("ponto y {}:", pontos);
        let mut y = String::new();
        io::stdin()
            .read_line(&mut y)
            .expect("erro na leitura");
        let y : f32 = y.trim().parse().expect("erro");
        checklist(x, y);
    }
}

```

### Resolução : **C++** por Yuri Delgado
```c++
#include <iostream>
#include <cmath>

int main () {
   int n;
   float x, y;


   std::cout << "Digite quantos potos deseja verificar: ";
   std::cin >> n;

   for (int i = 1; i <= n; i++) {

      std::cout << "x e y: ";
      std::cin >> x >> y;

      if (x >= 0 and y >= 0 and pow(x, 2) + pow(y, 2) <= 1) {
         std::cout << "O ponto " << i << " (" << x << ", " << y << ") " << "pertence a H." << std::endl;
      }
      else {
         std::cout << "O ponto " << i << " (" << x << ", " << y << ") " << " não pertence a H." << std::endl;

      }
      
   }

   return 0;
}
```

### Resolução : **Python** por Davi Chaves
```python
n = int(input("Digite a quantidade de pontos: "))
pontos = []

for _ in range(n):
    x = float(input("Digite o valor de x: "))
    y = float(input("Digite o valor de y: "))
    pontos.append((x, y))

print("\nOs pontos válidos são:")
for (x, y) in pontos:
    if x > 0 and y > 0 and x * x + y * y >= 1:
        print(f"({x}, {y})")
```

# Questão 5: Raízes da Equação do 2º Grau

## 📝 Enunciado

    Dados números reais a, b e c, calcular as raízes de uma equação do 2∘ grau da forma ax2+bx+c=0. Imprimir a solução em uma das seguintes formas: 

a. DUPLA b. REAIS DISTINTAS c. COMPLEXAS

## 🧠 Contexto

Este é o clássico problema da fórmula de Bhaskara. O fluxo do programa depende inteiramente do valor do discriminante (Delta: Δ=b2−4ac):
- Calcular Delta (Δ).

- Se Δ>0: Existem duas raízes reais distintas. Calcule-as usando a fórmula (−b±Δ​)/(2a) e imprima "REAIS DISTINTAS" seguido das duas raízes.

- Se Δ=0: Existe uma raiz real dupla. Calcule-a usando a fórmula −b/(2a) e imprima "DUPLA" seguido da raiz.

- Se Δ<0: Existem duas raízes complexas conjugadas. Calcule a parte real (−b/(2a)) e a parte imaginária (−Δ​/(2a)). Imprima "COMPLEXAS" seguido da parte real e da parte imaginária.

## 💻 Código


### Resolução : **Rust** por Ícaro Santana
```rust
use std::io;

/*
Delta = b² - 4ac
*/
fn delta(a : f32, b : f32, c : f32) -> (String, f32){
    let delta = (b*b) - (4.0 * a * c);
    if delta > 0.0 {
        return (String::from("Reais distintas"), delta);
    }
    if delta == 0.0 {
        return (String::from("Raiz única"), delta);
    }
    (String::from("Complexos"), delta)
}

fn raizes(caminho : &str, delta : f32, b : f32, a : f32){
    match caminho {
        "Reais distintas" => {
            let raiz1 = (-b + delta.sqrt() )/ (2.0 * a);
            println!("Raiz 1 : {}", raiz1);
            let raiz2 = (-b - delta.sqrt() )/( 2.0 * a);
            println!("Raiz 2 : {}", raiz2);
        },
        "Raiz única" => {
            let raiz = -b / (2.0 * a);
            println!("Raiz única : {}", raiz);
        },
        "Complexos" => {
            let real = -b / (2.0 * a);
            let imaginaria = ((-delta).sqrt())/(2.0 * a);
            println!("Parte real : {}\nParte imaginária : {}", real, imaginaria);
        },
        &_ =>panic!("Erro na string de recebimento")

    }
}


fn main() {
    println!("A :");
    let mut a = String::new();
    io::stdin()
        .read_line(&mut a)
        .expect("erro");
    let a : f32 = a.trim().parse().expect("erro no parser");
    println!("B :");
    let mut b = String::new();
    io::stdin()
        .read_line(&mut b)
        .expect("erro");
    let b : f32 = b.trim().parse().expect("erro no parser");
    println!("C :");
    let mut c = String::new();
    io::stdin()
        .read_line(&mut c)
        .expect("erro");
    let c : f32 = c.trim().parse().expect("erro no parser");
    
    // ax² + bx² + c = 0
    if a == 0.0{
        if b != 0.0{
            // bx + c = 0
            let raiz = -c / b;
            println!("Equação do 1 grau raiz = {}", raiz);
        }else {
            // b = 0 ou c == 0
            if c == 0.0{
                println!("Infinitas soluçõess");
            }else{
                println!("Nenhuma solução {} = 0", c);
            }
        }
    }else {
        let (caminho, result_delta) = delta(a, b, c);
        raizes(&caminho[..], result_delta, b, a);
    }
}

```

### Resolução : **C++** por Yuri Delgado
```c++
#include <iostream>
#include <cmath>

int main() {
   float a, b, c, delta, raiz1, raiz2;

   std::cout << "a, b, c: ";
   std::cin >> a >> b >> c;

   delta = b * b - 4 * a * c;
//   std::cout << delta << std::endl;

   if (delta == 0) {
      raiz1 = -b / (2 * a);

      std::cout << "a. DUPLA" << std::endl;
      std::cout << "   raiz: " << raiz1 << std::endl; 
   }

   else if (delta > 0) {
      raiz1 = ( -b + sqrt(delta) ) / (2 * a);
      raiz2 = ( -b - sqrt(delta) ) / (2 * a);

      std::cout << "b. REAIS DISTINTAS" << std::endl;
      std::cout << "   raiz 1: " << raiz1 << std::endl;
      std::cout << "   raiz 2: " << raiz2 << std::endl;
   }

   else {
      float parteReal = -b / (2 *a);
      float parteImaginaria = sqrt(- delta) / (2 * a);

      std::cout << "c. COMPLEXAS" << std::endl;
      std::cout << "   parte real: " << parteReal << std::endl;
      std::cout << "   parte imaginária: " << parteImaginaria << std::endl;
   }

   return 0;
}
```

### Resolução : **Python** por Davi Chaves
```python

import math

a = float(input("Digite o valor de a: "))
b = float(input("Digite o valor de b: "))
c = float(input("Digite o valor de c: "))

delta = bb - 4ac

if delta == 0:
    print("a) RAÍZES REAIS E IGUAIS")
    raiz = -b / (2 a)
    print(f"Raiz dupla: {raiz}")

elif delta > 0:
    print("b) RAÍZES REAIS E DISTINTAS")
    raiz1 = (-b + math.sqrt(delta)) / (2 * a)
    raiz2 = (-b - math.sqrt(delta)) / (2 * a)
    print(f"Raiz 1: {raiz1}")
    print(f"Raiz 2: {raiz2}")

else:
    print("c) RAÍZES COMPLEXAS")
    parte_real = -b / (2 * a)
    parte_imaginaria = math.sqrt(-delta) / (2 * a)
    print(f"Parte real: {parte_real}")
    print(f"Parte imaginária: ±{parte_imaginaria}i")
```

# Questão 6: Médias da Classe

## 📝 Enunciado

    Para n alunos de uma determinada classe são dadas as 3 notas das provas. Calcular a média aritmética das provas de cada aluno, a média da classe, o número de aprovados e o número de reprovados (critério de aprovação: média maior ou igual a cinco). 

## 🧠 Contexto

Este problema requer o uso de laços e variáveis "acumuladoras". O programa deve:
- Manter contadores para totalAprovados, totalReprovados e um acumulador para somaMediasDaClasse.

- Iniciar um laço que se repete n vezes (um para cada aluno).

Dentro do laço:
- Ler as 3 notas do aluno.

- Calcular a mediaAluno (soma das 3 notas / 3).

- Imprimir a mediaAluno.

- Verificar se mediaAluno >= 5.0. Se sim, totalAprovados++, senão totalReprovados++.

- Adicionar a mediaAluno ao acumulador somaMediasDaClasse.

- Após o laço, calcular a mediaClasse (somaMediasDaClasse / n).

- Imprimir a mediaClasse, totalAprovados e totalReprovados.

## 💻 Código


### Resolução : **Rust** por Ícaro Santana
```rust
use std::io;

struct  Resultados{
    aprovados : i32,
    reprovados : i32,
}
fn main() {
    // quantidade de alunos 
    let mut n = String::new();
    io::stdin()
        .read_line(&mut n)
        .expect("erro");
    let n : i32 = n.trim().parse().expect("erro");
    //vetor de médias
    let mut vet : Vec<f32> = Vec::new();
    for _alunos in 0 .. n{
        let mut sum = 0.0;
        let mut notas = String::new();
        io::stdin()
            .read_line(&mut notas)
            .expect("erro");
        let vetor_notas : Vec<&str> = notas.split_whitespace().collect();
        for nota in vetor_notas{
            let provas : f32 = nota.to_string().parse().expect("erro");
            sum += provas;
        }
        sum /= 3.0;
        vet.push(sum);
    }
    let mut media_classe = 0.0;
    let mut resultados   = Resultados{
        aprovados : 0,
        reprovados : 0,
    };
    for media in &vet{
        if *media >= 5.0{
            resultados.aprovados += 1;
        }else{
            resultados.reprovados += 1;
        }
        media_classe += *media;
        println!("Media aluno: {}", *media);
    }
    media_classe /= vet.len() as f32;
    println!("Média da sala : {}\nNúmero de aprovados : {}\nNúmero de reprovados : {}",
    media_classe,
    resultados.aprovados,
    resultados.reprovados
    );
}

```

### Resolução : **C++** por Yuri Delgado
```c++
#include <iostream>

int main() {
   int n, aprovados = 0, reprovados = 0;
   float nota1, nota2, nota3, alunoMedia, mediaSoma, mediaTotal;

   std::cout << "Informe a quantidade de alunos: ";
   std::cin >> n;

   for (int i = 1; i <= n; i++) {
      std::cout << i << "° aluno, digite a primeira nota: ";
      std::cin >> nota1;
      std::cout << i << "° aluno, digite a segunda nota: ";
      std::cin >> nota2;
      std::cout << i << "° aluno, digite a terceira nota: ";
      std::cin >> nota3;

      alunoMedia = (nota1 + nota2 + nota3) / 3;

      mediaSoma += alunoMedia;

      if (alunoMedia >= 5) {
         aprovados++;
      }
      else {
         reprovados++;
      }

      std::cout << "---->  Media do " << i << "° aluno: " << alunoMedia << std::endl;
   }

   mediaTotal = mediaSoma / n;

   std::cout << "Média da classe: " << mediaTotal << std::endl;
   std::cout << "Número de aprovados: " << aprovados << std::endl;
   std::cout << "Número de reprovados: " << reprovados << std::endl;

   return 0;
}
```

# Questão 7: Operações Básicas

## 📝 Enunciado

    Dadas n triplas compostas por um símbolo de operação (+, -, * ou /) e dois números reais, calcule o resultado ao efetuar a operação indicada para os dois números (Sugestão: use switch). 

## 🧠 Contexto

O programa deve ler n operações. Para cada operação, ele precisa ler um caractere (ou string) para o símbolo da operação e dois números (operandos).

Conforme a sugestão, uma estrutura switch-case (ou uma série de if-else if-else) é ideal para tratar o símbolo da operação:

- Se o símbolo for +, calcule a soma.

- Se o símbolo for -, calcule a subtração.

- Se o símbolo for *, calcule a multiplicação.

- Se o símbolo for /, calcule a divisão (atenção para o caso de divisão por zero!).

Imprima o resultado de cada operação antes de passar para a próxima.

## 💻 Código

### Resolução : **Rust** por Ícaro Santana
```rust
use std::io::{self, Write};
fn main() {
    print!("Número de expressões:");
    io::stdout().flush().expect("erro");
    let mut n = String::new();
    io::stdin()
        .read_line(&mut n)
        .expect("erro");
    let n : i32 = n.trim().parse().expect("erro");
    for _ in 0 .. n{
        print!(">");
        io::stdout().flush().expect("erro");
        let mut line = String::new();
        io::stdin()
            .read_line(&mut line)
            .expect("erro");
        let vet : Vec<&str> = line.split_whitespace().collect();
        match vet.as_slice(){
            [n1, operador, n2] => {
                let x : f32 = match (*n1).to_string().parse(){
                    Ok(num) => num,
                    Err(_) => {
                        println!("Valor inválido escreva em forma decimal!");
                        continue;
                },
                };
                let y : f32 = match (*n2).to_string().parse(){
                    Ok(num) => num,
                    Err(_) => {
                        println!("Valor inválido escreva em forma decimal!");
                        continue;
                    },
                };
                match *operador {
                    "+" => {
                        println!("Resultado : {}", x + y);
                    },
                    "-" => {
                        println!("Resultado : {}", x - y);
                    },
                    "/" => {
                        if y > 0.0{
                            println!("Resultado : {}", x / y);
                        }
                        else{
                            println!("Erro : divisão por zero");
                        }
                    },
                    "*" => {
                        println!("Resultado : {}", x * y);
                    },
                    &_ => println!("Operação desconhecida"),
                }
            }
            _ => println!("Entrada não esperada"),
        };
    }
}

```

### Resolução : **C++** por Yuri Delgado
```c++
#include <iostream>

int main() {

    int n;
    char operacao;
    float resultado, a, b;

    std::cout << "Número de operações: ";
    std::cin >> n;

    for (int i = 1; i <= n; i++) {

        std::cout << "Digite o símbolo da operação (+, -, *, /): ";
        std::cin >> operacao;

        std::cout << "valor de a: ";
        std::cin >> a;

        std::cout << "valor de b: ";
        std::cin >> b;

        switch (operacao) {
            case '+':
                resultado = a + b;
                break;

            case '-':
                resultado = a - b;
                break;

            case '*':
                resultado = a * b;
                break;

            case '/':
                if (b == 0) {
                    std::cout << "Não é possível dividir por 0." << std::endl;
                    continue;
                }
                resultado = a / b;
                break;

            default:
                std::cout << "Operação inválida" << std::endl;
                continue;
        }

        std::cout << "Resultado = " << resultado << std::endl;
    }

    return 0;
}
```

# 🌟 Desafio: Valid Parentheses (LeetCode)

## 📝 Enunciado

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:
- Open brackets must be closed by the same type of brackets.

- Open brackets must be closed in the correct order.

- Every close bracket has a corresponding open bracket of the same type.

## 🧠 Contexto

Este é um problema clássico resolvido com uma Pilha (Stack). A lógica é iterar pela string:
- Se você encontrar um caractere de abertura ((, {, [), empurre-o (push) para a pilha.

- Se você encontrar um caractere de fechamento (), }, ]):

- Verifique se a pilha está vazia. Se estiver, a string é inválida (pois há um fechamento sem abertura).

- Se a pilha não estiver vazia, olha (peek) o topo. Se o topo não for o par correspondente ex: o fechamento ) mas o topo é {), a string é inválida.

- e o topo for o par correspondente, "desempilhe" (pop) o caractere da pilha.

- Após iterar por toda a string, verifique se a pilha está vazia. Se estiver, a string é válida. Se sobrar algo na pilha (ex: ((()), a string é inválida.

## 💻 Código

### Resolução : **Rust** por Ícaro Santana
```rust
fn is_valid(s : String) -> bool{
    let mut vet: Vec<char> = Vec::new();
    for chars in s.chars(){
        match chars{
            '(' => vet.push(chars),
            '[' => vet.push(chars),
            '{' => vet.push(chars),
            ')' => {
                if vet[vet.len()-1] != '('{
                    return false;
                }else{
                    vet.pop();
                }
            },
/*
string = ([{}])

stack : 
*/
            ']' => {
                if vet[vet.len()-1] != '['{
                    return false;
                }else{
                    vet.pop();
                }
            },
            '}' => {
                if vet[vet.len()-1] != '{'{
                    return false;
                }else{
                    vet.pop();
                }
            },
            _ => (),
        };
    }
    if vet.len() > 0{
        false
    }else{
        true
    }
}

/*
first in
first out
*/
fn main() {
    println!("{}", is_valid(String::from("({[{[]}]})")));
}

```
