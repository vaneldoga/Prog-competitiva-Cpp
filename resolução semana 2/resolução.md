# Resoluções de Exercícios C++

Coleção de resoluções de problemas de programação.

---

## 💃 Questão: Dança

**Problema:** Dado uma matriz de N linhas e K colunas, inicialmente preenchida com números sequenciais (1 a N\*K), o programa processa P operações. Cada operação pode ser 'c' (trocar duas colunas especificadas) ou 'l' (trocar duas linhas especificadas). Ao final de todas as operações, o programa imprime a matriz resultante.

**Resolução (C++):**
```cpp
#include <iostream>
using namespace std;

struct Passos{
    char posicao;
    unsigned a = 0, b = 0;
};
using Passos = struct Passos;

int main(){
    unsigned n, k, p;
    int indices = 1;
    cin>>n>>k>>p;
    Passos lista_passos[p];
    for(unsigned i = 0; i<p; i++){
        cin>>lista_passos[i].posicao
        >>lista_passos[i].a>>lista_passos[i].b;
        lista_passos[i].a --;
        lista_passos[i].b --;
    }
    // formando a matriz inicial
    int matriz[n][k];
    for(unsigned i = 0; i < n; i ++){
        for(unsigned j = 0; j < k; j++){
            matriz[i][j] = indices++;
        }
    }
    for(unsigned i = 0; i < p; i++){
        if(tolower(lista_passos[i].posicao) == 'c'){
            for(unsigned j = 0; j < n; j++){
                int temp = matriz[j][lista_passos[i].b];
                matriz[j][lista_passos[i].b] = matriz[j][lista_passos[i].a];
                matriz[j][lista_passos[i].a] = temp;
            }
        }else if(tolower(lista_passos[i].posicao) == 'l'){
            for(unsigned j = 0; j < k; j++){
                int temp = matriz[lista_passos[i].b][j];
                matriz[lista_passos[i].b][j] = matriz[lista_passos[i].a][j];
                matriz[lista_passos[i].a][j] = temp;
            }
        }
    }
    cout<<endl;
    for(unsigned i = 0; i < n; i ++){
        for(unsigned j = 0; j < k; j++){
            cout<<matriz[i][j]<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```
## 🔤 Questão: Alfabeto

**Problema:** O programa verifica se uma string ("mensagem") pode ser formada usando apenas os caracteres contidos em outra string ("alfabeto"). Ele lê os comprimentos esperados, as duas strings, e valida se os comprimentos batem. Em seguida, checa se cada caractere da mensagem existe no alfabeto. Se todos existirem, imprime 'S'; caso contrário, imprime 'N'.

**Resolução (C++):**
```cpp
#include <iostream>
using namespace std;

int main() {
    int K, N;
    cin >> K >> N;

    char alien[100];

    for (int i = 0; i < K; i++) {
        cin >> alien[i];
    }

    bool veio_do_espaco = true;

    for (int i = 0; i < N; i++) {
        char caractere;
        cin >> caractere;

        bool encontrado = false;

        for (int j = 0; j < K; j++) {
            if (caractere == alien[j]) {
                encontrado = true;                
            }
        }
        if (encontrado == false) {
            veio_do_espaco = false;            
        }
    }

    if (veio_do_espaco == true) {
        cout << 'S' << endl;
    }
    else {
        cout << 'N' << endl;
    }

    return 0;
}
```
## 🧾 Questão: Lista

**Problema:** Dada uma lista de strings (que representam números) e um conjunto de "perguntas" (que são intervalos inicio-fim), o programa calcula uma soma para cada pergunta. A soma é obtida iterando por todos os pares (i, j) distintos dentro do intervalo, concatenando as strings lista_valores[i] e lista_valores[j], convertendo o resultado para inteiro e somando ao total (desde que lista_valores[j] não seja negativo).

