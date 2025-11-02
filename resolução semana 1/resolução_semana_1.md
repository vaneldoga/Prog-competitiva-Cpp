# Resoluções da primeira semana

Coleção das resoluções da semana 1

---

## Questão: Relógio

### ⏰ Problema

Dado um horário inicial (horas, minutos, segundos) e uma duração adicional (em segundos), calcular e imprimir o novo horário após somar a duração.

### Resolução (C++)

```cpp
#include <iostream>
#include <cmath>

int main(){
    unsigned h, m, s, t, total;
    std::cin>>h>>m>>s>>t;
    total = (h * 60 * 60) + (m * 60) + s + t;
    s = round(((total/60.0) - (total/60))*60);
    total = unsigned(total/60);
    m = round(((total/60.0) - (total / 60))*60);
    h = (total/60);
    std::cout<<h<<"\n"<<m<<"\n"<<s<<std::endl;
    return 0;
}
```
## Questão: Ogro

### 👹 Problema

Calcula um valor com base em duas entradas inteiras, e e d. Se e for maior que d, o resultado é a soma. Caso contrário (e se forem diferentes), o resultado é o dobro da diferença.

### Resolução (C++)

```cpp

#include <iostream>


int main(){
    int e, d, sum;
    std::cin>>e>>d;
    if((e<=5 or d<=5) and (e>=0 or d >= 0) and (e != d)){
        if(e>d){sum = e + d;}
        else{sum =  2 * (d - e);}
        std::cout<<sum<<std::endl;
    }
    return 0;
}
```
## Questão: Concurso

### 📝 Problema

Dado um número total de alunos, um número mínimo de aprovados e a lista de notas, o programa determina a nota de corte mais baixa que ainda garante que o número mínimo de alunos seja aprovado.

### Resolução (C++)

```cpp

#include <iostream>

int main(){
    int alunos, a_minimo;
    std::cin>>alunos>>a_minimo;
    int notas[alunos];
    for(int i = 0; i<alunos; i++){
        std::cin>>notas[i];
    }
    int contador_nota = 0;
    int nota_final = 0;
    for(int i = 0; i<alunos; i++){
        contador_nota = 0;
        for(int j = 0; j<alunos; j++){
            if(notas[i] <= notas[j]){
                contador_nota++;
            }
        }
        if(contador_nota>=a_minimo){
            nota_final = notas[i];
        }
    }
    std::cout<<"media:"<<nota_final<<std::endl;
    return 0;
}
```
## Questão: Roman to Int

### 🏛️ Problema

Converter um numeral romano, fornecido como uma string, para seu valor inteiro correspondente. O algoritmo lida com as regras de subtração (como IV, IX, XL, etc.).

### Resolução (C++)

```cpp

#include <iostream>
#include <string>

unsigned charToInt(char s){
    switch(s){
        case 'I':
            return 1;
        case 'V':
            return 5;
        case 'X':
            return 10;
        case 'L':
            return 50;
        case 'C':
            return 100;
        case 'D':
            return 500;
        case 'M':
            return 1000;
        default:
            return 0;
    }
    return 0;
}

unsigned romanToInt(std::string s){
    unsigned total = 0;
    for(int i=0; s[i] != '\0'; i++){
        if(charToInt(s[i])>=charToInt(s[i+1]))
            total += charToInt(s[i]);
        else{
            total += charToInt(s[i+1])-charToInt(s[i]);
            i++;
        }
    }   
    return total;
}



int main(){
    std::string v = "MCMXCIV";
    std::cout<<romanToInt(v)<<std::endl;
    return 0;
}
```
