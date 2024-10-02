# Controller

```java
package JavaAulas.aula1.controller;  
import java.util.Scanner;  
import JavaAulas.aula1.model.Pessoa;  
  
public class CtrlPrograma {  
    public static void main(String[] args) {  
        Scanner teclado = new Scanner(System.in);  
        Pessoa p1 = null;  
  
        Pessoa[] listaDePessoas = new Pessoa[5];  
  
        try {  
            System.out.println("Entre com o CPF: ");  
            String c = teclado.nextLine();  
            System.out.println("Entre com o Nome: ");  
            String n = teclado.nextLine();  
            p1 = new Pessoa(c,n);  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
  
        System.out.println(p1);  
  
    }  
  
}
```
---
##  Fatos

<font color="#2DC26B">Static</font> : Um método estático é um método que pertence à própria classe, e não a uma instância específica dessa classe. Isso significa que você pode chamar um método estático diretamente pela classe, sem precisar criar um objeto dessa classe. (uma variável global) 

<font color="#2DC26B">Scanner</font>: Quando você utiliza a classe `Scanner`, ela lê a entrada de dados e a divide em blocos chamados **tokens**. Esses tokens são sequências de caracteres separados por delimitadores, que por padrão são espaços em branco, tabulações e quebras de linha. Isso permite que você converta facilmente a entrada do usuário em tipos de dados que o programa pode manipular.

---
<font color="#2DC26B">[]</font> : São instruções que demostram ao programa a entrada de um Vetor, quando preenchido e passado o contexto de tamanho, ele serve pra informar, é posicionado de diferentes formas dependendo do tipo.

Ex: [5] = [0],[1],[2],[3],[4]  : Assim tem tamanho 5, mas tem apenas 4 posições.

<font color="#2DC26B">Try</font> e <font color="#c00000">Catch</font>: função realizar uma validação para evitar erros durante a compilação. Ela simula a execução do programa e, caso encontre um erro, lança uma exceção (`Exception` ou outra). Ao encontrar um erro, a função retorna a primeira exceção encontrada, encerrando o programa. Para uma melhor visualização do erro, utilize `e.printStackTrace()` para informar o erro.

---
<font color="#00b050">New</font>: vai cria e construir o objeto, informando quais instruções vai receber pelo acordo descrito no construtor 

---
---

# Model

```java 
    package JavaAulas.aula1.model;  
  
public class Pessoa {  
    //  
    // ATRIBUTOS    //    private String cpf;  
    private String nome;  
  
    //  
    // MÉTODOS    //    public Pessoa(String cpf, String nome) throws Exception {  
        super();
        this.setCpf(cpf);  
        this.setNome(nome);  
    }  
  
    public String getCpf() {  
        return this.cpf;  
    }  
    /**  
     *Caso necessario chamar o atributo no main, para usar os get, assim consultando de maneira segura um dado!     *     */  
    public void setCpf(String cpf) throws Exception {  
        Pessoa.validarCpf(cpf);  
        this.cpf = cpf;  
    }  
  
    public String getNome() {  
        return this.nome;  
    }  
  
    public void setNome(String nome) throws Exception {  
        Pessoa.validarNome(nome);  
        this.nome = nome;  
    }  
  
    public static void validarCpf(String cpf) throws Exception {  
        if (cpf == null || cpf.length() == 0)  
            throw new Exception("O CPF não pode ser nulo!");  
        if (cpf.length() != 14)  
            throw new Exception("O CPF deve ter 14 caracteres!");  
        for (int i = 0; i < cpf.length(); i++) {  
            char c = cpf.charAt(i);  
            switch (i) {  
                case 3:  
                case 7:  
                    if (c != '.')  
                        throw new Exception("O caracter na posição " + i + " deve ser '.'");  
                    break;  
                case 11:  
                    if (c != '-')  
                        throw new Exception("O caracter na posição 11 deve ser '-'");  
                    break;  
                default:  
                    if (!Character.isDigit(c))  
                        throw new Exception("O caracter na posição " + i + " deve ser dígito");  
                    break;  
            }  
        }  
    }  
  
    public static void validarNome(String nome) throws Exception {  
        if (nome == null || nome.length() == 0)  
            throw new Exception("O nome não pode ser nulo!");  
        if (nome.length() < 5 || nome.length() > 40)  
            throw new Exception("O nome deve ter entre 5 e 40");  
        for (int i = 0; i < nome.length(); i++) {  
            char c = nome.charAt(i);  
            if (!Character.isAlphabetic(c) && !Character.isSpaceChar(c))  
                throw new Exception("O caracter na posição " + i + " do nomé é inválido");  
        }  
    }  
  
    //verificar  
    public String toString() {  
        return this.cpf + " : " + this.nome;  
    }  
}
```
---
## fatos