**Resolução (C++):**
```cpp
#include <iostream>
#include <string>
using namespace std;

struct posicao{
    unsigned inicio, fim;
};
using posicao = struct posicao;

bool is_numerical(const string &word){
    string::const_iterator count = word.begin();
    while(count != word.end()){
        if(!isdigit(*(count++))){
            return false;
        }
    }
    return true;
}


int main(){
    unsigned tamanho_lista;
    unsigned tamanho_perguntas;
    cin>>tamanho_lista;
    cin>>tamanho_perguntas;
    string lista_valores[tamanho_lista];
    int respostas[tamanho_perguntas];
    posicao lista_perguntas[tamanho_perguntas];
    for(unsigned i = 0; i<tamanho_lista; i++){
        cin>>lista_valores[i];
    }
    for(unsigned i = 0; i<tamanho_perguntas; i++){
        cin>>lista_perguntas[i].inicio>>lista_perguntas[i].fim;
        lista_perguntas[i].inicio --;
        lista_perguntas[i].fim --;
    }
    // numero de combinações  n * (n - 1)
    // cocatenar todos menos a si mesmo!!
    for(unsigned count = 0; count < tamanho_perguntas; count++){
        int sum = 0;
        for(unsigned i = lista_perguntas[count].inicio; i<=lista_perguntas[count].fim; i++){
            for(unsigned j = lista_perguntas[count].inicio; j<=lista_perguntas[count].fim; j++){
                if(not ((is_numerical(lista_valores[i]) and is_numerical(lista_valores[j])))){
                    cerr<<"valores devem ser inteiros"<<endl;
                    return -1;
                }
                if((j != i) and (stoi(lista_valores[j])>=0)){
                    sum += stoi((lista_valores[i] + lista_valores[j]));
                }
            }
        }
        respostas[count] = sum;
    }
    cout<<"respostas:"<<endl;
    for(unsigned i = 0; i < tamanho_perguntas; i++){
        cout<<respostas[i]<<endl;
    }
    return 0;
}
```
## 🛣️ Questão: Avenida

**Problema:** Dado um conjunto de pontos fixos em uma avenida ({0, 400, 800, 1200, 1600, 2000}) e uma localização de entrada (um número inteiro), o programa calcula e imprime a distância da entrada até o ponto fixo mais próximo. Ele faz isso encontrando o intervalo que contém a entrada e calculando a menor das duas distâncias (para o ponto anterior e o posterior).

**Resolução (C++):**
```cpp
#include <iostream>
using namespace std;

int main() {
   int D, caminho_1, caminho_2;

   cin >> D;

   caminho_1 = D % 400;
   caminho_2 = 400 - caminho_1;

   if (caminho_1 < caminho_2) {
      cout << caminho_1 << endl;
   }
   else {
      cout << caminho_2 << endl;
   }

   return 0;
}
```
## 🔁 Questão: Palíndromo (Desafio)

**Problema:** Verifica se um número inteiro é um palíndromo. Um palíndromo é um número que permanece o mesmo quando seus dígitos são invertidos (ex: 121, 141). O programa converte o número para string e compara os caracteres do início (s_count) e do fim (f_count), movendo os iteradores para o centro.

**Resolução (C++):**
```cpp
#include <iostream>
#include <string>
using namespace std;

bool isPalindrome(int x) {
    string palindromo = to_string(x);
    string::iterator s_count = palindromo.begin();
    string::iterator f_count = palindromo.end();
    f_count--;
    while((s_count != f_count) and (*s_count != '\0')){
        if(*(s_count++) != *(f_count--)){
            return false;
        }
    }
    return true;
}
//  string = "11\0"  "oi, mundo\0"
//   |s_count| = 0x0004 *|s_count| = '1'; 
//   |s_count|++ = 0x005 *|s_count| = '1';
//   |s_count|++ = 0x006 *|s_count| = '\0'
 /*
    *|s_count| = '1'   *|f_count| = '1'
    *|f_count| != *|s_count| => return false
    *|s_count| == *|f_count| => s_count++  f_count--
    s_count++ *|s_count| = '\0'


*/


int main(){
    int x = 141;
    if(isPalindrome(x)){
        cout<<"é palindromo\n";
    }else{
        cout<<"não é palindromo\n";
    }
    return 0;
}
```
