# Controller
``` java

package JavaAulas.aula2.controller;  
  
import JavaAulas.aula2.model.Pessoa;  
  
import java.util.Scanner;  
  
public class CtrlPrograma {  
  
    public static void main(String[] args) {  
        Scanner teclado = new Scanner(System.in);  
        Pessoa[] listaDePessoas = new Pessoa[3];// = [0] [1] [2]  
        int posicao = 0;  // usado para manipular pessoa[i]
  
        while(true) {  
            try {  
                System.out.println("Entre com o CPF ou [Enter] para terminar: ");  
                String c = teclado.nextLine();  
                if(c == null || c.length() == 0)  
                    break;  
  
                System.out.println("Entre com o Nome: ");  
                String n = teclado.nextLine();  
  
                System.out.println("Entre com a Idade: ");  
                int idd = teclado.nextInt();  
                //no lugar?  
                //String aux = teclado.nextLine(); // necessita do aux?                //int idd = Integer.parseInt(aux);  
                Pessoa p = new Pessoa(c, n, idd);  
                listaDePessoas[posicao] = p;  
                posicao++;  
  
            } catch (Exception e) {  
                e.printStackTrace();  
            }  
        }  
        for(int i = 0; i < posicao; i++)  
            System.out.println(listaDePessoas[i]);  
    }  
}

```
---
<font color="#00b050">loop</font> : O while e usado para  se manter no cadastro, é no começo já entra uma condição para sair do mesmo.

posição server como o i de um for loop.

for ao final para apresentar os elementos.

declaração: Pessoa[] listaDePessoas = new Pessoa[3]; // forma de declarar um objeto de vetores

---
---

# Model
```java

package JavaAulas.aula2.model;  
  
public class Pessoa {  
    //  
    // ATRIBUTOS    //    private String cpf;  
    private String nome;  
    private int idade;  
  
    //  
    // MÉTODOS    //    public Pessoa(String c, String n, int i) throws Exception {  
        super();  
        this.setCpf(c);  
        this.setNome(n);  
        this.setIdade(i);  
    }  
  
    public String getCpf() {  
        return this.cpf;  
    }  
  
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
  
    public int getIdade() {  
        return this.idade;  
    }  
  
    public void setIdade(int idade) throws Exception {  
        Pessoa.validarIdade(idade);  
        this.idade = idade;  
    }  
  
    public static void validarCpf(String cpf) throws Exception {  
        if(cpf == null || cpf.length() == 0)  
            throw new Exception("O CPF não pode ser nulo!");  
        if(cpf.length() != 14)  
            throw new Exception("O CPF deve ter 14 caracteres!");  
        for(int i = 0; i < cpf.length(); i++) {  
            char c = cpf.charAt(i);  
            switch(i) {  
                case 3:  
                case 7:  
                    if(c != '.')  
                        throw new Exception("O caracter na posição " + i + " deve ser '.'");  
                    break;  
                case 11:  
                    if(c != '-')  
                        throw new Exception("O caracter na posição 11 deve ser '-'");  
                    break;  
                default:  
                    if(!Character.isDigit(c))  
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
  
    public static void validarIdade(int idade) throws Exception {  
        if(idade < 0 || idade > 150)  
            throw new Exception("A idade passada é inválida: " + idade);  
    }  
  
    @Override  
    public String toString() {  
        return this.cpf + " - " + this.nome + " - " + this.idade;  
    }  
}
```

## conceitos

Quando o construtor de uma classe filha não chama explicitamente o construtor da classe pai usando `super()`, a IDE assume que existe um construtor padrão na classe pai e tenta chamá-lo implicitamente.

THIS! se refere o atributo daquela classe 

A palavra-chave `this` em Java é usada para referenciar o objeto atual da classe onde o código está sendo executado. Aqui estão algumas das principais funções e propósitos do `this`:

1. **Diferenciação de Variáveis**: Quando os parâmetros do método têm o mesmo nome que os atributos da classe, o `this` é usado para diferenciar entre eles. Por exemplo:
    
    ```java
    public class Exemplo {
        private int valor;
    
        public Exemplo(int valor) {
            this.valor = valor; // 'this.valor' refere-se ao atributo da classe, 'valor' ao parâmetro do método
        }
    }
    ```
    
2. **Chamada de Construtores**: O `this` pode ser usado para chamar outro construtor da mesma classe, ajudando a evitar duplicação de código:
    
    ```java
    public class Exemplo {
        private int valor;
        private String nome;
    
        public Exemplo(int valor) {
            this(valor, "Padrão");
        }
    
        public Exemplo(int valor, String nome) {
            this.valor = valor;
            this.nome = nome;
        }
    }
    ```
    
3. **Referência ao Objeto Atual**: Em métodos, o `this` pode ser usado para passar o objeto atual como argumento para outro método ou retornar o objeto atual:
    
    ```java
    public class Exemplo {
        public Exemplo retornaEste() {
            return this;
        }
    }
    ```
    

Usar o `this` corretamente ajuda a evitar ambiguidades e torna o código mais legível