<font color="#00b050">Método Construtor</font>: possui o mesmo nome da classe `public class Pessoa ` ele vai informa quais instruções são necessárias pra inicialização do objeto

Ex: ( p1 = new Pessoa ("texto" 56) ), onde ele vai criar o elemento e segundo o construtor os mesmos serão atribuídos  pelo `set` e usado pelo `get` tal como validados e utilizados por funções secundarias dependendo do tipo de manipulação.

Os elementos internos são separados em: CLASSE INTERNA, ATRIBUTOS, MÉTODO e CONSTANTES, Podendo  ser privados ou públicos.

---
Retorno da função, uma função pode ter diverso tipos primários de retorno como: numérico, alfanumérico, objeto, booleano  e void (sem retorno, vazio). 

---
<font color="#00b050">o método super() e para que serve?</font>
O método `super()` em Java é usado para chamar o construtor ou métodos da classe pai (superclasse). Ele é útil quando uma classe herda de outra e você quer acessar algum comportamento da superclasse.

<font color="#00b050">Utilidades do super():</font>

- **Chamar o construtor da superclasse:** Garante que a inicialização da classe pai seja feita corretamente.
  
- **Acessar métodos ou atributos da superclasse:** Permite acessar a versão original de métodos ou atributos que foram sobrescritos na classe filha.

---
<font color="#00b050">throws Exception</font> e <font color="#ff0000"> throw new Exception(" ")</font> : quando a classe tem uma validação, ou seja ela pode retorna um erro ela vai ser uma classe do tipo adicional `throws Exception` indicando que um método pode lançar uma exceção, após isso se usa filtros para dizer onde tá o erro através da mensagem `throw new Exception("Mensagem")` lança uma nova exceção com uma mensagem específica. É usado dentro do método para sinalizar onde ocorreu erro.

---
<font color="#ff0000">@Override</font>

- <font color="#00b050">O que é?</font>: Uma anotação que indica que um método está sobrescrevendo um método da superclasse ou interface.
  
- <font color="#00b050">Por que usar?</font>: Ajuda a evitar erros, garantindo que a assinatura do método sobrescrito corresponda corretamente ao da superclasse.

---
 Método<font color="#ff0000"> toString()</font>

- <font color="#00b050">O que é?</font>: Um método herdado da classe `Object` que retorna uma representação em string da instância.
  
- <font color="#00b050">Por que sobrescrever?</font>: Para fornecer uma representação mais significativa dos dados do objeto, em vez da referência de memória padrão.

---
 Lógica por Trás do <font color="#ff0000">toString()</font>

- <font color="#00b050">Objetivo</font>: Retornar uma representação textual do objeto.
- <font color="#00b050">Vantagem</font>: Quando sobrescrito, o método `toString()` exibe os atributos do objeto de forma legível, em vez de um código hexadecimal.

<font color="#ff0000"> Problema Comum</font>

- <font color="#00b050">Sem Sobrescrita</font>: O método `toString()` da classe `Object` é chamado, resultando em uma saída como `Pessoa@6d06d69c`, que é menos informativa.

---
 <font color="#ff0000">Solução</font>

- **Reimplementar o `toString()`**: Para corrigir e imprimir uma saída mais legível, sobrescreva o método `toString()` na classe `Pessoa`.
  <BR>
-  **Sobrescrita do `toString()`**: Permite que a impressão de um objeto `Pessoa` seja formatada de maneira legível.


---
---

 `charAt(int index)`

- **O que faz?**: Retorna o caractere na posição especificada de uma string.
- **Exemplo**:
    
    ```java
    String texto = "Olá";
    char c = texto.charAt(1);  // c será 'l'
    ```
    
----
 `isSpaceChar(char c)`

- **O que faz?**: Verifica se o caractere fornecido é um espaço em branco.
- **Exemplo**:
    
    ```java
    boolean espaco = Character.isSpaceChar(' ');  // espaco será true
    ```
    
---
 `isAlphabetic(char c)`

- **O que faz?**: Verifica se o caractere fornecido é uma letra alfabética.
- **Exemplo**:
    
    ```java
    boolean letra = Character.isAlphabetic('A');  // letra será true
    ```
    
---
 `length()`

- **O que faz?**: Retorna o comprimento de uma string (número de caracteres).
- **Exemplo**:
    
    ```java
    String texto = "Olá";
    int comprimento = texto.length();  // comprimento será 3
    ```
    
---
 `isDigit(char c)`

- **O que faz?**: Verifica se o caractere fornecido é um dígito (0-9).
- **Exemplo**:
    
    ```java
    boolean digito = Character.isDigit('5');  // digito será true
    ```
    