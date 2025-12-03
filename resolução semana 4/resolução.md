# Resoluções dos Exercícios Semanais

## Questão 1: Verificação de Caminhos (Grafos)

**Objetivo:**
O código implementa uma verificação de rotas em um sistema de salas e corredores (grafo). Ele analisa uma série de sugestões de trajetos e valida quantas são possíveis com base nas conexões predefinidas entre as salas.

```rust
use core::panic;
use std::io;

fn main() {
    let mut caminhos : Vec<(i32, i32)> = Vec::new();
    let mut salas = String::new();
    let mut corredores = String::new();
    io::stdin()
        .read_line(&mut salas)
        .expect("erro");
    io::stdin()
        .read_line(&mut corredores)
        .expect("erro");
    let salas : i32 = salas.trim().parse().expect("erro");
    let corredores : i32 = corredores.trim().parse().expect("erro");
    for _ in 0 .. corredores{
        let mut con_a = String::new();
        let mut con_b = String::new();
        io::stdin()
            .read_line(&mut con_a)
            .expect("erro");
        io::stdin()
            .read_line(&mut con_b)
            .expect("erro");
        let con_a : i32 = con_a.trim().parse().expect("erro");
        let con_b : i32 = con_b.trim().parse().expect("erro");
        if con_a > salas || con_b > salas{
            panic!("erro");
        }
        caminhos.push((con_a, con_b));
    }
    let mut sugestoes = String::new();
    io::stdin()
        .read_line(&mut sugestoes)
        .expect("erro");
    let sugestoes : i32 = sugestoes.trim().parse().expect("erro");
    let mut count = 0;
    for _ in 0 .. sugestoes{
        let mut s : Vec<i32> = Vec::new();
        let mut n = String::new();
        io::stdin()
            .read_line(&mut n)
            .expect("erro");
        let n : i32 = n.trim().parse().expect("erro");
        for _ in 0 .. n{
            let mut a = String::new();
            io::stdin()
                .read_line(&mut a)
                .expect("erro");
            let a : i32 = a.trim().parse().expect("erro");
            s.push(a);
        }
        let mut valid = false;
        for i in 0 .. (n - 1) as usize{
            for (a, b) in &caminhos{
                if (s[i] == *a && s[i+1] == *b) || (s[i+1] == *a && s[i] == *b){
                    valid = true;
                    break;
                }else{
                    valid = false;
                }
            }
            if !valid{
                break;
            }
        }
        if valid {
            count += 1;
        }
    }
    println!("validos : {}", count);
}

```

---

## Questão 2: Gestão de Vendas em Matriz

**Objetivo:**
Este algoritmo gerencia um estoque organizado em formato de matriz (linhas e colunas). O objetivo é processar pedidos de vendas verificando a disponibilidade do item na coordenada específica e contabilizar o número de vendas efetivadas com sucesso.

```rust
use std::io;

fn main() {
    let mut matriz : Vec<Vec<i32>> = Vec::new();
    let mut linhas = String::new();
    let mut colunas = String::new();
    io::stdin()
        .read_line(&mut linhas)
        .expect("erro");
    io::stdin()
        .read_line(&mut colunas)
        .expect("erro");
    let linhas : usize = linhas.trim().parse().expect("erro");
    let colunas : usize = colunas.trim().parse().expect("erro");
    for _ in 0 .. linhas{
        let mut coluna : Vec<i32> = Vec::new();
        for _ in 0 .. colunas{
            let mut aux = String::new();
            io::stdin()
                .read_line(&mut aux)
                .expect("erro");
            let aux : i32 = aux.trim().parse().expect("erro");
            coluna.push(aux);
        }
        matriz.push(coluna);
    }
    let mut vendas  = String::new();
    io::stdin()
        .read_line(&mut vendas)
        .expect("erro");
    let vendas : usize = vendas.trim().parse().expect("erro");
    let mut vec_vendas : Vec<(usize, usize)> = Vec::new();
    for _ in 0 .. vendas{
        let mut linha = String::new();
        let mut coluna = String::new();
        io::stdin()
            .read_line(&mut linha)
            .expect("erro");
        io::stdin()
            .read_line(&mut coluna)
            .expect("erro");
        let mut linha : usize = linha.trim().parse().expect("erro");
        let mut coluna : usize = coluna.trim().parse().expect("erro");
        linha -= 1;
        coluna -= 1;
        vec_vendas.push((linha, coluna));
    }
    let mut count = 0;
    for (linha, coluna) in vec_vendas{
        if matriz[linha][coluna] > 0{
            matriz[linha][coluna] -= 1;
            count += 1;
        }
    } 
    println!("vendas : {}", count);
}

```

---

## Questão 3: Sistema de Leilão (Maior Lance)

**Objetivo:**
O programa processa uma lista de participantes e seus respectivos lances para determinar o vencedor. Ele itera sobre os dados de entrada para identificar e exibir quem ofereceu o maior valor monetário.

```rust
use std::io;

#[derive(Debug)]
struct Comprador{
    nome : String,
    valor : f32, 
}


fn main() {
    let mut vec : Vec<Comprador> = Vec::new();
    let mut num = String::new();
    io::stdin()
        .read_line(&mut num) 
        .expect("erro");
    let num : usize = num.trim().parse().expect("erro");
    for _ in 0 .. num{
        let mut name = String::new();
        let mut value = String::new();
        io::stdin()
            .read_line(&mut name)
            .expect("erro");
        io::stdin()
            .read_line(&mut value)
            .expect("erro");
        let value : f32 = value.trim().parse().expect("erro");
        let novo_lance = Comprador{
            nome : name,
            valor : value,
        };
        vec.push(novo_lance);
    }
    let mut maior = &vec[0];
    for compradores in &vec{
        if compradores.valor > maior.valor{
            maior = compradores;
        }
    }
    println!("{:?}", maior);
}

```

---

## Questão 4: Gerenciamento de Orçamento

**Objetivo:**
O código resolve um problema de otimização simples de pagamentos. Dado um saldo inicial e um conjunto fixo de contas, ele calcula quantas dessas contas podem ser pagas sequencialmente antes que o saldo se esgote.

```rust
use std::io;

fn main() {
    let mut saldo = String::new();
    let mut contas = [0;3];
    io::stdin()
        .read_line(&mut saldo)
        .expect("erro");
    let mut saldo : i32 = saldo.trim().parse().expect("erro");
    for conta in contas.iter_mut(){
        let mut aux = String::new();
        io::stdin()
            .read_line(&mut aux)
            .expect("erro");
        let aux : i32  = aux.trim().parse().expect("erro");
        *conta = aux;
    }
    let mut counter = 0;
    for conta in contas{
        if conta <= saldo{
            counter += 1;
            saldo -=  conta;        
        }
    }
    println!("{}", counter);
}

```

---

## Desafio: Comprimento da Última Palavra

**Objetivo:**
O algoritmo recebe uma frase (string) contendo palavras e espaços. O objetivo é isolar a última palavra, ignorando espaços em branco excedentes no final da string, e retornar o tamanho (número de caracteres) dessa palavra.

```rust
fn length_of_lastword(s : String) -> usize{
    let vec : Vec<&str> = s.split_whitespace().collect();
    vec[vec.len()-1].len()
}
```

fn main() {
    println!("{}", length_of_lastword(String::from("   fly me   to   the moon  ")));
}
